---
layout: post
title: "✈️ 여행지 로밍이 끊겨도 OK! PWA 환율 계산기 개발기 (1/3)"
date: 2026-01-07
author: Seansble
categories: [Tech]
tags:
  - DevLog
  - PWA
  - Performance
  - JavaScript
  - Service-Worker
description: "베트남, 필리핀 등 여행지 통신 환경을 고려한 오프라인 퍼스트(Offline-First) 환율 계산기 개발 경험을 공유합니다."
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

/* 다음 글 네비게이션 */
.next-post-nav {
  margin-top: 60px;
  padding-top: 40px;
  border-top: 1px solid #e5e7eb;
}

.next-post-link {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #f8fafc;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 20px 24px;
  text-decoration: none !important;
  transition: all 0.2s;
}

.next-post-link:hover {
  border-color: #3b82f6;
  box-shadow: 0 4px 12px rgba(59, 130, 246, 0.15);
}

.next-post-label {
  font-size: 13px;
  color: #64748b;
  margin-bottom: 4px;
}

.next-post-title {
  font-size: 16px;
  font-weight: 700;
  color: #1e293b !important;
}

.next-post-arrow {
  font-size: 24px;
  color: #3b82f6;
}

/* 모바일 대응 */
@media (max-width: 768px) {
  .post-content-custom p { font-size: 16px !important; }
  .section-title { font-size: 20px !important; margin-top: 40px !important; }
  .code-block { padding: 18px 16px !important; font-size: 13px !important; border-radius: 8px !important; }
  .intro-box { padding: 22px 20px; }
  .cta-section { padding: 32px 24px; }
  .series-nav { padding: 16px 18px; }
}
</style>

<div class="post-content-custom" markdown="0">

<!-- 시리즈 네비게이션 -->
<nav class="series-nav">
  <div class="series-nav-title">📚 환율 계산기 개발기 시리즈</div>
  <div class="series-nav-list">
    <span class="series-nav-item current">
      <span class="num">1</span> 오프라인 퍼스트 & PWA 전략
    </span>
    <a href="{{ '/2026/01/08/exchange-calculator-seo' | relative_url }}" class="series-nav-item">
      <span class="num">2</span> 49개국 URL 라우팅 & SEO 최적화
    </a>
    <a href="{{ '/2026/01/09/exchange-calculator-security' | relative_url }}" class="series-nav-item">
      <span class="num">3</span> 보안 강화 & 성능 튜닝
    </a>
  </div>
</nav>

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

<pre class="code-block"><code><span class="hl-comment">// calculator.js - Fail-over 핵심 로직</span>
<span class="hl-keyword">const</span> EXCHANGE_API_URL = <span class="hl-string">'https://sudanghelp-rates.workers.dev'</span>;

<span class="hl-keyword">async function</span> <span class="hl-function">loadRates</span>() {
    <span class="hl-keyword">const</span> rateInfo = document.<span class="hl-method">getElementById</span>(<span class="hl-string">'rate-update-info'</span>);
    
    <span class="hl-keyword">try</span> {
        <span class="hl-comment">// 1. Cloudflare Edge에서 최신 환율 요청</span>
        <span class="hl-keyword">const</span> response = <span class="hl-keyword">await</span> <span class="hl-function">fetch</span>(EXCHANGE_API_URL);
        <span class="hl-keyword">if</span> (!response.ok) <span class="hl-keyword">throw new</span> <span class="hl-function">Error</span>(<span class="hl-string">'Network Error'</span>);
        
        <span class="hl-comment">// 2. 성공 시 LocalStorage에 백업 저장</span>
        <span class="hl-keyword">const</span> data = <span class="hl-keyword">await</span> response.<span class="hl-method">json</span>();
        <span class="hl-function">saveToStorage</span>(<span class="hl-string">'cachedRates'</span>, data);
        <span class="hl-function">updateRates</span>(data);
        
    } <span class="hl-keyword">catch</span> (e) {
        <span class="hl-comment">// 3. 🚨 실패 시: 에러 대신 '오프라인 모드' 전환</span>
        console.<span class="hl-method">warn</span>(<span class="hl-string">'Offline Mode Activated'</span>);
        
        <span class="hl-comment">// 캐싱된 환율로 계산기 기능 유지</span>
        <span class="hl-keyword">const</span> cached = <span class="hl-function">loadFromStorage</span>(<span class="hl-string">'cachedRates'</span>);
        <span class="hl-keyword">if</span> (cached) <span class="hl-function">updateRates</span>(cached);
        
        rateInfo.<span class="hl-property">textContent</span> = <span class="hl-string">'오프라인 모드 (최근 데이터)'</span>;
        rateInfo.<span class="hl-property">style</span>.<span class="hl-property">color</span> = <span class="hl-string">'#ef4444'</span>; 
    }
}</code></pre>

<div class="tip-box">
  <p><strong>💡 핵심 포인트:</strong> <code>catch</code> 블록에서 에러를 중단시키지 않고 LocalStorage 캐시로 폴백합니다. 사용자는 "오프라인 모드"임을 인지하면서도 계산기를 정상 사용할 수 있습니다.</p>
</div>

<!-- 섹션 2 -->
<h2 class="section-title">⚡ 2. Service Worker 캐싱 전략</h2>

<p>
  PWA의 핵심은 <strong>Service Worker</strong>입니다. 정적 자산은 캐시 우선(Cache-First), HTML은 네트워크 우선(Network-First) 전략을 사용했습니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// sw.js - 하이브리드 캐싱 전략</span>
<span class="hl-keyword">const</span> CACHE_NAME = <span class="hl-string">'travel-helper-v4'</span>;

<span class="hl-comment">// 정적 자산: Cache-First (빠른 로딩)</span>
<span class="hl-keyword">async function</span> <span class="hl-function">cacheFirst</span>(request) {
    <span class="hl-keyword">const</span> cached = <span class="hl-keyword">await</span> caches.<span class="hl-method">match</span>(request);
    <span class="hl-keyword">if</span> (cached) {
        <span class="hl-function">updateCache</span>(request); <span class="hl-comment">// 백그라운드 갱신</span>
        <span class="hl-keyword">return</span> cached;
    }
    <span class="hl-keyword">return</span> <span class="hl-function">fetch</span>(request);
}

<span class="hl-comment">// HTML: Network-First (최신 콘텐츠 보장)</span>
<span class="hl-keyword">async function</span> <span class="hl-function">networkFirst</span>(request) {
    <span class="hl-keyword">try</span> {
        <span class="hl-keyword">const</span> response = <span class="hl-keyword">await</span> <span class="hl-function">fetch</span>(request);
        <span class="hl-keyword">const</span> cache = <span class="hl-keyword">await</span> caches.<span class="hl-method">open</span>(CACHE_NAME);
        cache.<span class="hl-method">put</span>(request, response.<span class="hl-method">clone</span>());
        <span class="hl-keyword">return</span> response;
    } <span class="hl-keyword">catch</span> {
        <span class="hl-comment">// 오프라인 → 캐시 또는 오프라인 페이지</span>
        <span class="hl-keyword">return</span> caches.<span class="hl-method">match</span>(request) || 
               caches.<span class="hl-method">match</span>(<span class="hl-string">'/travel/offline.html'</span>);
    }
}</code></pre>

<!-- 섹션 3 -->
<h2 class="section-title">📱 3. PWA 설치 UX (홈 화면 추가)</h2>

<p>
  <code>beforeinstallprompt</code> 이벤트를 캐치해서 커스텀 설치 버튼을 만들었습니다. iOS는 네이티브 프롬프트가 없어서 Toast로 안내합니다.
</p>

<pre class="code-block"><code><span class="hl-comment">// PWA 설치 버튼 로직</span>
<span class="hl-keyword">let</span> deferredPrompt = <span class="hl-keyword">null</span>;
<span class="hl-keyword">const</span> isIOS = <span class="hl-string">/iPad|iPhone|iPod/</span>.<span class="hl-method">test</span>(navigator.userAgent);

window.<span class="hl-method">addEventListener</span>(<span class="hl-string">'beforeinstallprompt'</span>, (e) => {
    e.<span class="hl-method">preventDefault</span>();
    deferredPrompt = e; <span class="hl-comment">// 나중에 사용</span>
});

pwaInstallBtn.<span class="hl-method">addEventListener</span>(<span class="hl-string">'click'</span>, <span class="hl-keyword">async</span> () => {
    <span class="hl-keyword">if</span> (deferredPrompt) {
        <span class="hl-comment">// Android/Chrome: 네이티브 프롬프트</span>
        deferredPrompt.<span class="hl-method">prompt</span>();
        <span class="hl-keyword">const</span> { outcome } = <span class="hl-keyword">await</span> deferredPrompt.userChoice;
        deferredPrompt = <span class="hl-keyword">null</span>;
    } <span class="hl-keyword">else if</span> (isIOS) {
        <span class="hl-comment">// iOS: 수동 안내</span>
        <span class="hl-function">showToast</span>(<span class="hl-string">'공유 버튼(□↑) → 홈 화면에 추가'</span>);
    }
});</code></pre>

<div class="tip-box">
  <p><strong>💡 iOS 대응:</strong> iOS Safari는 PWA 설치 프롬프트를 지원하지 않습니다. 사용자에게 "공유 → 홈 화면에 추가" 경로를 Toast로 안내해야 합니다.</p>
</div>

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

<!-- 다음 글 -->
<nav class="next-post-nav">
  <a href="{{ '/2026/01/08/exchange-calculator-seo' | relative_url }}" class="next-post-link">
    <div>
      <div class="next-post-label">다음 글 (2/3)</div>
      <div class="next-post-title">🔍 49개국 URL 라우팅 & SEO 최적화</div>
    </div>
    <span class="next-post-arrow">→</span>
  </a>
</nav>

</div>
