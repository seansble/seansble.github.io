---
layout: null
---
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>수당헬프 개발 기술 블로그 | Money Flow & Code Vibe</title>
  <meta name="description" content="수당헬프 개발자 Seansble의 기술 블로그. 실업급여·부모급여·군인월급·환율·대출 등 돈의 흐름을 계산하는 핀테크 도구를 Vanilla JS·PWA·SEO 관점에서 구현한 과정을 기록합니다.">
  <link rel="canonical" href="{{ site.url }}{{ page.url }}">
  <style>
    /* 1. 기본 초기화 & 폰트 */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background-color: #f8f9fa;
      color: #333;
      font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", Roboto, sans-serif;
      line-height: 1.6;
    }

    .wrapper {
      max-width: 1200px;
      padding: 0 20px;
      margin: 0 auto;
    }

    /* 링크 밑줄 제거 */
    a { 
      text-decoration: none; 
      color: inherit; 
    }

    /* 2. 헤더 섹션 (인트로) */
    .header-section {
      text-align: center;
      padding: 80px 0 60px;
      background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
      color: white;
      border-radius: 0 0 24px 24px;
      margin-bottom: 60px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    }

    .header-inner {
      max-width: 1200px;
      padding: 0 20px;
      margin: 0 auto;
    }

    .main-title {
      font-size: 42px;
      font-weight: 800;
      margin-bottom: 16px;
      background: linear-gradient(to right, #60a5fa, #a78bfa);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      display: inline-block;
    }

    .sub-desc {
      font-size: 18px;
      color: #cbd5e1;
      line-height: 1.8;
      max-width: 700px;
      margin: 0 auto;
    }

    .sub-desc a {
      color: #60a5fa;
      font-weight: bold;
      border-bottom: 1px solid #60a5fa;
    }

    .sub-desc a:hover {
      color: #93c5fd;
    }

    /* 3. 메인 콘텐츠 영역 */
    main.wrapper {
      max-width: 1200px;
      padding: 0 20px;
      margin: 0 auto;
    }

    /* 4. 섹션 공통 스타일 */
    .section-container {
      margin-bottom: 80px;
    }

    .section-header {
      display: flex;
      align-items: center;
      margin-bottom: 32px;
      border-bottom: 2px solid #e2e8f0;
      padding-bottom: 12px;
    }

    .section-icon {
      font-size: 28px;
      margin-right: 12px;
    }

    .section-title {
      font-size: 28px;
      font-weight: 700;
      color: #1e293b;
      margin: 0;
    }

    /* 5. 서비스 카드 그리드 */
    .grid-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
      gap: 30px;
    }

    .card {
      background: white;
      border-radius: 16px;
      padding: 30px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.02);
      border: 1px solid #f1f5f9;
      transition: transform 0.2s, box-shadow 0.2s;
      height: 100%;
      display: flex;
      flex-direction: column;
    }

    .card:hover {
      transform: translateY(-5px);
      box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
      border-color: #e2e8f0;
    }

    .card-header {
      display: flex;
      align-items: center;
      margin-bottom: 20px;
    }

    .card-icon {
      width: 48px;
      height: 48px;
      background: #eff6ff;
      color: #2563eb;
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      margin-right: 16px;
    }

    .card-title {
      font-size: 22px;
      font-weight: 700;
      color: #1e293b;
      margin: 0;
    }

    .card-desc {
      color: #64748b;
      margin-bottom: 24px;
      font-size: 16px;
      line-height: 1.5;
    }

    /* 링크 리스트 */
    .link-list {
      list-style: none;
      padding: 0;
      margin: 0;
      margin-top: auto;
    }

    .link-item {
      margin-bottom: 12px;
    }

    .link-item a {
      color: #334155;
      font-weight: 600;
      font-size: 16px;
      transition: color 0.2s, background 0.2s;
      display: flex;
      align-items: center;
      width: 100%;
      padding: 8px 12px;
      background: #f8fafc;
      border-radius: 8px;
    }

    .link-item a:hover {
      color: #2563eb;
      background: #eff6ff;
    }

    .arrow-icon {
      margin-left: auto;
      font-size: 14px;
      color: #94a3b8;
    }

    /* 6. 기술 스택 */
    .tech-wrapper {
      background: white;
      padding: 40px;
      border-radius: 16px;
      border: 1px solid #e2e8f0;
    }

    .tech-row {
      display: flex;
      align-items: baseline;
      margin-bottom: 20px;
      border-bottom: 1px dashed #e2e8f0;
      padding-bottom: 20px;
    }

    .tech-row:last-child { 
      margin-bottom: 0; 
      border: none; 
      padding-bottom: 0; 
    }

    .tech-category {
      font-size: 18px;
      font-weight: 800;
      color: #2563eb;
      width: 100px;
      flex-shrink: 0;
    }

    .tech-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }

    .tag {
      background: #f1f5f9;
      color: #475569;
      padding: 6px 12px;
      border-radius: 6px;
      font-size: 15px;
      font-weight: 500;
      border: 1px solid #e2e8f0;
    }

    /* 7. 블로그 글 목록 */
    .post-list-modern {
      list-style: none;
      padding: 0;
    }

    .post-card {
      background: white;
      padding: 24px;
      border-radius: 12px;
      margin-bottom: 16px;
      border: 1px solid #e2e8f0;
      transition: all 0.2s;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .post-card:hover {
      border-color: #2563eb;
      transform: translateX(5px);
    }

    .post-title-link {
      font-size: 18px;
      font-weight: 700;
      color: #1e293b;
    }

    .post-card:hover .post-title-link {
      color: #2563eb;
    }

    .post-meta-date {
      color: #94a3b8;
      font-size: 14px;
      font-family: monospace;
      background: #f8fafc;
      padding: 4px 8px;
      border-radius: 4px;
    }

    /* 8. 푸터 */
    .footer {
      text-align: center;
      padding: 40px 20px;
      color: #94a3b8;
      font-size: 14px;
      border-top: 1px solid #e2e8f0;
      margin-top: 40px;
    }

    .footer a {
      color: #64748b;
      font-weight: 600;
    }

    .footer a:hover {
      color: #2563eb;
    }

    /* 모바일 대응 */
    @media (max-width: 768px) {
      .header-section { 
        padding: 40px 20px; 
        border-radius: 0; 
      }
      .main-title { 
        font-size: 28px; 
      }
      .sub-desc {
        font-size: 16px;
      }
      .grid-container {
        grid-template-columns: 1fr;
      }
      .card { 
        padding: 24px; 
      }
      .section-title {
        font-size: 22px;
      }
      .tech-wrapper {
        padding: 24px;
      }
      .tech-row { 
        flex-direction: column; 
        gap: 10px; 
      }
      .tech-category {
        width: auto;
      }
      .post-card { 
        flex-direction: column; 
        align-items: flex-start; 
        gap: 10px; 
      }
    }
  </style>
</head>
<body>

  <!-- 헤더 (그라데이션 배경) -->
  <header class="header-section">
    <div class="header-inner">
      <h1 class="main-title">Money Flow & Code Vibe</h1>
      <p class="sub-desc">
        안녕하세요, <strong>"돈의 흐름을 추적하는 바이브 코딩"</strong>으로<br>
        핀테크 도구 <a href="https://sudanghelp.co.kr/" target="_blank" rel="noopener noreferrer">[수당헬프]</a>를 개발하는 <strong>Seansble</strong>입니다.<br>
        기술적 경험(PWA, SEO)과 금융 로직 구현 과정을 기록합니다.
      </p>
    </div>
  </header>

  <!-- 메인 콘텐츠 -->
  <main class="wrapper">

    <!-- 서비스 아키텍처 (카드 그리드) -->
    <section class="section-container">
      <div class="section-header">
        <span class="section-icon">🗺️</span>
        <h2 class="section-title">Service Architecture</h2>
      </div>
      
      <div class="grid-container">
        <!-- 카드 1: 소득 -->
        <article class="card">
          <div class="card-header">
            <div class="card-icon">💵</div>
            <h3 class="card-title">소득 & 보장</h3>
          </div>
          <p class="card-desc">국가에서 보장하는 권리와 혜택을<br>놓치지 않도록 돕습니다.</p>
          <ul class="link-list">
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/parents/" target="_blank" rel="noopener noreferrer">
                👶 출산/육아 (부모급여) <span class="arrow-icon">➔</span>
              </a>
            </li>
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/military/salary/" target="_blank" rel="noopener noreferrer">
                🪖 군인 (월급/적금) <span class="arrow-icon">➔</span>
              </a>
            </li>
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/unemployment/" target="_blank" rel="noopener noreferrer">
                💼 실업급여 모의계산 <span class="arrow-icon">➔</span>
              </a>
            </li>
          </ul>
        </article>

        <!-- 카드 2: 지출 -->
        <article class="card">
          <div class="card-header">
            <div class="card-icon">💸</div>
            <h3 class="card-title">비용 & 지출</h3>
          </div>
          <p class="card-desc">새는 돈을 막고,<br>합리적인 소비를 지원합니다.</p>
          <ul class="link-list">
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank" rel="noopener noreferrer">
                ✈️ 여행/환전 (PWA) <span class="arrow-icon">➔</span>
              </a>
            </li>
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/creditcalc/step-loan/" target="_blank" rel="noopener noreferrer">
                🏦 대출 (체증식/중도상환) <span class="arrow-icon">➔</span>
              </a>
            </li>
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/additionaltax/supply-calc/" target="_blank" rel="noopener noreferrer">
                🧾 세금 (부가세/공급가액) <span class="arrow-icon">➔</span>
              </a>
            </li>
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/electricity/" target="_blank" rel="noopener noreferrer">
                ⚡ 공과금 (전기요금) <span class="arrow-icon">➔</span>
              </a>
            </li>
          </ul>
        </article>

        <!-- 카드 3: 자산 -->
        <article class="card">
          <div class="card-header">
            <div class="card-icon">💰</div>
            <h3 class="card-title">자산 형성</h3>
          </div>
          <p class="card-desc">미래를 위한 자산 증식<br>시뮬레이션을 제공합니다.</p>
          <ul class="link-list">
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/compoundcalc/" target="_blank" rel="noopener noreferrer">
                📈 투자 설계 (복리/적금) <span class="arrow-icon">➔</span>
              </a>
            </li>
            <li class="link-item">
              <a href="https://sudanghelp.co.kr/coinmore/" target="_blank" rel="noopener noreferrer">
                🪙 크립토 (물타기) <span class="arrow-icon">➔</span>
              </a>
            </li>
          </ul>
        </article>
      </div>
    </section>

    <!-- 기술 스택 -->
    <section class="section-container">
      <div class="section-header">
        <span class="section-icon">🛠️</span>
        <h2 class="section-title">Tech Stack</h2>
      </div>
      <div class="tech-wrapper">
        <div class="tech-row">
          <div class="tech-category">Core</div>
          <div class="tech-tags">
            <span class="tag">Vanilla JS</span>
            <span class="tag">Performance Optimized</span>
            <span class="tag">Cloudflare Workers</span>
          </div>
        </div>
        <div class="tech-row">
          <div class="tech-category">PWA</div>
          <div class="tech-tags">
            <span class="tag">Service Worker</span>
            <span class="tag">Offline Support</span>
            <span class="tag">Manifest</span>
          </div>
        </div>
        <div class="tech-row">
          <div class="tech-category">SEO</div>
          <div class="tech-tags">
            <span class="tag">JSON-LD</span>
            <span class="tag">Meta Optimization</span>
            <span class="tag">Sitemap Clustering</span>
          </div>
        </div>
      </div>
    </section>

    <!-- 최신 글 목록 -->
    <section class="section-container">
      <div class="section-header">
        <span class="section-icon">📝</span>
        <h2 class="section-title">Latest Dev Logs</h2>
      </div>
      <ul class="post-list-modern">
        {% for post in site.posts %}
          <li class="post-card">
            <a href="{{ post.url | relative_url }}" class="post-title-link">{{ post.title }}</a>
            <span class="post-meta-date">{{ post.date | date: "%Y-%m-%d" }}</span>
          </li>
        {% endfor %}
      </ul>
    </section>

  </main>

  <!-- 푸터 -->
  <footer class="footer">
    <p>© 2025 <a href="https://sudanghelp.co.kr/" target="_blank" rel="noopener noreferrer">수당헬프</a> · Built with Jekyll & GitHub Pages</p>
  </footer>

</body>
</html>
