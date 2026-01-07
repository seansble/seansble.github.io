layout: default title: 수당헬프 개발 기술 블로그

<!-- 🎨 스타일 정의 (가독성 & 카드 디자인 강화) -->

<style>
/* 1. 전체 레이아웃 & 기본 폰트 /
.wrapper {
max-width: 900px !important;
padding: 0 24px !important;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif !important;
color: #333;
line-height: 1.8; / 줄간격 더 시원하게 */
}

/* 2. 타이포그래피 (폰트 크기 UP) /
h1 {
font-size: 38px; / 제목 더 크게 /
font-weight: 800;
margin-top: 60px;
margin-bottom: 24px;
color: #111;
letter-spacing: -0.5px;
text-align: center; / 제목 중앙 정렬 */
}

h2.section-title {
font-size: 30px; /* 섹션 제목도 키움 */
font-weight: 700;
color: #222;
border-bottom: 3px solid #eee;
padding-bottom: 16px;
margin-top: 80px;
margin-bottom: 32px;
}

h3 {
font-size: 24px; /* 소제목 키움 */
font-weight: 700;
color: #444;
margin-top: 40px;
margin-bottom: 16px;
}

p {
font-size: 19px; /* ★ 본문 폰트 19px로 확대 ★ */
color: #4a4a4a;
margin-bottom: 28px;
word-break: keep-all;
}

li {
font-size: 19px; /* 리스트 폰트도 19px */
margin-bottom: 12px;
color: #4a4a4a;
}

/* 3. 인트로 카드 (깔끔한 박스 디자인) /
.intro-card {
background-color: #f8fafc;
border: 1px solid #e2e8f0;
border-radius: 16px;
padding: 40px;
margin-bottom: 60px;
text-align: center;
box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05); / 은은한 그림자 */
}

.intro-text {
font-size: 20px;
line-height: 1.6;
color: #475569;
margin: 0;
}

.intro-text strong {
color: #2563eb; /* 강조색 파랑 */
}

/* 4. 서비스 리스트 (카드형) */
.service-list {
list-style: none;
padding: 0;
margin: 0 0 50px 0;
}

.service-item {
background: #fff;
border: 1px solid #eee;
border-radius: 12px;
padding: 20px;
margin-bottom: 16px;
box-shadow: 0 2px 4px rgba(0,0,0,0.02);
transition: transform 0.2s;
}

.service-item:hover {
transform: translateY(-2px);
box-shadow: 0 4px 12px rgba(0,0,0,0.08);
border-color: #ddd;
}

.service-category {
font-weight: 800;
color: #1e293b;
font-size: 18px;
display: inline-block;
min-width: 100px;
margin-right: 12px;
}

/* 5. 링크 스타일 */
a {
color: #2563eb;
text-decoration: none;
font-weight: 600;
border-bottom: 1px solid transparent;
transition: all 0.2s;
}
a:hover {
border-bottom-color: #2563eb;
color: #1d4ed8;
}

/* 6. 기술 스택 (그리드 박스) /
.tech-container {
background: #1e293b; / 다크 모드 박스 */
color: #fff;
padding: 30px;
border-radius: 16px;
margin-bottom: 60px;
}

.tech-row {
margin-bottom: 20px;
font-size: 18px;
display: flex;
align-items: baseline;
}
.tech-row:last-child { margin-bottom: 0; }

.tech-label {
font-weight: 700;
color: #60a5fa; /* 밝은 파랑 */
width: 80px;
flex-shrink: 0;
}

.tech-content { color: #e2e8f0; }

/* 7. 글 목록 /
.post-list {
list-style: none;
padding: 0;
margin-top: 30px;
}
.post-item {
padding: 20px 0;
border-bottom: 1px solid #eee;
font-size: 19px; / 글 목록도 크게 */
display: flex;
align-items: center;
}
.post-date {
color: #94a3b8;
font-family: monospace;
font-size: 16px;
margin-right: 24px;
min-width: 120px;
}

/* 모바일 대응 */
@media (max-width: 768px) {
.wrapper { padding: 0 20px !important; }
h1 { font-size: 32px; margin-top: 40px; }
.intro-card { padding: 30px 20px; }
.intro-text { font-size: 18px; }
.tech-row { flex-direction: column; gap: 8px; }
.post-item { flex-direction: column; align-items: flex-start; gap: 8px; }
.post-date { margin-bottom: 0; }
}
</style>

<!-- 본문 시작 -->

<h1>💸 Money Flow & Code Vibe 👋</h1>

<div class="intro-card">
<p class="intro-text">
안녕하세요, <strong>"돈의 흐름을 추적하는 바이브 코딩"</strong>으로




핀테크 도구 <a href="https://sudanghelp.co.kr/" target="_blank">[수당헬프]</a>를 개발하는 <strong>Seansble</strong>입니다.






이곳은 서비스를 개발하며 겪은 기술적인 경험(PWA, SEO),




그리고 복잡한 금융 로직을 웹으로 구현한 과정을 기록합니다.
</p>
</div>

<h2 class="section-title">🗺️ Service Architecture</h2>
<p style="text-align: center; color: #666; margin-bottom: 50px;">
수당헬프는 단순한 계산기를 넘어,




<strong>소득 · 지출 · 자산</strong>을 아우르는 3가지 핵심 축으로 구성되어 있습니다.
</p>

<h3>1. 소득 & 보장 (Income)</h3>
<p style="margin-bottom: 15px; color: #666; font-size: 18px;">국가에서 보장하는 권리와 혜택을 놓치지 않도록 돕습니다.</p>
<ul class="service-list">
<li class="service-item">
<span class="service-category">출산/육아</span>
<a href="https://sudanghelp.co.kr/parents/" target="_blank">부모급여 통합 계산기</a>, 아동수당 가이드
</li>
<li class="service-item">
<span class="service-category">군인</span>
<a href="https://sudanghelp.co.kr/military/salary/" target="_blank">2026 군인 월급/적금 계산기</a>, 공군 점수 계산
</li>
<li class="service-item">
<span class="service-category">실업급여</span>
<a href="https://sudanghelp.co.kr/unemployment/" target="_blank">실업급여 모의계산</a>, 가이드
</li>
</ul>

<h3>2. 비용 & 지출 (Expense)</h3>
<p style="margin-bottom: 15px; color: #666; font-size: 18px;">새는 돈을 막고, 합리적인 소비를 지원하는 도구입니다.</p>
<ul class="service-list">
<li class="service-item">
<span class="service-category">여행/환전</span>
<a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank">PWA 환율 계산기 (오프라인 지원)</a>, 여행 가계부
</li>
<li class="service-item">
<span class="service-category">대출</span>
<a href="https://sudanghelp.co.kr/creditcalc/step-loan/" target="_blank">체증식 대출 계산기</a>, 중도상환수수료 계산
</li>
<li class="service-item">
<span class="service-category">세금(VAT)</span>
<a href="https://sudanghelp.co.kr/additionaltax/supply-calc/" target="_blank">부가세/공급가액 계산</a>, 간이과세 체크
</li>
<li class="service-item">
<span class="service-category">공과금</span>
<a href="https://sudanghelp.co.kr/electricity/" target="_blank">전기요금 누진세 계산기</a>
</li>
</ul>

<h3>3. 자산 형성 (Asset)</h3>
<p style="margin-bottom: 15px; color: #666; font-size: 18px;">미래를 위한 자산 증식 시뮬레이션을 제공합니다.</p>
<ul class="service-list">
<li class="service-item">
<span class="service-category">투자 설계</span>
<a href="https://sudanghelp.co.kr/compoundcalc/" target="_blank">복리(예금/적금) 계산기</a>, 1억 만들기 플랜
</li>
<li class="service-item">
<span class="service-category">크립토</span>
<a href="https://sudanghelp.co.kr/coinmore/" target="_blank">코인 물타기 계산기</a>
</li>
</ul>

<h2 class="section-title">🛠️ Tech Stack</h2>
<div class="tech-container">
<div class="tech-row">
<span class="tech-label">Core</span>
<span class="tech-content">Vanilla JS (Performance), Cloudflare Workers</span>
</div>
<div class="tech-row">
<span class="tech-label">PWA</span>
<span class="tech-content">Service Worker (Offline Support), Manifest</span>
</div>
<div class="tech-row">
<span class="tech-label">SEO</span>
<span class="tech-content">JSON-LD, Meta Tag Optimization, Sitemap</span>
</div>
</div>

<h2 class="section-title">📝 Latest Dev Logs</h2>
<ul class="post-list">
{% for post in site.posts %}
<li class="post-item">
<span class="post-date">[{{ post.date | date: "%Y-%m-%d" }}]</span>
<a href="{{ post.url }}">{{ post.title }}</a>
</li>
{% endfor %}
</ul>
