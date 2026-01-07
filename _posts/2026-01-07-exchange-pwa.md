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

<!-- 🎨 스타일 정의 (가독성 & 다크모드 강제 적용) -->
<style>
  /* 1. 전체 레이아웃 */
  .wrapper {
    max-width: 900px !important;
    padding: 0 20px !important;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif !important;
  }
  
  /* 제목 여백 */
  .post-header { margin-bottom: 60px !important; }
  .post-title { margin-top: 20px !important; margin-bottom: 20px !important; line-height: 1.4 !important; }
  .post-meta { margin-bottom: 40px !important; color: #666 !important; }
  
  /* 2. 본문 텍스트 */
  p, li {
    font-size: 17px !important;
    line-height: 1.8 !important;
    color: #333333 !important;
    margin-bottom: 24px !important;
  }

  /* 3. 섹션 제목 스타일 (무조건 통일) */
  h2.section-title {
    margin-top: 70px !important;
    margin-bottom: 24px !important;
    font-size: 26px !important;
    font-weight: 800 !important;
    color: #111111 !important;
    border-bottom: 2px solid #eeeeee;
    padding-bottom: 12px !important;
    line-height: 1.3 !important;
    display: block !important;
  }

  /* 4. 코드 블록 (리얼 블랙 + 쨍한 흰색) */
  pre.code-box {
    background-color: #111111 !important;
    color: #ffffff !important;
    padding: 24px !important;
    border-radius: 8px !important;
    border: 1px solid #333333 !important;
    font-family: 'Consolas', 'Monaco', monospace !important;
    line-height: 1.6 !important;
    font-size: 15px !important;
    margin: 30px 0 !important;
    overflow-x: auto;
    white-space: pre; /* 줄바꿈 유지 */
  }
  
  /* 코드 내부 텍스트 강제 흰색 (기본값) */
  pre.code-box code, 
  pre.code-box span {
    color: #ffffff !important; 
  }

  /* 수동 하이라이팅 (형광색 포인트) */
  .c-blue { color: #569cd6 !important; font-weight: bold; }   /* const, function */
  .c-purple { color: #c586c0 !important; font-weight: bold; } /* async, await, try, if */
  .c-yellow { color: #dcdcaa !important; }  /* 함수명 */
  .c-orange { color: #ce9178 !important; }  /* 문자열 */
  .c-green { color: #6a9955 !important; }   /* 주석 */
  .c-red { color: #ff6b6b !important; }     /* 에러 등 */
  
  /* 5. 인라인 코드 */
  code.inline {
    background-color: #f3f4f6 !important;
    color: #e11d48 !important;
    padding: 2px 6px !important;
    border-radius: 4px !important;
    font-family: monospace !important;
    font-weight: 600 !important;
    font-size: 0.95em !important;
    border: 1px solid #e5e7eb !important;
  }

  /* 6. 링크 스타일 */
  a { text-decoration: none; transition: color 0.2s; }
  a:hover { text-decoration: underline; }
  
  /* 인트로 박스 */
  .intro-box {
    background-color: #f9fafb;
    border: 1px solid #e5e7eb;
    border-radius: 12px;
    padding: 30px;
    margin-bottom: 60px;
  }
</style>

<!-- 본문 시작 -->

<div class="intro-box">
  <h3 style="margin-top: 0; color: #111; font-size: 22px; font-weight: 700; margin-bottom: 12px;">🏝️ "계산대 앞에서 인터넷이 안 터진다면?"</h3>
  <p style="font-size: 17px; line-height: 1.7; color: #4b5563; margin: 0;">
    해외여행 중 가장 당황스러운 순간은 환율 계산기 앱이 로딩되다가 멈출 때입니다.<br>
    저는 이 문제를 해결하기 위해 <strong><a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" style="color: #2563eb; font-weight: 800; border-bottom: 2px solid #2563eb;">[수당헬프 환율 계산기]</a></strong>를 개발하며 <strong>"비행기 모드에서도 0.1초 만에 실행되는 웹"</strong>을 목표로 잡았습니다.
  </p>
</div>

<h2 class="section-title">📡 1. '오프라인'을 고려한 Fail-over 전략</h2>

<p>
환율 데이터는 실시간성이 중요하지만, 여행지에서는 <code class="inline">'가용성(Availability)'</code>이 더 중요합니다. API 호출이 실패했을 때 에러를 띄우는 대신, <strong>캐싱된 데이터</strong>를 보여주는 로직을 구현했습니다.
</p>

<!-- 코드 블록 1 -->
<pre class="code-box"><code><span class="c-green">// calculator.js 핵심 로직</span>
<span class="c-purple">async</span> <span class="c-blue">function</span> <span class="c-yellow">loadRates</span>() {
    <span class="c-blue">const</span> rateInfo = document.<span class="c-yellow">getElementById</span>(<span class="c-orange">'rate-update-info'</span>);
    
    <span class="c-purple">try</span> {
        <span class="c-green">// 1. Edge Network에서 최신 환율 요청</span>
        <span class="c-blue">const</span> response = <span class="c-purple">await</span> fetch(EXCHANGE_API_URL);
        <span class="c-purple">if</span> (!response.ok) <span class="c-purple">throw</span> <span class="c-blue">new</span> Error(<span class="c-orange">'Network Error'</span>);
        
        <span class="c-green">// 2. 성공 시 데이터 갱신</span>
        <span class="c-blue">const</span> data = <span class="c-purple">await</span> response.json();
        <span class="c-yellow">updateRates</span>(data);
        
    } <span class="c-purple">catch</span> (e) {
        <span class="c-green">// 3. 🚨 실패 시: 에러 대신 '오프라인 모드' 전환</span>
        console.<span class="c-yellow">warn</span>(<span class="c-orange">'Offline Mode Activated'</span>);
        
        <span class="c-green">// 기존 LocalStorage 값을 그대로 사용하여 계산기 기능 유지</span>
        rateInfo.textContent = <span class="c-orange">'오프라인 모드 (최근 데이터)'</span>;
        rateInfo.style.color = <span class="c-orange">'#ef4444'</span>; 
    }
}</code></pre>

<div style="background: #fff; border: 1px solid #ddd; border-left: 5px solid #22c55e; padding: 20px; border-radius: 4px; margin: 30px 0;">
  <strong style="color: #15803d; display: block; margin-bottom: 8px; font-size: 16px;">💡 개발 포인트</strong>
  <span style="color: #374151; font-size: 16px; line-height: 1.6;">
  <code class="inline">catch</code> 블록에서 에러를 중단시키지 않고, <strong>사용자에게 "오프라인 모드"임을 인지시키는 UX</strong>로 전환하여 앱의 연속성을 보장했습니다.
  </span>
</div>

<h2 class="section-title">⚡ 2. 저사양 기기를 위한 DOM 캐싱</h2>

<p>
키패드를 누를 때마다 화면이 갱신되어야 하는데, 매번 <code class="inline">document.getElementById</code>를 호출하면 구형 기기에서 <strong>버벅거림(Jank)</strong>이 발생합니다. 이를 <strong>DOM Reference Caching</strong>으로 해결했습니다.
</p>

<!-- 코드 블록 2 -->
<pre class="code-box"><code><span class="c-green">// DOM 요소를 메모리에 한 번만 저장 (Look-up 비용 절감)</span>
<span class="c-blue">const</span> DOM = {};

document.<span class="c-yellow">addEventListener</span>(<span class="c-orange">'DOMContentLoaded'</span>, () => {
    DOM.amountValue = document.<span class="c-yellow">getElementById</span>(<span class="c-orange">'amount-value-input'</span>);
    DOM.resultBox = document.<span class="c-yellow">getElementById</span>(<span class="c-orange">'conversion-results'</span>);
});

<span class="c-blue">function</span> <span class="c-yellow">updateDisplay</span>() {
    <span class="c-green">// 렌더링 시에는 메모리 주소로 즉시 접근 (No Reflow overhead)</span>
    DOM.amountValue.textContent = <span class="c-yellow">formatNumber</span>(currentInput); 
}</code></pre>

<p>
이 최적화를 통해 <strong>갤럭시 S8급 구형 기기</strong>에서도 <strong>60fps의 부드러운 반응 속도</strong>를 확보했습니다.
</p>

<h2 class="section-title">🔍 3. 국가별 SEO를 위한 URL 전략</h2>

<p>
사용자는 "환율 계산기"보다 <strong>"베트남 돈 계산"</strong>처럼 구체적으로 검색합니다. 이를 잡기 위해 URL 라우팅을 자동화했습니다.
</p>

<!-- 코드 블록 3 -->
<pre class="code-box"><code><span class="c-green">// URL path를 감지하여 해당 국가로 자동 세팅</span>
<span class="c-blue">const</span> COUNTRY_PRESETS = {
    <span class="c-orange">'vietnam'</span>: { from: <span class="c-orange">'VND'</span>, to: <span class="c-orange">'KRW'</span> },
    <span class="c-orange">'thailand'</span>: { from: <span class="c-orange">'THB'</span>, to: <span class="c-orange">'KRW'</span> },
    <span class="c-green">// ... 49개국 매핑</span>
};</code></pre>

<br>

<!-- 하단 버튼 -->
<div style="text-align: center; margin-top: 60px; padding: 50px 20px; background: #f8fafc; border-radius: 16px; border: 1px solid #e2e8f0;">
    <h2 style="margin-top: 0 !important; border: none !important; font-size: 26px !important; margin-bottom: 12px !important; color: #111 !important;">🚀 직접 사용해보세요</h2>
    <p style="color: #64748b; margin-bottom: 30px; font-size: 17px;">
        <strong>10개국 환율 계산 / 오프라인 지원 / 가계부 연동</strong>
    </p>
    
    <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" 
       style="
         display: inline-block;
         background: #111;
         color: #fff;
         padding: 18px 36px;
         font-size: 17px;
         font-weight: bold;
         border-radius: 8px;
         transition: transform 0.2s;
       "
    >
       👉 수당헬프 환율 계산기 실행하기
    </a>
</div>
