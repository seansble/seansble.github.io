---
layout: post
title: "✈️ 여행지 로밍이 끊겨도 OK? PWA 환율 계산기 개발기"
date: 2026-01-07
author: Seansble
categories: [Tech]
tags:
  - DevLog
  - PWA
  - Performance
  - JavaScript
  - Cloudflare
  - SEO
description: "베트남, 필리핀 등 여행지 통신 환경을 고려한 오프라인 퍼스트(Offline-First) 환율 계산기 개발 경험을 공유합니다."
image: "https://sudanghelp.co.kr/og-image.png"
---

<style>
/* ===== 포스트 전용 가독성 스타일 ===== */

/* 본문 컨테이너 */
.post-content-custom {
  max-width: 860px;
  margin: 0 auto;
  font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", sans-serif;
}

/* 본문 텍스트 */
.post-content-custom p {
  font-size: 17px !important;
  line-height: 1.9 !important;
  color: #374151 !important;
  margin-bottom: 24px !important;
  word-break: keep-all;
}

/* 링크 */
.post-content-custom a {
  color: #2563eb !important;
  text-decoration: none !important;
  font-weight: 600;
  border-bottom: 1px solid transparent;
  transition: border-color 0.2s;
}

.post-content-custom a:hover {
  border-bottom-color: #2563eb;
}

/* 인트로 박스 */
.intro-box {
  background: linear-gradient(135deg, #f0f9ff 0%, #e0f2fe 100%);
  border: 1px solid #bae6fd;
  border-radius: 16px;
  padding: 28px 32px;
  margin-bottom: 48px;
}

.intro-box h2 {
  font-size: 20px !important;
  font-weight: 700 !important;
  color: #0c4a6e !important;
  margin: 0 0 12px 0 !important;
  border: none !important;
  padding: 0 !important;
}

.intro-box p {
  color: #0369a1 !important;
  margin-bottom: 0 !important;
  font-size: 16px !important;
  line-height: 1.8 !important;
}

/* 섹션 타이틀 */
.section-title {
  margin-top: 56px !important;
  margin-bottom: 20px !important;
  font-size: 24px !important;
  font-weight: 800 !important;
  color: #111827 !important;
  border-bottom: 2px solid #e5e7eb !important;
  padding-bottom: 12px !important;
  line-height: 1.4 !important;
}

/* 코드 블록 */
.code-block {
  background: #0f172a !important;
  color: #e2e8f0 !important;
  padding: 24px 28px !important;
  border-radius: 12px !important;
  font-family: 'JetBrains Mono', 'Fira Code', Consolas, monospace !important;
  font-size: 14px !important;
  line-height: 1.7 !important;
  margin: 24px 0 !important;
  overflow-x: auto !important;
  border: 1px solid #334155 !important;
  white-space: pre !important;
}

/* 코드 하이라이팅 */
.hl-keyword { color: #c792ea; }
.hl-function { color: #82aaff; }
.hl-string { color: #c3e88d; }
.hl-comment { color: #637777; font-style: italic; }
.hl-property { color: #ffcb6b; }
.hl-method { color: #89ddff; }

/* 인라인 코드 */
.post-content-custom code:not(.code-block code) {
  background: #f1f5f9 !important;
  color: #dc2626 !important;
  padding: 3px 8px !important;
  border-radius: 6px !important;
  font-family: 'JetBrains Mono', monospace !important;
  font-size: 0.88em !important;
  font-weight: 600 !important;
  border: 1px solid #e2e8f0 !important;
}

/* 팁 박스 */
.tip-box {
  background: #fefce8;
  border-left: 4px solid #eab308;
  padding: 20px 24px;
  margin: 28px 0;
  border-radius: 0 12px 12px 0;
}

.tip-box p {
  margin-bottom: 0 !important;
  color: #713f12 !important;
  font-size: 16px !important;
}

.tip-box strong {
  color: #a16207;
}

/* CTA 섹션 */
.cta-section {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  padding: 40px 36px;
  border-radius: 16px;
  text-align: center;
  margin-top: 56px;
}

.cta-section h3 {
  color: white !important;
  font-size: 22px !important;
  margin: 0 0 10px 0 !important;
  border: none !important;
}

.cta-section p {
  color: #94a3b8 !important;
  margin-bottom: 24px !important;
  font-size: 15px !important;
}

.cta-button {
  display: inline-block;
  background: linear-gradient(to right, #3b82f6, #8b5cf6);
  color: white !important;
  padding: 16px 32px;
  font-size: 16px;
  font-weight: 700;
  border-radius: 10px;
  text-decoration: none !important;
  border-bottom: none !important;
  transition: transform 0.2s, box-shadow 0.2s;
}

.cta-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(59, 130, 246, 0.35);
  color: white !important;
  border-bottom: none !important;
}

/* 강조 텍스트 */
.post-content-custom strong {
  color: #1e293b;
  font-weight: 700;
}

/* 모바일 대응 */
@media (max-width: 768px) {
  .post-content-custom p {
    font-size: 16px !important;
  }
  
  .section-title {
    font-size: 20px !important;
    margin-top: 40px !important;
  }
  
  .code-block {
    padding: 18px 16px !important;
    font-size: 13px !important;
    border-radius: 8px !important;
  }
  
  .intro-box {
    padding: 22px 20px;
  }
  
  .cta-section {
    padding: 32px 24px;
  }
}
</style>

<div class="post-content-custom" markdown="0">

<!-- 인트로 -->
<div class="intro-box">
  <h2>🏝️ "계산대 앞에서 인터넷이 안 터진다면?"</h2>
  <p>
    해외여행 중 가장 당황스러운 순간은 환율 계산기 앱이 로딩되다가 멈출 때입니다.<br>
    저는 이 문제를 해결하기 위해 <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" rel="noopener noreferrer">수당헬프 환율 계산기</a>를 개발하며 <strong>"비행기 모드에서도 0.1초 만에 실행되는 웹"</strong>을 목표로 잡았습니다.
  </p>
</div>

<!-- 섹션 1 -->
<h2 class="section-title">📡 1. '오프라인'을 고려한 Fail-over 전략</h2>

<p>
  환율 데이터는 실시간성이 중요하지만, 여행지에서는 <strong>'가용성(Availability)'</strong>이 더 중요합니다. 
  API 호출이 실패했을 때 에러를 띄우는 대신, 캐싱된 데이터를 보여주는 로직을 구현했습니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// calculator.js 핵심 로직</span>
<span class="hl-keyword">async function</span> <span class="hl-function">loadRates</span>() {
    <span class="hl-keyword">const</span> rateInfo = document.<span class="hl-method">getElementById</span>(<span class="hl-string">'rate-update-info'</span>);
    
    <span class="hl-keyword">try</span> {
        <span class="hl-comment">// 1. Edge Network에서 최신 환율 요청</span>
        <span class="hl-keyword">const</span> response = <span class="hl-keyword">await</span> <span class="hl-function">fetch</span>(EXCHANGE_API_URL);
        <span class="hl-keyword">if</span> (!response.ok) <span class="hl-keyword">throw new</span> <span class="hl-function">Error</span>(<span class="hl-string">'Network Error'</span>);
        
        <span class="hl-comment">// 2. 성공 시 데이터 갱신</span>
        <span class="hl-keyword">const</span> data = <span class="hl-keyword">await</span> response.<span class="hl-method">json</span>();
        <span class="hl-function">updateRates</span>(data);
        
    } <span class="hl-keyword">catch</span> (e) {
        <span class="hl-comment">// 3. 🚨 실패 시: 에러 대신 '오프라인 모드' 전환</span>
        console.<span class="hl-method">warn</span>(<span class="hl-string">'Offline Mode Activated'</span>);
        
        <span class="hl-comment">// 기존 LocalStorage 값을 그대로 사용</span>
        rateInfo.<span class="hl-property">textContent</span> = <span class="hl-string">'오프라인 모드 (최근 데이터)'</span>;
        rateInfo.<span class="hl-property">style</span>.<span class="hl-property">color</span> = <span class="hl-string">'#ef4444'</span>; 
    }
}</code></pre>

<div class="tip-box">
  <p><strong>💡 개발 포인트:</strong> <code>catch</code> 블록에서 에러를 중단시키지 않고, 사용자에게 "오프라인 모드"임을 인지시키는 UX로 전환하여 앱의 연속성을 보장했습니다.</p>
</div>

<!-- 섹션 2 -->
<h2 class="section-title">⚡ 2. 저사양 기기를 위한 DOM 캐싱</h2>

<p>
  키패드를 누를 때마다 화면이 갱신되어야 하는데, 매번 <code>document.getElementById</code>를 호출하면 
  구형 기기에서 버벅거림(Jank)이 발생합니다. 이를 <strong>DOM Reference Caching</strong>으로 해결했습니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// DOM 요소를 메모리에 한 번만 저장 (Look-up 비용 절감)</span>
<span class="hl-keyword">const</span> DOM = {};

document.<span class="hl-method">addEventListener</span>(<span class="hl-string">'DOMContentLoaded'</span>, () => {
    DOM.<span class="hl-property">amountValue</span> = document.<span class="hl-method">getElementById</span>(<span class="hl-string">'amount-value-input'</span>);
    DOM.<span class="hl-property">resultBox</span> = document.<span class="hl-method">getElementById</span>(<span class="hl-string">'conversion-results'</span>);
});

<span class="hl-keyword">function</span> <span class="hl-function">updateDisplay</span>() {
    <span class="hl-comment">// 렌더링 시에는 메모리 주소로 즉시 접근</span>
    DOM.<span class="hl-property">amountValue</span>.<span class="hl-property">textContent</span> = <span class="hl-function">formatNumber</span>(currentInput); 
}</code></pre>

<p>
  이 최적화를 통해 <strong>갤럭시 S8급 구형 기기에서도 60fps</strong>의 부드러운 반응 속도를 확보했습니다.
</p>

<!-- 섹션 3 -->
<h2 class="section-title">🔍 3. 국가별 SEO를 위한 URL 전략</h2>

<p>
  사용자는 "환율 계산기"보다 <strong>"베트남 돈 계산"</strong>처럼 구체적으로 검색합니다. 
  이를 잡기 위해 URL 라우팅을 자동화했습니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// URL path를 감지하여 해당 국가로 자동 세팅</span>
<span class="hl-keyword">const</span> COUNTRY_PRESETS = {
    <span class="hl-string">'vietnam'</span>:   { <span class="hl-property">from</span>: <span class="hl-string">'VND'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-string">'thailand'</span>:  { <span class="hl-property">from</span>: <span class="hl-string">'THB'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-string">'japan'</span>:     { <span class="hl-property">from</span>: <span class="hl-string">'JPY'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-string">'usa'</span>:       { <span class="hl-property">from</span>: <span class="hl-string">'USD'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-comment">// ... 49개국 매핑</span>
};</code></pre>

<!-- CTA -->
<div class="cta-section">
  <h3>🚀 직접 사용해보세요</h3>
  <p>10개국 환율 계산 · 오프라인 지원 · 가계부 연동</p>
  <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" 
     target="_blank" 
     rel="noopener noreferrer"
     class="cta-button">
    수당헬프 환율 계산기 실행하기 →
  </a>
</div>

</div>
