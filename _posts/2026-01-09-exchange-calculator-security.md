---
layout: post
title: "🔒 XSS 방지 & 성능 튜닝 - 환율 계산기 개발기 (3/3)"
date: 2026-01-09
author: Seansble
tags:
  - DevLog
  - Security
  - Performance
  - JavaScript
  - XSS
description: "금융 계산기에서 필수적인 입력값 검증, XSS 방지, DOM 캐싱을 통한 성능 최적화 전략을 공유합니다."
image: "https://sudanghelp.co.kr/og-image.png"
---

<style>
/* ===== 포스트 전용 가독성 스타일 ===== */
.post-content-custom {
  max-width: 860px;
  margin: 0 auto;
  font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", sans-serif;
}

.post-content-custom p {
  font-size: 17px !important;
  line-height: 1.9 !important;
  color: #374151 !important;
  margin-bottom: 24px !important;
  word-break: keep-all;
}

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

/* 시리즈 네비게이션 */
.series-nav {
  background: linear-gradient(135deg, #1e293b 0%, #334155 100%);
  border-radius: 12px;
  padding: 20px 24px;
  margin-bottom: 40px;
}

.series-nav-title {
  color: #94a3b8;
  font-size: 13px;
  font-weight: 600;
  margin-bottom: 12px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.series-nav-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.series-nav-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 14px;
  border-radius: 8px;
  font-size: 14px;
  color: #cbd5e1;
  text-decoration: none !important;
  transition: all 0.2s;
}

.series-nav-item:hover {
  background: rgba(255,255,255,0.05);
  color: #fff;
}

.series-nav-item.current {
  background: rgba(59, 130, 246, 0.2);
  color: #60a5fa;
  font-weight: 600;
}

.series-nav-item .num {
  background: rgba(255,255,255,0.1);
  width: 24px;
  height: 24px;
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  font-weight: 700;
}

.series-nav-item.current .num {
  background: #3b82f6;
  color: #fff;
}

/* 인트로 박스 - 보안 테마 (빨간색 계열) */
.intro-box {
  background: linear-gradient(135deg, #fef2f2 0%, #fee2e2 100%);
  border: 1px solid #fecaca;
  border-radius: 16px;
  padding: 28px 32px;
  margin-bottom: 48px;
}

.intro-box h2 {
  font-size: 20px !important;
  font-weight: 700 !important;
  color: #991b1b !important;
  margin: 0 0 12px 0 !important;
  border: none !important;
  padding: 0 !important;
}

.intro-box p {
  color: #b91c1c !important;
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

.hl-keyword { color: #c792ea; }
.hl-function { color: #82aaff; }
.hl-string { color: #c3e88d; }
.hl-comment { color: #637777; font-style: italic; }
.hl-property { color: #ffcb6b; }
.hl-method { color: #89ddff; }

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

/* 경고 박스 */
.warning-box {
  background: #fef2f2;
  border-left: 4px solid #ef4444;
  padding: 20px 24px;
  margin: 28px 0;
  border-radius: 0 12px 12px 0;
}

.warning-box p {
  margin-bottom: 0 !important;
  color: #991b1b !important;
  font-size: 16px !important;
}

.warning-box strong {
  color: #dc2626;
}

/* 비교 박스 */
.compare-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  margin: 24px 0;
}

.compare-box {
  padding: 20px;
  border-radius: 12px;
  font-size: 14px;
}

.compare-box.bad {
  background: #fef2f2;
  border: 1px solid #fecaca;
}

.compare-box.good {
  background: #f0fdf4;
  border: 1px solid #bbf7d0;
}

.compare-box .label {
  font-size: 12px;
  font-weight: 700;
  margin-bottom: 8px;
  text-transform: uppercase;
}

.compare-box.bad .label { color: #dc2626; }
.compare-box.good .label { color: #16a34a; }

.compare-box code {
  display: block;
  background: rgba(0,0,0,0.05) !important;
  padding: 12px !important;
  border-radius: 6px !important;
  font-size: 13px !important;
  white-space: pre-wrap;
  word-break: break-all;
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
}

/* 시리즈 완료 박스 */
.series-complete {
  background: linear-gradient(135deg, #ecfdf5 0%, #d1fae5 100%);
  border: 2px solid #10b981;
  border-radius: 16px;
  padding: 32px;
  margin-top: 60px;
  text-align: center;
}

.series-complete h3 {
  color: #065f46 !important;
  font-size: 20px !important;
  margin: 0 0 12px 0 !important;
  border: none !important;
}

.series-complete p {
  color: #047857 !important;
  margin-bottom: 20px !important;
}

.series-links {
  display: flex;
  flex-direction: column;
  gap: 8px;
  max-width: 400px;
  margin: 0 auto;
}

.series-link {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px 16px;
  background: white;
  border: 1px solid #a7f3d0;
  border-radius: 8px;
  text-decoration: none !important;
  font-size: 14px;
  font-weight: 600;
  color: #065f46 !important;
  transition: all 0.2s;
}

.series-link:hover {
  background: #d1fae5;
  border-color: #34d399;
}

.series-link .num {
  background: #10b981;
  color: white;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
}

/* 포스트 네비게이션 */
.post-nav {
  margin-top: 40px;
  padding-top: 40px;
  border-top: 1px solid #e5e7eb;
}

.post-nav-link {
  display: flex;
  align-items: center;
  gap: 12px;
  background: #f8fafc;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 16px 20px;
  text-decoration: none !important;
  transition: all 0.2s;
  max-width: 300px;
}

.post-nav-link:hover {
  border-color: #3b82f6;
  box-shadow: 0 4px 12px rgba(59, 130, 246, 0.15);
}

.post-nav-arrow {
  font-size: 20px;
  color: #3b82f6;
}

.post-nav-label {
  font-size: 12px;
  color: #64748b;
  margin-bottom: 2px;
}

.post-nav-title {
  font-size: 14px;
  font-weight: 700;
  color: #1e293b !important;
}

@media (max-width: 768px) {
  .post-content-custom p { font-size: 16px !important; }
  .section-title { font-size: 20px !important; margin-top: 40px !important; }
  .code-block { padding: 18px 16px !important; font-size: 13px !important; }
  .intro-box { padding: 22px 20px; }
  .cta-section { padding: 32px 24px; }
  .series-nav { padding: 16px 18px; }
  .compare-grid { grid-template-columns: 1fr; }
}
</style>

<div class="post-content-custom" markdown="0">

<!-- 시리즈 네비게이션 -->
<nav class="series-nav">
  <div class="series-nav-title">📚 환율 계산기 개발기 시리즈</div>
  <div class="series-nav-list">
    <a href="{{ '/2026/01/07/exchange-calculator-pwa' | relative_url }}" class="series-nav-item">
      <span class="num">1</span> 오프라인 퍼스트 & PWA 전략
    </a>
    <a href="{{ '/2026/01/08/exchange-calculator-seo' | relative_url }}" class="series-nav-item">
      <span class="num">2</span> 49개국 URL 라우팅 & SEO 최적화
    </a>
    <span class="series-nav-item current">
      <span class="num">3</span> 보안 강화 & 성능 튜닝
    </span>
  </div>
</nav>

<!-- 인트로 -->
<div class="intro-box">
  <h2>🚨 "금융 계산기에서 XSS가 터지면?"</h2>
  <p>
    환율 계산기는 <strong>금융 데이터</strong>를 다루는 도구입니다. localStorage에 저장된 즐겨찾기, 계산 내역이 오염되면 사용자 신뢰를 잃습니다.<br>
    이번 글에서는 <strong>입력값 검증</strong>과 <strong>안전한 DOM 조작</strong> 패턴을 공유합니다.
  </p>
</div>

<!-- 섹션 1 -->
<h2 class="section-title">🛡️ 1. 통화 코드 화이트리스트 검증</h2>

<p>
  사용자가 조작한 통화 코드가 시스템에 들어오면 안 됩니다. <strong>화이트리스트 방식</strong>으로 허용된 코드만 통과시킵니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// 🔒 보안: 허용된 통화 코드만 사용</span>
<span class="hl-keyword">const</span> CURRENCY_INFO = {
    <span class="hl-string">'KRW'</span>: { <span class="hl-property">name</span>: <span class="hl-string">'대한민국 원'</span>, <span class="hl-property">symbol</span>: <span class="hl-string">'₩'</span> },
    <span class="hl-string">'USD'</span>: { <span class="hl-property">name</span>: <span class="hl-string">'미국 달러'</span>, <span class="hl-property">symbol</span>: <span class="hl-string">'$'</span> },
    <span class="hl-string">'VND'</span>: { <span class="hl-property">name</span>: <span class="hl-string">'베트남 동'</span>, <span class="hl-property">symbol</span>: <span class="hl-string">'₫'</span> },
    <span class="hl-comment">// ... 49개 통화</span>
};

<span class="hl-comment">// 화이트리스트 검증 함수</span>
<span class="hl-keyword">function</span> <span class="hl-function">isValidCurrencyCode</span>(code) {
    <span class="hl-keyword">return typeof</span> code === <span class="hl-string">'string'</span> && 
           CURRENCY_INFO.<span class="hl-method">hasOwnProperty</span>(code);
}

<span class="hl-comment">// 사용 예시</span>
<span class="hl-keyword">function</span> <span class="hl-function">setFromCurrency</span>(code) {
    <span class="hl-keyword">if</span> (!<span class="hl-function">isValidCurrencyCode</span>(code)) {
        console.<span class="hl-method">warn</span>(<span class="hl-string">'Invalid currency:'</span>, code);
        <span class="hl-keyword">return</span>;
    }
    <span class="hl-comment">// 안전하게 처리</span>
}</code></pre>

<div class="warning-box">
  <p><strong>⚠️ 왜 중요한가:</strong> <code>&lt;script&gt;alert(1)&lt;/script&gt;</code> 같은 문자열이 통화 코드로 들어오면 XSS 공격이 가능합니다. 화이트리스트로 원천 차단합니다.</p>
</div>

<!-- 섹션 2 -->
<h2 class="section-title">🧱 2. innerHTML 대신 안전한 DOM 생성</h2>

<p>
  <code>innerHTML</code>은 XSS의 주범입니다. 대신 <code>createElement</code> + <code>textContent</code> 패턴을 사용합니다.
</p>

<div class="compare-grid">
  <div class="compare-box bad">
    <div class="label">❌ 위험한 코드</div>
    <code>el.innerHTML = `&lt;span&gt;${userInput}&lt;/span&gt;`;</code>
  </div>
  <div class="compare-box good">
    <div class="label">✅ 안전한 코드</div>
    <code>const span = document.createElement('span');
span.textContent = userInput;
el.appendChild(span);</code>
  </div>
</div>

<p>
  실제 프로젝트에서는 헬퍼 함수를 만들어 일관성을 유지합니다:
</p>

<pre class="code-block"><code><span class="hl-comment">// 🔒 안전한 DOM 생성 헬퍼</span>
<span class="hl-keyword">function</span> <span class="hl-function">createElement</span>(tag, options = {}) {
    <span class="hl-keyword">const</span> el = document.<span class="hl-method">createElement</span>(tag);
    
    <span class="hl-keyword">if</span> (options.className) el.className = options.className;
    <span class="hl-keyword">if</span> (options.textContent) el.textContent = options.textContent;
    <span class="hl-keyword">if</span> (options.onclick) el.onclick = options.onclick;
    
    <span class="hl-comment">// innerHTML은 의도적으로 지원 안 함!</span>
    <span class="hl-keyword">return</span> el;
}

<span class="hl-comment">// 사용 예시</span>
<span class="hl-keyword">const</span> badge = <span class="hl-function">createElement</span>(<span class="hl-string">'span'</span>, {
    <span class="hl-property">className</span>: <span class="hl-string">'currency-badge'</span>,
    <span class="hl-property">textContent</span>: currencyCode  <span class="hl-comment">// 자동 이스케이프</span>
});</code></pre>

<!-- 섹션 3 -->
<h2 class="section-title">⚡ 3. DOM 캐싱으로 60fps 확보</h2>

<p>
  키패드를 누를 때마다 <code>getElementById</code>를 호출하면 구형 기기에서 버벅입니다. <strong>DOM Reference Caching</strong>으로 해결했습니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// 🔥 DOM 캐시 (성능 최적화)</span>
<span class="hl-keyword">const</span> DOM = {};

document.<span class="hl-method">addEventListener</span>(<span class="hl-string">'DOMContentLoaded'</span>, () => {
    <span class="hl-comment">// 한 번만 조회해서 메모리에 저장</span>
    DOM.<span class="hl-property">amountValue</span> = document.<span class="hl-method">getElementById</span>(<span class="hl-string">'amount-value-input'</span>);
    DOM.<span class="hl-property">resultBox</span> = document.<span class="hl-method">getElementById</span>(<span class="hl-string">'conversion-results'</span>);
    DOM.<span class="hl-property">rateInfo</span> = document.<span class="hl-method">getElementById</span>(<span class="hl-string">'rate-update-info'</span>);
});

<span class="hl-keyword">function</span> <span class="hl-function">updateDisplay</span>() {
    <span class="hl-comment">// 캐시된 참조로 즉시 접근 (No DOM lookup)</span>
    DOM.<span class="hl-property">amountValue</span>.<span class="hl-property">textContent</span> = <span class="hl-function">formatNumber</span>(currentInput);
}</code></pre>

<div class="tip-box">
  <p><strong>💡 성능 결과:</strong> 갤럭시 S8급 구형 기기에서 키패드 입력 시 <strong>60fps</strong>를 유지합니다. DOM lookup 비용이 0에 가까워졌기 때문입니다.</p>
</div>

<!-- 섹션 4 -->
<h2 class="section-title">🧹 4. localStorage 데이터 정제</h2>

<p>
  localStorage는 사용자가 직접 수정할 수 있습니다. 불러올 때 항상 검증합니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// localStorage에서 안전하게 불러오기</span>
<span class="hl-keyword">function</span> <span class="hl-function">sanitizeCurrencies</span>(arr) {
    <span class="hl-keyword">if</span> (!Array.<span class="hl-method">isArray</span>(arr)) <span class="hl-keyword">return</span> [<span class="hl-string">'KRW'</span>];
    
    <span class="hl-keyword">const</span> filtered = arr
        .<span class="hl-method">filter</span>(code => <span class="hl-function">isValidCurrencyCode</span>(code))
        .<span class="hl-method">slice</span>(0, 3);  <span class="hl-comment">// 최대 3개</span>
    
    <span class="hl-keyword">return</span> filtered.length > 0 ? filtered : [<span class="hl-string">'KRW'</span>];
}

<span class="hl-comment">// 사용</span>
<span class="hl-keyword">const</span> saved = <span class="hl-function">loadFromStorage</span>(<span class="hl-string">'selectedCurrencies'</span>, []);
<span class="hl-keyword">const</span> currencies = <span class="hl-function">sanitizeCurrencies</span>(saved);  <span class="hl-comment">// 항상 안전</span></code></pre>

<!-- CTA -->
<div class="cta-section">
  <h3>🔒 안전하고 빠른 환율 계산기</h3>
  <p>XSS 방지 · DOM 캐싱 · 입력값 검증</p>
  <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" 
     target="_blank" 
     rel="noopener noreferrer"
     class="cta-button">
    수당헬프 환율 계산기 실행하기 →
  </a>
</div>

<!-- 시리즈 완료 -->
<div class="series-complete">
  <h3>🎉 환율 계산기 개발기 시리즈 완료!</h3>
  <p>3편에 걸쳐 PWA, SEO, 보안 최적화를 다뤘습니다.</p>
  <div class="series-links">
    <a href="{{ '/2026/01/07/exchange-calculator-pwa' | relative_url }}" class="series-link">
      <span class="num">1</span> 오프라인 퍼스트 & PWA 전략
    </a>
    <a href="{{ '/2026/01/08/exchange-calculator-seo' | relative_url }}" class="series-link">
      <span class="num">2</span> 49개국 URL 라우팅 & SEO 최적화
    </a>
    <a href="{{ '/2026/01/09/exchange-calculator-security' | relative_url }}" class="series-link">
      <span class="num">3</span> 보안 강화 & 성능 튜닝
    </a>
  </div>
</div>

<!-- 이전 글 -->
<nav class="post-nav">
  <a href="{{ '/2026/01/08/exchange-calculator-seo' | relative_url }}" class="post-nav-link">
    <span class="post-nav-arrow">←</span>
    <div>
      <div class="post-nav-label">이전 글 (2/3)</div>
      <div class="post-nav-title">49개국 URL 라우팅 & SEO</div>
    </div>
  </a>
</nav>

</div>
