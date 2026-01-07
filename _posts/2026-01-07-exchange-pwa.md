---
layout: post
title: "✈️ 여행지 로밍이 끊겨도 OK? PWA 환율 계산기 개발기"
date: 2026-01-07
author: Seansble
categories: [Tech, DevLog]
tags: [PWA, Performance, JavaScript, Cloudflare, SEO]
description: "베트남, 필리핀 등 여행지 통신 환경을 고려한 오프라인 퍼스트(Offline-First) 환율 계산기 개발 경험을 공유합니다."
image: "https://sudanghelp.co.kr/og-image.png"
---

<div style="background: #f1f5f9; padding: 25px; border-radius: 12px; border-left: 6px solid #3b82f6; color: #334155; margin-bottom: 40px; box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);">
  <h3 style="margin-top: 0; color: #1e293b;">🏝️ "계산대 앞에서 인터넷이 안 터진다면?"</h3>
  <p style="font-size: 1.05em; line-height: 1.7; margin-bottom: 0;">
    해외여행 중 가장 당황스러운 순간은 환율 계산기 앱이 로딩되다가 멈출 때입니다.<br>
    저는 이 문제를 해결하기 위해 <strong><a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" style="color: #2563eb; text-decoration: none; font-weight: 800; border-bottom: 2px solid #2563eb;">[수당헬프 환율 계산기]</a></strong>를 개발하며 <strong>"비행기 모드에서도 0.1초 만에 실행되는 웹"</strong>을 목표로 잡았습니다.
  </p>
</div>

---

## 📡 1. '오프라인'을 고려한 Fail-over 전략

<p style="font-size: 1.1em; line-height: 1.8; color: #475569;">
환율 데이터는 실시간성이 중요하지만, 여행지에서는 <strong>'가용성(Availability)'</strong>이 더 중요합니다. API 호출이 실패했을 때 에러를 띄우는 대신, <strong>캐싱된 데이터</strong>를 보여주는 로직을 구현했습니다.
</p>

```javascript
// calculator.js 핵심 로직
async function loadRates() {
    const rateInfo = document.getElementById('rate-update-info');
    
    try {
        // 1. Edge Network에서 최신 환율 요청
        const response = await fetch(EXCHANGE_API_URL);
        if (!response.ok) throw new Error('Network Error');
        
        // 2. 성공 시 데이터 갱신
        const data = await response.json();
        updateRates(data);
        
    } catch (e) {
        // 3. 🚨 실패 시: 에러 대신 '오프라인 모드' 전환
        console.warn('Offline Mode Activated');
        
        // 기존 LocalStorage 값을 그대로 사용하여 계산기 기능 유지
        rateInfo.textContent = '오프라인 모드 (최근 데이터)';
        rateInfo.style.color = '#ef4444'; 
    }
}
<div style="background: #ecfdf5; border: 1px solid #a7f3d0; border-radius: 8px; padding: 15px 20px; margin: 20px 0;"> <strong style="color: #059669;">💡 개발 포인트</strong>


<span style="color: #065f46; font-size: 0.95em;"> <code>catch</code> 블록에서 에러를 중단시키지 않고, <strong>사용자에게 "오프라인 모드"임을 인지시키는 UX</strong>로 전환하여 앱의 연속성을 보장했습니다. </span> </div>

⚡ 2. 저사양 기기를 위한 DOM 캐싱
<p style="font-size: 1.1em; line-height: 1.8; color: #475569;"> 키패드를 누를 때마다 화면이 갱신되어야 하는데, 매번 <code>document.getElementById</code>를 호출하면 구형 기기에서 <strong>버벅거림(Jank)</strong>이 발생합니다. 이를 <strong>DOM Reference Caching</strong>으로 해결했습니다. </p>

JavaScript

// DOM 요소를 메모리에 한 번만 저장 (Look-up 비용 절감)
const DOM = {};

document.addEventListener('DOMContentLoaded', () => {
    DOM.amountValue = document.getElementById('amount-value-input');
    DOM.resultBox = document.getElementById('conversion-results');
});

function updateDisplay() {
    // 렌더링 시에는 메모리 주소로 즉시 접근 (No Reflow overhead)
    DOM.amountValue.textContent = formatNumber(currentInput); 
}
<p style="background: #fffbeb; padding: 10px 15px; border-left: 4px solid #f59e0b; color: #92400e;"> 🚀 <strong>Result:</strong> 갤럭시 S8급 구형 기기에서도 <strong>60fps의 부드러운 반응 속도</strong>를 확보했습니다. </p>

🔍 3. 국가별 SEO를 위한 URL 전략
<p style="font-size: 1.1em; line-height: 1.8; color: #475569;"> 사용자는 "환율 계산기"보다 <strong>"베트남 돈 계산"</strong>처럼 구체적으로 검색합니다. 이를 잡기 위해 URL 라우팅을 자동화했습니다. </p>

JavaScript

// URL path를 감지하여 해당 국가로 자동 세팅
const COUNTRY_PRESETS = {
    'vietnam': { from: 'VND', to: 'KRW' },
    'thailand': { from: 'THB', to: 'KRW' },
    // ... 49개국 매핑
};
<div style="text-align: center; padding: 40px 20px; background: linear-gradient(to bottom right, #f8fafc, #eff6ff); border-radius: 16px; border: 1px solid #e2e8f0;"> <h2 style="margin-top: 0; color: #1e293b; font-size: 1.8em;">🚀 직접 사용해보세요</h2> <p style="color: #64748b; margin-bottom: 30px; font-size: 1.1em;"> 앱 설치 없이, 브라우저에서 바로 실행됩니다.


<strong>10개국 환율 계산 / 오프라인 지원 / 가계부 연동</strong> </p>

<a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" 
   style="
     display: inline-block;
     background: #2563eb;
     color: white;
     padding: 16px 32px;
     font-size: 1.2em;
     font-weight: bold;
     text-decoration: none;
     border-radius: 50px;
     box-shadow: 0 10px 15px -3px rgba(37, 99, 235, 0.3);
     transition: all 0.2s;
   "
   onmouseover="this.style.transform='translateY(-2px)'; this.style.boxShadow='0 20px 25px -5px rgba(37, 99, 235, 0.4)';"
   onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 10px 15px -3px rgba(37, 99, 235, 0.3)';"
>
   👉 수당헬프 환율 계산기 실행하기
</a>
</div>
