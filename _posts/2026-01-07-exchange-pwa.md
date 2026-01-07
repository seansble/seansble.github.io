---
layout: null
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
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>✈️ 여행지 로밍이 끊겨도 OK? PWA 환율 계산기 개발기 | 수당헬프 기술 블로그</title>
  <meta name="description" content="베트남, 필리핀 등 여행지 통신 환경을 고려한 오프라인 퍼스트(Offline-First) 환율 계산기 개발 경험을 공유합니다.">
  <meta property="og:image" content="https://sudanghelp.co.kr/og-image.png">
  <link rel="canonical" href="{{ site.url }}{{ page.url }}">
  <style>
    /* ===== 포스트 전용 스타일 (Scoped) ===== */
    
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background-color: #f8f9fa;
      color: #333;
      font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", Roboto, sans-serif;
      line-height: 1.7;
    }

    /* 1. 레이아웃 - 넓은 너비 */
    .post-container {
      max-width: 1100px;
      margin: 0 auto;
      padding: 0 24px;
    }

    /* 2. 헤더 영역 */
    .post-header {
      background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
      color: white;
      padding: 60px 0 50px;
      margin-bottom: 50px;
      border-radius: 0 0 24px 24px;
    }

    .post-header-inner {
      max-width: 1100px;
      margin: 0 auto;
      padding: 0 24px;
    }

    .post-title {
      font-size: 36px;
      font-weight: 800;
      line-height: 1.3;
      margin-bottom: 16px;
      background: linear-gradient(to right, #60a5fa, #a78bfa);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .post-meta {
      color: #94a3b8;
      font-size: 15px;
      display: flex;
      gap: 20px;
      flex-wrap: wrap;
    }

    .post-meta span {
      display: flex;
      align-items: center;
      gap: 6px;
    }

    /* 3. 본문 콘텐츠 */
    .post-content {
      background: white;
      padding: 50px;
      border-radius: 16px;
      border: 1px solid #e2e8f0;
      margin-bottom: 40px;
    }

    .post-content p {
      font-size: 17px;
      line-height: 1.85;
      color: #334155;
      margin-bottom: 24px;
    }

    .post-content a {
      color: #2563eb;
      text-decoration: none;
      font-weight: 600;
      border-bottom: 1px solid transparent;
      transition: border-color 0.2s;
    }

    .post-content a:hover {
      border-bottom-color: #2563eb;
    }

    /* 4. 인트로 박스 */
    .intro-box {
      background: linear-gradient(135deg, #f0f9ff 0%, #e0f2fe 100%);
      border: 1px solid #bae6fd;
      border-radius: 12px;
      padding: 32px;
      margin-bottom: 50px;
    }

    .intro-box h2 {
      font-size: 22px;
      font-weight: 700;
      color: #0c4a6e;
      margin-bottom: 12px;
    }

    .intro-box p {
      color: #0369a1;
      margin-bottom: 0;
    }

    /* 5. 섹션 타이틀 */
    .section-title {
      margin-top: 60px;
      margin-bottom: 24px;
      font-size: 26px;
      font-weight: 800;
      color: #1e293b;
      border-bottom: 2px solid #e2e8f0;
      padding-bottom: 12px;
      line-height: 1.4;
    }

    /* 6. 코드 블록 - 넓게! */
    .code-box {
      background-color: #0f172a;
      color: #e2e8f0;
      padding: 28px 32px;
      border-radius: 12px;
      font-family: 'JetBrains Mono', 'Fira Code', 'Consolas', monospace;
      font-size: 14px;
      line-height: 1.7;
      margin: 28px 0;
      overflow-x: auto;
      border: 1px solid #334155;
      white-space: pre;
      tab-size: 4;
    }

    .code-box code {
      color: #e2e8f0;
      font-family: inherit;
    }

    /* 코드 하이라이팅 */
    .c-keyword { color: #c792ea; }      /* const, function, async, await */
    .c-function { color: #82aaff; }     /* 함수명 */
    .c-string { color: #c3e88d; }       /* 문자열 */
    .c-comment { color: #637777; font-style: italic; }  /* 주석 */
    .c-number { color: #f78c6c; }       /* 숫자 */
    .c-property { color: #ffcb6b; }     /* 속성 */
    .c-method { color: #89ddff; }       /* 메서드 */

    /* 7. 팁 박스 */
    .tip-box {
      background: #fefce8;
      border-left: 4px solid #eab308;
      padding: 20px 24px;
      margin: 28px 0;
      border-radius: 0 8px 8px 0;
    }

    .tip-box strong {
      color: #a16207;
    }

    .tip-box p {
      margin-bottom: 0;
      color: #713f12;
    }

    /* 8. 인라인 코드 */
    .inline-code {
      background-color: #f1f5f9;
      color: #dc2626;
      padding: 2px 8px;
      border-radius: 4px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.9em;
      font-weight: 600;
      border: 1px solid #e2e8f0;
    }

    /* 9. CTA 버튼 */
    .cta-section {
      background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
      padding: 40px;
      border-radius: 16px;
      text-align: center;
      margin-top: 50px;
    }

    .cta-section h3 {
      color: white;
      font-size: 24px;
      margin-bottom: 12px;
    }

    .cta-section p {
      color: #94a3b8;
      margin-bottom: 24px;
    }

    .cta-button {
      display: inline-block;
      background: linear-gradient(to right, #3b82f6, #8b5cf6);
      color: white;
      padding: 16px 36px;
      font-size: 17px;
      font-weight: 700;
      border-radius: 8px;
      text-decoration: none;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .cta-button:hover {
      transform: translateY(-2px);
      box-shadow: 0 10px 20px rgba(59, 130, 246, 0.3);
    }

    /* 10. 푸터 네비게이션 */
    .post-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 30px 0;
      border-top: 1px solid #e2e8f0;
      margin-top: 40px;
    }

    .back-link {
      color: #64748b;
      text-decoration: none;
      font-weight: 600;
      display: flex;
      align-items: center;
      gap: 8px;
      transition: color 0.2s;
    }

    .back-link:hover {
      color: #2563eb;
    }

    /* 11. 모바일 대응 */
    @media (max-width: 768px) {
      .post-header {
        padding: 40px 0 30px;
        border-radius: 0;
      }

      .post-title {
        font-size: 26px;
      }

      .post-content {
        padding: 28px 20px;
      }

      .section-title {
        font-size: 22px;
        margin-top: 40px;
      }

      .code-box {
        padding: 20px 16px;
        font-size: 13px;
        border-radius: 8px;
      }

      .cta-section {
        padding: 30px 20px;
      }

      .post-footer {
        flex-direction: column;
        gap: 16px;
      }
    }
  </style>
</head>
<body>

  <!-- 헤더 -->
  <header class="post-header">
    <div class="post-header-inner">
      <h1 class="post-title">✈️ 여행지 로밍이 끊겨도 OK? PWA 환율 계산기 개발기</h1>
      <div class="post-meta">
        <span>📅 2026-01-07</span>
        <span>✍️ Seansble</span>
        <span>🏷️ PWA, Performance, JavaScript</span>
      </div>
    </div>
  </header>

  <!-- 본문 -->
  <main class="post-container">
    <article class="post-content">

      <!-- 인트로 -->
      <div class="intro-box">
        <h2>🏝️ "계산대 앞에서 인터넷이 안 터진다면?"</h2>
        <p>
          해외여행 중 가장 당황스러운 순간은 환율 계산기 앱이 로딩되다가 멈출 때입니다.<br>
          저는 이 문제를 해결하기 위해 <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" rel="noopener noreferrer">수당헬프 환율 계산기</a>를 개발하며 <strong>"비행기 모드에서도 0.1초 만에 실행되는 웹"</strong>을 목표로 잡았습니다.
        </p>
      </div>

      <!-- 섹션 1: Fail-over 전략 -->
      <h2 class="section-title">📡 1. '오프라인'을 고려한 Fail-over 전략</h2>
      
      <p>
        환율 데이터는 실시간성이 중요하지만, 여행지에서는 <strong>'가용성(Availability)'</strong>이 더 중요합니다. 
        API 호출이 실패했을 때 에러를 띄우는 대신, 캐싱된 데이터를 보여주는 로직을 구현했습니다.
      </p>

<pre class="code-box"><code><span class="c-comment">// calculator.js 핵심 로직</span>
<span class="c-keyword">async function</span> <span class="c-function">loadRates</span>() {
    <span class="c-keyword">const</span> rateInfo = document.<span class="c-method">getElementById</span>(<span class="c-string">'rate-update-info'</span>);
    
    <span class="c-keyword">try</span> {
        <span class="c-comment">// 1. Edge Network에서 최신 환율 요청</span>
        <span class="c-keyword">const</span> response = <span class="c-keyword">await</span> <span class="c-function">fetch</span>(EXCHANGE_API_URL);
        <span class="c-keyword">if</span> (!response.ok) <span class="c-keyword">throw new</span> <span class="c-function">Error</span>(<span class="c-string">'Network Error'</span>);
        
        <span class="c-comment">// 2. 성공 시 데이터 갱신</span>
        <span class="c-keyword">const</span> data = <span class="c-keyword">await</span> response.<span class="c-method">json</span>();
        <span class="c-function">updateRates</span>(data);
        
    } <span class="c-keyword">catch</span> (e) {
        <span class="c-comment">// 3. 🚨 실패 시: 에러 대신 '오프라인 모드' 전환</span>
        console.<span class="c-method">warn</span>(<span class="c-string">'Offline Mode Activated'</span>);
        
        <span class="c-comment">// 기존 LocalStorage 값을 그대로 사용하여 계산기 기능 유지</span>
        rateInfo.<span class="c-property">textContent</span> = <span class="c-string">'오프라인 모드 (최근 데이터)'</span>;
        rateInfo.<span class="c-property">style</span>.<span class="c-property">color</span> = <span class="c-string">'#ef4444'</span>; 
    }
}</code></pre>

      <div class="tip-box">
        <p><strong>💡 개발 포인트:</strong> <code class="inline-code">catch</code> 블록에서 에러를 중단시키지 않고, 사용자에게 "오프라인 모드"임을 인지시키는 UX로 전환하여 앱의 연속성을 보장했습니다.</p>
      </div>

      <!-- 섹션 2: DOM 캐싱 -->
      <h2 class="section-title">⚡ 2. 저사양 기기를 위한 DOM 캐싱</h2>
      
      <p>
        키패드를 누를 때마다 화면이 갱신되어야 하는데, 매번 <code class="inline-code">document.getElementById</code>를 호출하면 
        구형 기기에서 버벅거림(Jank)이 발생합니다. 이를 <strong>DOM Reference Caching</strong>으로 해결했습니다.
      </p>

<pre class="code-box"><code><span class="c-comment">// DOM 요소를 메모리에 한 번만 저장 (Look-up 비용 절감)</span>
<span class="c-keyword">const</span> DOM = {};

document.<span class="c-method">addEventListener</span>(<span class="c-string">'DOMContentLoaded'</span>, () => {
    DOM.<span class="c-property">amountValue</span> = document.<span class="c-method">getElementById</span>(<span class="c-string">'amount-value-input'</span>);
    DOM.<span class="c-property">resultBox</span> = document.<span class="c-method">getElementById</span>(<span class="c-string">'conversion-results'</span>);
});

<span class="c-keyword">function</span> <span class="c-function">updateDisplay</span>() {
    <span class="c-comment">// 렌더링 시에는 메모리 주소로 즉시 접근 (No Reflow overhead)</span>
    DOM.<span class="c-property">amountValue</span>.<span class="c-property">textContent</span> = <span class="c-function">formatNumber</span>(currentInput); 
}</code></pre>

      <p>
        이 최적화를 통해 <strong>갤럭시 S8급 구형 기기에서도 60fps</strong>의 부드러운 반응 속도를 확보했습니다.
      </p>

      <!-- 섹션 3: SEO URL 전략 -->
      <h2 class="section-title">🔍 3. 국가별 SEO를 위한 URL 전략</h2>
      
      <p>
        사용자는 "환율 계산기"보다 <strong>"베트남 돈 계산"</strong>처럼 구체적으로 검색합니다. 
        이를 잡기 위해 URL 라우팅을 자동화했습니다.
      </p>

<pre class="code-box"><code><span class="c-comment">// URL path를 감지하여 해당 국가로 자동 세팅</span>
<span class="c-keyword">const</span> COUNTRY_PRESETS = {
    <span class="c-string">'vietnam'</span>:   { <span class="c-property">from</span>: <span class="c-string">'VND'</span>, <span class="c-property">to</span>: <span class="c-string">'KRW'</span> },
    <span class="c-string">'thailand'</span>:  { <span class="c-property">from</span>: <span class="c-string">'THB'</span>, <span class="c-property">to</span>: <span class="c-string">'KRW'</span> },
    <span class="c-string">'japan'</span>:     { <span class="c-property">from</span>: <span class="c-string">'JPY'</span>, <span class="c-property">to</span>: <span class="c-string">'KRW'</span> },
    <span class="c-string">'usa'</span>:       { <span class="c-property">from</span>: <span class="c-string">'USD'</span>, <span class="c-property">to</span>: <span class="c-string">'KRW'</span> },
    <span class="c-comment">// ... 49개국 매핑</span>
};</code></pre>

      <!-- CTA 섹션 -->
      <div class="cta-section">
        <h3>🚀 직접 사용해보세요</h3>
        <p>10개국 환율 계산 / 오프라인 지원 / 가계부 연동</p>
        <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" 
           target="_blank" 
           rel="noopener noreferrer"
           class="cta-button">
          수당헬프 환율 계산기 실행하기 →
        </a>
      </div>

    </article>

    <!-- 푸터 네비게이션 -->
    <nav class="post-footer">
      <a href="{{ '/' | relative_url }}" class="back-link">
        ← 블로그 홈으로 돌아가기
      </a>
      <span style="color: #94a3b8; font-size: 14px;">
        © 2025 <a href="https://sudanghelp.co.kr/" target="_blank" rel="noopener noreferrer" style="color: #64748b;">수당헬프</a>
      </span>
    </nav>
  </main>

</body>
</html>
