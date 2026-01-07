---
layout: default
title: 수당헬프 개발 기술 블로그
---

<!-- 🎨 스타일 정의 (골드 샴페인 테마 이식) -->
<style>
  /* 1. 전체 레이아웃 & 배경 */
  body {
    background-color: #0a0c10 !important; /* 리얼 블랙 */
    background-image: radial-gradient(circle at 50% -10%, #1f232d 0%, #0a0c10 80%) !important;
    color: #e2e8f0 !important; /* 밝은 회색 텍스트 */
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif !important;
  }

  .wrapper {
    max-width: 1200px !important;
    padding: 0 40px !important;
  }

  /* 2. 타이포그래피 */
  h1, h2, h3 {
    color: #ffffff !important;
    letter-spacing: -0.5px;
  }

  h1 { font-size: 36px; font-weight: 800; margin-top: 60px; margin-bottom: 24px; }
  
  h2.section-title {
    font-size: 28px;
    font-weight: 700;
    color: #e2c068 !important; /* 골드 포인트 */
    border-bottom: 2px solid rgba(226, 192, 104, 0.2);
    padding-bottom: 16px;
    margin-top: 80px;
    margin-bottom: 40px;
    text-shadow: 0 0 20px rgba(226, 192, 104, 0.1);
  }

  h3 { font-size: 22px; margin-top: 40px; margin-bottom: 20px; color: #f1f5f9 !important; }
  p, li { font-size: 17px; line-height: 1.7; color: #94a3b8; }

  /* 3. 인트로 박스 (유리 질감) */
  .intro-container {
    background: rgba(18, 21, 28, 0.6);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 24px;
    padding: 60px 40px;
    text-align: center;
    margin-bottom: 80px;
    backdrop-filter: blur(10px);
    box-shadow: 0 20px 40px -10px rgba(0, 0, 0, 0.3);
  }
  
  .intro-title {
    background: linear-gradient(135deg, #e2c068 0%, #d4af37 100%); /* 골드 그라데이션 */
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    display: inline-block;
    margin-bottom: 20px;
  }

  /* 4. 서비스 카드 (다크모드 카드) */
  .service-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 24px;
    list-style: none;
    padding: 0;
  }
  
  .service-item {
    background: #12151c; /* 카드 배경 */
    border: 1px solid rgba(255, 255, 255, 0.05);
    border-radius: 16px;
    padding: 28px;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
  }

  .service-item:hover {
    transform: translateY(-5px);
    border-color: rgba(226, 192, 104, 0.3); /* 호버 시 골드 테두리 */
    box-shadow: 0 15px 30px -10px rgba(0, 0, 0, 0.5);
    background: #151922;
  }

  .service-item strong {
    display: block;
    color: #e2c068; /* 골드 */
    font-size: 19px;
    margin-bottom: 12px;
  }

  /* 링크 스타일 (골드) */
  a {
    color: #fff;
    text-decoration: none;
    border-bottom: 1px solid rgba(226, 192, 104, 0.3);
    transition: all 0.2s;
  }
  a:hover {
    color: #e2c068;
    border-bottom-color: #e2c068;
  }

  /* 5. 기술 스택 박스 */
  .tech-box {
    background: #0f1115;
    border: 1px solid rgba(255, 255, 255, 0.05);
    border-radius: 16px;
    padding: 32px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 30px;
  }
  
  .tech-label {
    color: #e2c068;
    font-weight: 700;
    font-size: 18px;
    display: block;
    margin-bottom: 10px;
    border-left: 3px solid #e2c068;
    padding-left: 12px;
  }
  
  .tech-keyword { color: #fff; font-weight: 600; }
  .tech-sub { color: #64748b; font-size: 0.9em; }

  /* 6. 포스트 리스트 */
  .post-list { padding: 0; list-style: none; }
  
  .post-item {
    padding: 24px 0;
    border-bottom: 1px solid rgba(255, 255, 255, 0.05);
    display: flex;
    align-items: center;
    transition: padding-left 0.2s;
  }
  
  .post-item:hover {
    padding-left: 15px; /* 호버 시 슬라이딩 효과 */
    border-bottom-color: rgba(226, 192, 104, 0.2);
  }
  
  .post-date {
    font-family: 'Consolas', monospace;
    color: #64748b;
    font-size: 14px;
    margin-right: 24px;
    background: rgba(255, 255, 255, 0.05);
    padding: 4px 8px;
    border-radius: 4px;
  }
  
  .post-link {
    font-size: 20px;
    color: #e2e8f0;
    font-weight: 600;
    border: none;
  }
  .post-link:hover { color: #e2c068; }

  /* 모바일 대응 */
  @media (max-width: 768px) {
    .wrapper { padding: 0 20px !important; }
    .intro-container { padding: 40px 20px; }
    h1 { font-size: 28px; }
    .post-item { flex-direction: column; align-items: flex-start; gap: 8px; }
  }
</style>

<!-- 본문 시작 -->

<div class="intro-container">
  <h1 class="intro-title">💸 Money Flow & Code Vibe 👋</h1>
  <p class="intro-desc">
    안녕하세요, <strong>"돈의 흐름을 추적하는 바이브 코딩"</strong>으로<br>
    핀테크 도구 <a href="https://sudanghelp.co.kr/" target="_blank">[수당헬프]</a>를 개발하는 <strong>Seansble</strong>입니다.<br>
    <br>
    이곳은 서비스를 개발하며 겪은 기술적인 경험(PWA, SEO),<br>
    그리고 복잡한 금융 로직을 웹으로 구현한 과정을 기록합니다.
  </p>
</div>

<h2 class="section-title">🗺️ Service Architecture</h2>
<p style="text-align: center; color: #94a3b8; margin-bottom: 50px; font-size: 18px;">
  수당헬프는 단순한 계산기를 넘어, <strong>소득·지출·자산</strong>을 아우르는 3가지 핵심 축으로 구성되어 있습니다.
</p>

<h3>1. 💵 소득 & 보장 (Income & Security)</h3>
<p style="margin-bottom: 20px;">국가에서 보장하는 권리와 혜택을 놓치지 않도록 돕습니다.</p>
<ul class="service-list">
  <li class="service-item">
    <strong>출산/육아</strong>
    <a href="https://sudanghelp.co.kr/parents/" target="_blank">부모급여 통합 계산기</a>, 아동수당 가이드
  </li>
  <li class="service-item">
    <strong>군인</strong>
    <a href="https://sudanghelp.co.kr/military/salary/" target="_blank">2026 군인 월급/적금 계산기</a>, 공군 점수 계산
  </li>
  <li class="service-item">
    <strong>실업급여</strong>
    <a href="https://sudanghelp.co.kr/unemployment/" target="_blank">실업급여 모의계산</a>, 가이드
  </li>
</ul>

<h3>2. 💸 비용 & 지출 (Expense & Spending)</h3>
<p style="margin-bottom: 20px;">새는 돈을 막고, 합리적인 소비를 지원하는 도구입니다.</p>
<ul class="service-list">
  <li class="service-item">
    <strong>여행/환전</strong>
    <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank">PWA 환율 계산기 (오프라인 지원)</a>, 여행 가계부
  </li>
  <li class="service-item">
    <strong>대출</strong>
    <a href="https://sudanghelp.co.kr/creditcalc/step-loan/" target="_blank">체증식 대출 계산기</a>, 중도상환수수료 계산
  </li>
  <li class="service-item">
    <strong>세금 (VAT)</strong>
    <a href="https://sudanghelp.co.kr/additionaltax/supply-calc/" target="_blank">부가세/공급가액 계산</a>, 간이과세 체크
  </li>
  <li class="service-item">
    <strong>공과금</strong>
    <a href="https://sudanghelp.co.kr/electricity/" target="_blank">전기요금 누진세 계산기</a>
  </li>
</ul>

<h3>3. 💰 자산 형성 (Asset Building)</h3>
<p style="margin-bottom: 20px;">미래를 위한 자산 증식 시뮬레이션을 제공합니다.</p>
<ul class="service-list">
  <li class="service-item">
    <strong>투자 설계</strong>
    <a href="https://sudanghelp.co.kr/compoundcalc/" target="_blank">복리(예금/적금) 계산기</a>, 1억 만들기 플랜
  </li>
  <li class="service-item">
    <strong>크립토</strong>
    <a href="https://sudanghelp.co.kr/coinmore/" target="_blank">코인 물타기 계산기</a>
  </li>
</ul>

<h2 class="section-title">🛠️ Tech Stack</h2>
<div class="tech-box">
  <div class="tech-item">
    <span class="tech-label">Core</span>
    <div class="tech-content">
      <span class="tech-keyword">Vanilla JS</span> <span class="tech-sub">(Performance)</span><br>
      <span class="tech-keyword">Cloudflare Workers</span> <span class="tech-sub">(Edge Computing)</span>
    </div>
  </div>
  <div class="tech-item">
    <span class="tech-label">PWA</span>
    <div class="tech-content">
      <span class="tech-keyword">Service Worker</span> <span class="tech-sub">(Offline Support)</span><br>
      <span class="tech-keyword">Manifest</span> <span class="tech-sub">(Installable)</span>
    </div>
  </div>
  <div class="tech-item">
    <span class="tech-label">SEO</span>
    <div class="tech-content">
      <span class="tech-keyword">JSON-LD Structure</span><br>
      <span class="tech-keyword">Meta Tag Optimization</span><br>
      <span class="tech-keyword">Sitemap Clustering</span>
    </div>
  </div>
</div>

<h2 class="section-title">📝 Latest Dev Logs (최신 개발기)</h2>

<ul class="post-list">
  {% for post in site.posts %}
    <li class="post-item">
      <span class="post-date">[{{ post.date | date: "%Y-%m-%d" }}]</span>
      <a href="{{ post.url }}" class="post-link">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
```
