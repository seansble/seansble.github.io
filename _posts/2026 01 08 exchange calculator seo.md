---
layout: post
title: "🔍 49개국 URL 라우팅 & SEO 최적화 - 환율 계산기 개발기 (2/3)"
date: 2026-01-08
author: Seansble
categories: [Tech]
tags:
  - DevLog
  - SEO
  - JavaScript
  - JSON-LD
  - Structured-Data
description: "베트남 환율, 태국 환율 등 국가별 롱테일 키워드를 잡기 위한 URL 라우팅과 구조화 데이터 최적화 전략을 공유합니다."
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

/* 인트로 박스 */
.intro-box {
  background: linear-gradient(135deg, #faf5ff 0%, #f3e8ff 100%);
  border: 1px solid #e9d5ff;
  border-radius: 16px;
  padding: 28px 32px;
  margin-bottom: 48px;
}

.intro-box h2 {
  font-size: 20px !important;
  font-weight: 700 !important;
  color: #581c87 !important;
  margin: 0 0 12px 0 !important;
  border: none !important;
  padding: 0 !important;
}

.intro-box p {
  color: #7e22ce !important;
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

/* 국가 테이블 */
.country-table {
  width: 100%;
  border-collapse: collapse;
  margin: 24px 0;
  font-size: 14px;
}

.country-table th {
  background: #f1f5f9;
  padding: 12px 16px;
  text-align: left;
  font-weight: 700;
  color: #334155;
  border-bottom: 2px solid #e2e8f0;
}

.country-table td {
  padding: 12px 16px;
  border-bottom: 1px solid #e2e8f0;
  color: #475569;
}

.country-table tr:hover td {
  background: #f8fafc;
}

.country-table code {
  background: #e0f2fe !important;
  color: #0369a1 !important;
  padding: 2px 6px !important;
  border-radius: 4px !important;
  font-size: 12px !important;
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

/* 포스트 네비게이션 */
.post-nav {
  margin-top: 60px;
  padding-top: 40px;
  border-top: 1px solid #e5e7eb;
  display: flex;
  gap: 16px;
}

.post-nav-link {
  flex: 1;
  display: flex;
  align-items: center;
  gap: 12px;
  background: #f8fafc;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 16px 20px;
  text-decoration: none !important;
  transition: all 0.2s;
}

.post-nav-link:hover {
  border-color: #3b82f6;
  box-shadow: 0 4px 12px rgba(59, 130, 246, 0.15);
}

.post-nav-link.prev { flex-direction: row; }
.post-nav-link.next { flex-direction: row-reverse; text-align: right; }

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
  .post-nav { flex-direction: column; }
  .country-table { font-size: 12px; }
  .country-table th, .country-table td { padding: 8px 10px; }
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
    <span class="series-nav-item current">
      <span class="num">2</span> 49개국 URL 라우팅 & SEO 최적화
    </span>
    <a href="{{ '/2026/01/09/exchange-calculator-security' | relative_url }}" class="series-nav-item">
      <span class="num">3</span> 보안 강화 & 성능 튜닝
    </a>
  </div>
</nav>

<!-- 인트로 -->
<div class="intro-box">
  <h2>🌏 "베트남 환율"로 검색하면 내 계산기가 나올까?</h2>
  <p>
    사용자들은 "환율 계산기"보다 <strong>"베트남 돈 계산"</strong>, <strong>"태국 바트 원화"</strong>처럼 구체적으로 검색합니다.<br>
    이 롱테일 키워드를 잡기 위해 <strong>49개국 × 개별 URL</strong> 전략을 적용했습니다.
  </p>
</div>

<!-- 섹션 1 -->
<h2 class="section-title">🗺️ 1. 국가별 URL 프리셋 시스템</h2>

<p>
  URL 경로를 감지해서 해당 국가 통화로 자동 세팅되는 구조입니다. 하나의 <code>calculator.js</code>로 49개국을 커버합니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// calculator.js - 국가별 URL 프리셋 (49개국)</span>
<span class="hl-keyword">const</span> COUNTRY_PRESETS = {
    <span class="hl-comment">// 동남아시아</span>
    <span class="hl-string">'vietnam'</span>:     { <span class="hl-property">from</span>: <span class="hl-string">'VND'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-string">'thailand'</span>:    { <span class="hl-property">from</span>: <span class="hl-string">'THB'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-string">'philippines'</span>: { <span class="hl-property">from</span>: <span class="hl-string">'PHP'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-string">'indonesia'</span>:   { <span class="hl-property">from</span>: <span class="hl-string">'IDR'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    
    <span class="hl-comment">// 동아시아</span>
    <span class="hl-string">'japan'</span>:       { <span class="hl-property">from</span>: <span class="hl-string">'JPY'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-string">'taiwan'</span>:      { <span class="hl-property">from</span>: <span class="hl-string">'TWD'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    <span class="hl-string">'hongkong'</span>:    { <span class="hl-property">from</span>: <span class="hl-string">'HKD'</span>, <span class="hl-property">to</span>: <span class="hl-string">'KRW'</span> },
    
    <span class="hl-comment">// ... 총 49개국 매핑</span>
};

<span class="hl-comment">// URL 경로에서 국가 감지</span>
<span class="hl-keyword">const</span> path = window.location.pathname;
<span class="hl-keyword">const</span> country = path.<span class="hl-method">split</span>(<span class="hl-string">'/'</span>).<span class="hl-method">filter</span>(Boolean).<span class="hl-method">pop</span>();

<span class="hl-keyword">if</span> (COUNTRY_PRESETS[country]) {
    <span class="hl-keyword">const</span> preset = COUNTRY_PRESETS[country];
    <span class="hl-function">setFromCurrency</span>(preset.from);
    <span class="hl-function">setToCurrency</span>(preset.to);
}</code></pre>

<p>이 구조의 장점:</p>

<table class="country-table">
  <thead>
    <tr>
      <th>URL 경로</th>
      <th>타겟 키워드</th>
      <th>자동 설정</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>/vietnam/</code></td>
      <td>베트남 환율, 베트남 돈 계산</td>
      <td>VND → KRW</td>
    </tr>
    <tr>
      <td><code>/thailand/</code></td>
      <td>태국 바트 환율, 바트 원화</td>
      <td>THB → KRW</td>
    </tr>
    <tr>
      <td><code>/japan/</code></td>
      <td>엔화 환율, 일본 돈 계산</td>
      <td>JPY → KRW</td>
    </tr>
  </tbody>
</table>

<!-- 섹션 2 -->
<h2 class="section-title">📊 2. JSON-LD 구조화 데이터</h2>

<p>
  Google이 계산기를 <strong>SoftwareApplication</strong>으로 인식하도록 구조화 데이터를 추가했습니다. FAQ 스키마도 함께 넣어 SERP 노출 면적을 늘렸습니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// index.html - JSON-LD 구조화 데이터</span>
&lt;script type=<span class="hl-string">"application/ld+json"</span>&gt;
{
    <span class="hl-string">"@context"</span>: <span class="hl-string">"https://schema.org"</span>,
    <span class="hl-string">"@graph"</span>: [
        {
            <span class="hl-string">"@type"</span>: <span class="hl-string">"SoftwareApplication"</span>,
            <span class="hl-string">"name"</span>: <span class="hl-string">"수당헬프 환율 계산기"</span>,
            <span class="hl-string">"applicationCategory"</span>: <span class="hl-string">"FinanceApplication"</span>,
            <span class="hl-string">"operatingSystem"</span>: <span class="hl-string">"Web Browser"</span>,
            <span class="hl-string">"offers"</span>: { <span class="hl-string">"price"</span>: <span class="hl-string">"0"</span> },
            <span class="hl-string">"aggregateRating"</span>: {
                <span class="hl-string">"ratingValue"</span>: <span class="hl-string">"4.6"</span>,
                <span class="hl-string">"ratingCount"</span>: <span class="hl-string">"423"</span>
            }
        },
        {
            <span class="hl-string">"@type"</span>: <span class="hl-string">"FAQPage"</span>,
            <span class="hl-string">"mainEntity"</span>: [
                {
                    <span class="hl-string">"@type"</span>: <span class="hl-string">"Question"</span>,
                    <span class="hl-string">"name"</span>: <span class="hl-string">"환율은 얼마나 자주 업데이트되나요?"</span>,
                    <span class="hl-string">"acceptedAnswer"</span>: {
                        <span class="hl-string">"text"</span>: <span class="hl-string">"1시간마다 자동 갱신됩니다."</span>
                    }
                }
            ]
        }
    ]
}
&lt;/script&gt;</code></pre>

<div class="tip-box">
  <p><strong>💡 SEO 팁:</strong> <code>aggregateRating</code>을 넣으면 검색 결과에 ⭐ 별점이 표시됩니다. 실제 리뷰 시스템을 구축한 후 추가하세요.</p>
</div>

<!-- 섹션 3 -->
<h2 class="section-title">🔗 3. BreadcrumbList로 사이트 구조 명시</h2>

<p>
  계층 구조를 Google에 명확히 전달해서 사이트링크 노출 확률을 높입니다.
</p>

<pre class="code-block"><code>{
    <span class="hl-string">"@type"</span>: <span class="hl-string">"BreadcrumbList"</span>,
    <span class="hl-string">"itemListElement"</span>: [
        { <span class="hl-string">"position"</span>: 1, <span class="hl-string">"name"</span>: <span class="hl-string">"홈"</span>, <span class="hl-string">"item"</span>: <span class="hl-string">"https://sudanghelp.co.kr/"</span> },
        { <span class="hl-string">"position"</span>: 2, <span class="hl-string">"name"</span>: <span class="hl-string">"비용·지출"</span>, <span class="hl-string">"item"</span>: <span class="hl-string">"https://sudanghelp.co.kr/expense/"</span> },
        { <span class="hl-string">"position"</span>: 3, <span class="hl-string">"name"</span>: <span class="hl-string">"여행 비용 플래너"</span>, <span class="hl-string">"item"</span>: <span class="hl-string">"https://sudanghelp.co.kr/travel/"</span> },
        { <span class="hl-string">"position"</span>: 4, <span class="hl-string">"name"</span>: <span class="hl-string">"환율 계산기"</span>, <span class="hl-string">"item"</span>: <span class="hl-string">"https://sudanghelp.co.kr/travel/exchange-calculator/"</span> }
    ]
}</code></pre>

<!-- CTA -->
<div class="cta-section">
  <h3>🌏 49개국 환율 계산기</h3>
  <p>베트남 · 태국 · 일본 · 필리핀 등 국가별 페이지 제공</p>
  <a href="https://sudanghelp.co.kr/travel/exchange-calculator/vietnam/" 
     target="_blank" 
     rel="noopener noreferrer"
     class="cta-button">
    베트남 환율 계산기 →
  </a>
</div>

<!-- 포스트 네비게이션 -->
<nav class="post-nav">
  <a href="{{ '/2026/01/07/exchange-calculator-pwa' | relative_url }}" class="post-nav-link prev">
    <span class="post-nav-arrow">←</span>
    <div>
      <div class="post-nav-label">이전 글 (1/3)</div>
      <div class="post-nav-title">오프라인 퍼스트 & PWA</div>
    </div>
  </a>
  <a href="{{ '/2026/01/09/exchange-calculator-security' | relative_url }}" class="post-nav-link next">
    <div>
      <div class="post-nav-label">다음 글 (3/3)</div>
      <div class="post-nav-title">보안 강화 & 성능 튜닝</div>
    </div>
    <span class="post-nav-arrow">→</span>
  </a>
</nav>

</div>
