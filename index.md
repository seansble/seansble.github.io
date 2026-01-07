layout: default title: 수당헬프 개발 기술 블로그

<!-- 🎨 스타일 정의 (긴급 복구 & 강제 적용) -->

<style>
/* 1. 전체 초기화 (테마 무시) /
body, .wrapper, .site-content, article {
background-color: #0a0c10 !important; / 리얼 블랙 /
background-image: radial-gradient(circle at 50% -10%, #1f232d 0%, #0a0c10 80%) !important;
color: #e2e8f0 !important; / 기본 글자색: 밝은 회색 */
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif !important;
line-height: 1.6 !important;
}

.wrapper {
max-width: 1200px !important;
padding: 0 20px !important;
margin: 0 auto !important;
}

/* 2. 타이포그래피 (색상 강제) /
h1, h2, h3, h4, strong, b {
color: #ffffff !important; / 제목/강조는 무조건 흰색 */
margin: 0 !important;
}

h1 { font-size: 32px !important; margin-bottom: 20px !important; }

h2.section-title {
font-size: 26px !important;
color: #e2c068 !important; /* 골드 포인트 */
border-bottom: 2px solid rgba(226, 192, 104, 0.3) !important;
padding-bottom: 15px !important;
margin-top: 60px !important;
margin-bottom: 30px !important;
display: block !important;
}

h3 {
font-size: 20px !important;
margin-top: 40px !important;
margin-bottom: 15px !important;
color: #f8fafc !important; /* 흰색에 가까운 회색 */
display: block !important;
}

p, li, span {
color: #cbd5e1 !important; /* 본문: 연한 회색 */
font-size: 16px !important;
}

/* 3. 인트로 박스 */
.intro-container {
background: rgba(255, 255, 255, 0.05) !important;
border: 1px solid rgba(255, 255, 255, 0.1) !important;
border-radius: 16px !important;
padding: 40px !important;
text-align: center !important;
margin-bottom: 60px !important;
}

.intro-title {
background: linear-gradient(135deg, #e2c068 0%, #d4af37 100%) !important;
-webkit-background-clip: text !important;
-webkit-text-fill-color: transparent !important;
font-size: 32px !important;
font-weight: 800 !important;
display: inline-block !important;
margin-bottom: 15px !important;
}

/* 4. 서비스 카드 (그리드 복구) */
.service-list {
display: grid !important;
grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)) !important;
gap: 20px !important;
list-style: none !important;
padding: 0 !important;
margin: 0 !important;
}

.service-item {
background: #12151c !important;
border: 1px solid rgba(255, 255, 255, 0.1) !important;
border-radius: 12px !important;
padding: 25px !important;
margin: 0 !important;
}

.service-item strong {
display: block !important;
color: #e2c068 !important; /* 골드 */
font-size: 18px !important;
margin-bottom: 10px !important;
border-bottom: 1px solid rgba(226, 192, 104, 0.2) !important;
padding-bottom: 8px !important;
}

/* 링크 (가장 중요: 안 보이는 문제 해결) /
a {
color: #60a5fa !important; / 밝은 파란색 /
text-decoration: none !important;
font-weight: bold !important;
}
a:hover {
color: #e2c068 !important; / 호버 시 골드 */
text-decoration: underline !important;
}

/* 5. 기술 스택 박스 */
.tech-box {
background: #0f1115 !important;
border: 1px solid rgba(255, 255, 255, 0.1) !important;
border-radius: 12px !important;
padding: 25px !important;
margin-top: 20px !important;
}

.tech-item {
margin-bottom: 15px !important;
display: block !important;
}

.tech-label {
color: #e2c068 !important;
font-weight: bold !important;
font-size: 16px !important;
display: inline-block !important;
width: 80px !important;
}

.tech-content {
display: inline !important;
color: #e2e8f0 !important;
}

/* 6. 포스트 리스트 */
.post-list {
list-style: none !important;
padding: 0 !important;
}

.post-item {
padding: 15px 0 !important;
border-bottom: 1px solid rgba(255, 255, 255, 0.1) !important;
display: flex !important;
align-items: center !important;
}

.post-date {
color: #94a3b8 !important;
font-family: monospace !important;
margin-right: 15px !important;
font-size: 14px !important;
}

.post-link {
font-size: 18px !important;
color: #fff !important;
}
</style>

<!-- 본문 내용 -->

<div class="intro-container">
<h1 class="intro-title">💸 Money Flow & Code Vibe 👋</h1>
<p style="margin: 0;">
안녕하세요, <strong>"돈의 흐름을 추적하는 바이브 코딩"</strong>으로




핀테크 도구 <a href="https://sudanghelp.co.kr/" target="_blank">[수당헬프]</a>를 개발하는 <strong>Seansble</strong>입니다.






이곳은 서비스를 개발하며 겪은 기술적인 경험(PWA, SEO),




그리고 복잡한 금융 로직을 웹으로 구현한 과정을 기록합니다.
</p>
</div>

<h2 class="section-title">🗺️ Service Architecture</h2>
<p style="text-align: center; margin-bottom: 40px; color: #cbd5e1 !important;">
수당헬프는 단순한 계산기를 넘어, <strong>소득·지출·자산</strong>을 아우르는




3가지 핵심 축으로 구성되어 있습니다.
</p>

<h3>1.  소득 & 보장 (Income & Security)</h3>
<p style="margin-bottom: 15px;">국가에서 보장하는 권리와 혜택을 놓치지 않도록 돕습니다.</p>
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

<h3>2.  비용 & 지출 (Expense & Spending)</h3>
<p style="margin-bottom: 15px;">새는 돈을 막고, 합리적인 소비를 지원하는 도구입니다.</p>
<ul class="service-list">
<li class="service-item">
<strong>여행/환전</strong>
<a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank">PWA 환율 계산기</a>, 여행 가계부
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

<h3>3.  자산 형성 (Asset Building)</h3>
<p style="margin-bottom: 15px;">미래를 위한 자산 증식 시뮬레이션을 제공합니다.</p>
<ul class="service-list">
<li class="service-item">
<strong>복리</strong>
<a href="https://sudanghelp.co.kr/compoundcalc/" target="_blank">복리(예금/적금) 계산기</a>, 1억 만들기 플랜
</li>
<li class="service-item">
<strong>암호화폐>암호화>암>암n
<a href="https://sudanghelp.co.kr/coinmore/" target="_blank">코인 물타기 계산기</a>
</li>
</ul>

<h2 class="section-title">🛠️ Tech Stack</h2>
<div class="tech-box">
<div class="tech-item">
<span class="tech-label">Core</span>
<span class="tech-content">Vanilla JS, Cloudflare Workers</span>
</div>
<div class="tech-item">
<span class="tech-label">PWA</span>
<span class="tech-content">Service Worker, Manifest (Offline)</span>
</div>
<div class="tech-item">
<span class="tech-label">SEO</span>
<span class="tech-content">JSON-LD, Sitemap Clustering</span>
</div>
</div>

<h2 class="section-title">📝 Latest Dev Logs</h2>

<ul class="post-list">
{% for post in site.posts %}
<li class="post-item">
<span class="post-date">[{{ post.date | date: "%Y-%m-%d" }}]</span>
<a href="{{ post.url }}" class="post-link">{{ post.title }}</a>
</li>
{% endfor %}
</ul>
