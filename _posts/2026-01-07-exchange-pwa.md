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

<style>
  /* 1. 전체 레이아웃 */
  .wrapper {
    max-width: 920px !important;
    padding: 0 20px !important;
  }
  
  /* 2. 섹션 제목 (무조건 통일됨) */
  h2.post-section-title {
    margin-top: 60px !important;
    margin-bottom: 24px !important;
    font-size: 26px !important;
    font-weight: 800 !important;
    color: #111827 !important;
    border-bottom: 2px solid #e5e7eb;
    padding-bottom: 12px !important;
    line-height: 1.3 !important;
  }
  
  /* 3. 본문 텍스트 */
  p.post-text {
    font-size: 17px !important;
    line-height: 1.8 !important;
    color: #374151 !important;
    margin-bottom: 24px !important;
  }

  /* 4. 코드 블록 (다크모드) */
  pre {
    background-color: #1e1e1e !important;
    color: #d4d4d4 !important;
    padding: 24px !important;
    border-radius: 12px !important;
    border: 1px solid #333 !important;
    font-family: 'Consolas', 'Monaco', monospace !important;
    line-height: 1.6 !important;
    margin: 30px 0 !important;
    font-size: 14px !important;
    overflow-x: auto;
  }
  
  /* 5. 인라인 코드 강조 */
  code.highlight-text {
    background-color: #f3f4f6 !important;
    color: #dc2626 !important;
    padding: 3px 6px !important;
    border-radius: 4px !important;
    font-family: monospace !important;
    font-weight: 600 !important;
    font-size: 0.95em !important;
    border: 1px solid #e5e7eb !important;
  }

  /* 링크 */
  a { text-decoration: none; transition: color 0.2s; }
  a:hover { text-decoration: underline; }
</style>

<div style="background: #f0f9ff; padding: 32px; border-radius: 16px; border: 1px solid #bae6fd; margin-bottom: 50px;">
  <h3 style="margin-top: 0; color: #0369a1; font-size: 20px; font-weight: 700; margin-bottom: 12px;">🏝️ "계산대 앞에서 인터넷이 안 터진다면?"</h3>
  <p style="font-size: 16px; line-height: 1.7; color: #0c4a6e; margin: 0;">
    해외여행 중 가장 당황스러운 순간은 환율 계산기 앱이 로딩되다가 멈출 때입니다.<br>
    저는 이 문제를 해결하기 위해 <strong><a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" style="color: #0284c7; font-weight: 800; border-bottom: 2px solid #0284c7;">[수당헬프 환율 계산기]</a></strong>를 개발하며 <strong>"비행기 모드에서도 0.1초 만에 실행되는 웹"</strong>을 목표로 잡았습니다.
  </p>
</div>

<h2 class="post-section-title">📡 1. '오프라인'을 고려한 Fail-over 전략</h2>

<p class="post-text">
환율 데이터는 실시간성이 중요하지만, 여행지에서는 <code class="highlight-text">'가용성(Availability)'</code>이 더 중요합니다. API 호출이 실패했을 때 에러를 띄우는 대신, <strong>캐싱된 데이터</strong>를 보여주는 로직을 구현했습니다.
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
<div style="background: #fdf2f8; border-left: 5px solid #db2777; padding: 20px; border-radius: 4px; margin: 30px 0;"> <strong style="color: #be185d; display: block; margin-bottom: 8px; font-size: 16px;">💡 개발 포인트</strong> <span style="color: #831843; font-size: 15px; line-height: 1.6;"> <code class="highlight-text">catch</code> 블록에서 에러를 중단시키지 않고, <strong>사용자에게 "오프라인 모드"임을 인지시키는 UX</strong>로 전환하여 앱의 연속성을 보장했습니다. </span> </div>

<h2 class="post-section-title">⚡ 2. 저사양 기기를 위한 DOM 캐싱</h2>

<p class="post-text"> 키패드를 누를 때마다 화면이 갱신되어야 하는데, 매번 <code class="highlight-text">document.getElementById</code>를 호출하면 구형 기기에서 <strong>버벅거림(Jank)</strong>이 발생합니다. 이를 <strong>DOM Reference Caching</strong>으로 해결했습니다. </p>

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
<p class="post-text"> 이 최적화를 통해 <strong>갤럭시 S8급 구형 기기</strong>에서도 <strong>60fps의 부드러운 반응 속도</strong>를 확보했습니다. </p>

<h2 class="post-section-title">🔍 3. 국가별 SEO를 위한 URL 전략</h2>

<p class="post-text"> 사용자는 "환율 계산기"보다 <strong>"베트남 돈 계산"</strong>처럼 구체적으로 검색합니다. 이를 잡기 위해 URL 라우팅을 자동화했습니다. </p>

JavaScript

// URL path를 감지하여 해당 국가로 자동 세팅
const COUNTRY_PRESETS = {
    'vietnam': { from: 'VND', to: 'KRW' },
    'thailand': { from: 'THB', to: 'KRW' },
    // ... 49개국 매핑
};
<div style="text-align: center; padding: 60px 20px; background: #f9fafb; border-radius: 20px; border: 1px solid #e5e7eb; margin-top: 60px;"> <h2 style="margin-top: 0 !important; border: none !important; font-size: 28px !important; margin-bottom: 16px !important;">🚀 직접 사용해보세요</h2> <p style="color: #6b7280; margin-bottom: 30px; font-size: 16px;"> 앱 설치 없이, 브라우저에서 바로 실행됩니다.


<strong>10개국 환율 계산 / 오프라인 지원 / 가계부 연동</strong> </p>

<a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" 
   style="
     display: inline-block;
     background: #2563eb;
     color: white;
     padding: 18px 40px;
     font-size: 18px;
     font-weight: bold;
     border-radius: 12px;
     box-shadow: 0 4px 6px -1px rgba(37, 99, 235, 0.5);
   "
>
   👉 수당헬프 환율 계산기 실행하기
</a>
</div>
