---
layout: post
title: "여행지 로밍이 끊겨도 OK? PWA 환율 계산기 개발기 (Cloudflare & DOM 최적화)"
date: 2026-01-07
categories: tech pwa performance
description: "베트남, 필리핀 등 여행지 통신 환경을 고려한 오프라인 퍼스트(Offline-First) 환율 계산기 개발 경험을 공유합니다."
image: "[https://sudanghelp.co.kr/og-image.png](https://sudanghelp.co.kr/og-image.png)"
---

<div style="background-color: #f8f9fa; padding: 20px; border-left: 5px solid #007bff; color: #555; line-height: 1.8; margin-bottom: 40px; border-radius: 4px;">
  <p style="margin-top: 0;">해외여행 중 가장 당황스러운 순간은? 바로 <strong>"계산대 앞에서 인터넷이 안 터질 때"</strong>입니다.<br>
  특히 베트남이나 필리핀의 외곽 지역에서는 환율 계산기 앱이 로딩되다가 멈추는 경우가 허다합니다.</p>
  
  <p style="margin-bottom: 0;">저는 이 문제를 해결하기 위해 <strong><a href="[https://sudanghelp.co.kr/travel/exchange-calculator/](https://sudanghelp.co.kr/travel/exchange-calculator/)" target="_blank" style="color: #007bff; text-decoration: none; font-weight: bold;">[수당헬프 환율 계산기]</a></strong>를 개발하면서, <strong>"비행기 모드에서도 즉시 실행되는 웹"</strong>을 목표로 잡았습니다. 실제 프로덕션 코드에 적용된 <strong>PWA 전략</strong>과 <strong>성능 최적화 패턴</strong>을 공유합니다.</p>
</div>

<hr style="margin: 40px 0; border: 0; border-top: 1px solid #eee;">

## 1. '오프라인'을 고려한 Fail-over 전략

환율 데이터는 실시간성이 중요하지만, 여행지 환경에서는 **'가용성(Availability)'**이 더 중요합니다. API 호출이 실패했을 때 사용자에게 "에러"를 띄우는 대신, 기존에 캐싱된 데이터를 보여주는 **Fail-over 로직**을 `calculator.js`에 구현했습니다.

### 🛠️ 실제 구현 코드 (JavaScript)

```javascript
// calculator.js 핵심 로직 (Cloudflare Workers KV 연동)
async function loadRates() {
    const rateInfo = document.getElementById('rate-update-info');
    
    try {
        // 1. Cloudflare Workers KV에서 최신 환율 요청 (Edge Network 활용)
        const response = await fetch(EXCHANGE_API_URL);
        
        if (!response.ok) throw new Error('Network response was not ok');
        
        const data = await response.json();
        
        // 2. 성공 시 메모리 및 스토리지에 갱신
        Object.keys(EXCHANGE_RATES).forEach(code => {
            if (data.rates[code]) EXCHANGE_RATES[code] = data.rates[code];
        });
        
        rateInfo.textContent = `${getCurrentTime()} 기준`; // 성공 시 시간 갱신
        
    } catch (e) {
        // 3. 🚨 실패 시(오프라인): 에러를 내지 않고 '오프라인 모드'로 전환
        console.error('환율 로드 실패:', e);
        
        // 기존 하드코딩된 값(EXCHANGE_RATES)이나 LocalStorage 값을 그대로 사용
        rateInfo.textContent = '오프라인 모드 (최근 데이터)';
        rateInfo.style.color = '#ff6b6b'; // UX: 붉은색으로 상태 알림
    }
}
<blockquote style="border-left: 4px solid #28a745; padding-left: 15px; color: #666; margin: 20px 0; background: #f1f8e9; padding: 15px;"> <strong>💡 개발 포인트:</strong>


<code>catch</code> 블록에서 에러를 삼키고(Swallow), 대신 <strong>사용자에게 "오프라인 모드"임을 인지시키는 UX</strong>를 제공함으로써, 네트워크가 불안정한 환경에서도 계산기가 멈추지 않도록 했습니다. </blockquote>

2. 저사양 기기를 위한 DOM 캐싱 (Performance)
환율 계산기는 키패드를 누를 때마다(input 이벤트) 화면이 즉각적으로 갱신되어야 합니다. 매번 document.getElementById를 호출하면 오래된 안드로이드 기기에서 미세한 버벅거림(Jank)이 발생할 수 있습니다.

이를 방지하기 위해 DOM Reference Caching 패턴을 적용하여 렌더링 성능을 극대화했습니다.

JavaScript

// calculator.js - DOM 캐싱 객체 선언
const DOM = {};

document.addEventListener('DOMContentLoaded', () => {
    // 1. 초기화 시점에 DOM 요소를 메모리에 한 번만 저장 (Look-up 비용 절감)
    DOM.amountValue = document.getElementById('amount-value-input');
    DOM.amountKorean = document.getElementById('amount-korean-input');
    DOM.conversionResults = document.getElementById('conversion-results');
    
    // ... 초기화 로직 ...
});

function updateDisplay() {
    // 2. 렌더링 시에는 DOM 탐색 없이 메모리 주소로 즉시 접근
    // formatNumber 함수로 천 단위 콤마(,) 포맷팅 적용
    DOM.amountValue.textContent = formatNumber(currentInput); 
    
    // ...
}
이 최적화를 통해 갤럭시 S8급 구형 기기에서도 60fps의 부드러운 키패드 반응 속도를 확보할 수 있었습니다.

3. 국가별 SEO를 위한 URL 프리셋 전략
사용자는 "환율 계산기"라고 검색하기보다 "베트남 환율 계산기", **"태국 바트 계산"**처럼 구체적으로 검색합니다. 이를 잡기 위해 COUNTRY_PRESETS 객체를 활용해 URL 라우팅을 처리했습니다.

JavaScript

// calculator.js - 국가별 프리셋 매핑
const COUNTRY_PRESETS = {
    'vietnam': { from: 'VND', to: 'KRW' },
    'thailand': { from: 'THB', to: 'KRW' },
    'japan': { from: 'JPY', to: 'KRW' },
    // ... 49개국 데이터 매핑
};

// URL path 감지하여 자동 세팅
const pathParts = location.pathname.split('/').filter(Boolean);
let countrySlug = pathParts[pathParts.length - 1]; 
const preset = COUNTRY_PRESETS[countrySlug];

if (preset) {
    updateFromDisplay(preset.from); // 해당 국가 통화로 자동 세팅
}
이 덕분에 사용자는 별도의 설정 없이, 검색해서 들어온 국가의 환율을 바로 계산할 수 있습니다.

<hr style="margin: 40px 0; border: 0; border-top: 1px solid #eee;">

🚀 결과 및 데모
위 기술들이 적용된 계산기는 현재 **수당헬프(SudangHelp)**에서 서비스 중입니다. PWA가 적용되어 있어 홈 화면에 추가하면 앱처럼 사용할 수 있습니다.

<div style="background-color: #f1f8ff; border: 1px solid #c8e1ff; padding: 20px; border-radius: 8px; text-align: center; margin: 30px 0;"> <h3 style="margin-top: 0; color: #0366d6;">✈️ 실제 서비스 사용해보기</h3> <p style="margin-bottom: 20px; color: #555;">오프라인에서도 작동하는 10개국 환율 계산기를 경험해보세요.</p> <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" style="background-color: #2ea44f; color: white; padding: 12px 24px; text-decoration: none; border-radius: 6px; font-weight: bold; font-size: 1.1em; display: inline-block; box-shadow: 0 2px 5px rgba(0,0,0,0.2);"> 👉 수당헬프 환율 계산기 바로가기 </a> </div>

<p>다음 포스팅에서는 <code>common.css</code>에서 <strong>모바일 가상 키보드가 올라올 때 뷰포트가 깨지는 문제</strong>를 <code>calc(100dvh)</code>로 해결한 CSS 트릭에 대해 다뤄보겠습니다.</p>
