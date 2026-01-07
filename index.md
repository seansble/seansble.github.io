layout: default title: 수당헬프 개발 기술 블로그

<!-- 🎨 스타일 정의 (심플 & 클린) -->

<style>
/* 1. 전체 레이아웃 /
.wrapper {
max-width: 900px !important; / 읽기 가장 편한 폭 */
padding: 0 20px !important;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif !important;
color: #333;
line-height: 1.7;
}

/* 2. 타이포그래피 (위계질서 확립) */
h1 {
font-size: 34px;
font-weight: 800;
color: #111;
margin-top: 60px;
margin-bottom: 20px;
letter-spacing: -0.5px;
}

h2.section-title {
font-size: 26px;
font-weight: 700;
color: #222;
border-bottom: 2px solid #eee; /* 깔끔한 구분선 /
padding-bottom: 12px;
margin-top: 70px; / 섹션 간격 넓게 */
margin-bottom: 24px;
}

h3 {
font-size: 20px;
font-weight: 600;
color: #444;
margin-top: 30px;
margin-bottom: 12px;
}

p {
font-size: 17px;
color: #555;
margin-bottom: 24px;
word-break: keep-all; /* 단어 단위 줄바꿈 */
}

/* 3. 인트로 박스 (미니멀) */
.intro-container {
background-color: #f9f9f9;
padding: 40px;
border-radius: 8px;
margin-bottom: 60px;
text-align: center;
}

.intro-title {
font-size: 30px;
font-weight: 800;
margin-bottom: 16px;
color: #111;
}

.intro-desc {
font-size: 18px;
color: #666;
margin: 0;
}

/* 4. 서비스 리스트 (깔끔한 목록형) */
.service-list {
list-style: none;
padding: 0;
margin: 0;
}

.service-item {
margin-bottom: 12px;
padding-left: 16px;
border-left: 3px solid #ddd; /* 왼쪽 포인트 선 */
font-size: 17px;
}

.service-category {
font-weight: 700;
color: #333;
margin-right: 8px;
}

/* 5. 링크 스타일 (가독성 파란색) /
a {
color: #0366d6; / 깃허브 블루 */
text-decoration: none;
font-weight: 500;
}
a:hover {
text-decoration: underline;
}

/* 6. 기술 스택 (심플 박스) */
.tech-container {
background: #f1f3f5;
padding: 24px;
border-radius: 8px;
}
.tech-row {
margin-bottom: 10px;
font-size: 16px;
}
.tech-label {
font-weight: 700;
color: #111;
display: inline-block;
width: 60px;
}

/* 7. 글 목록 */
.post-list {
list-style: none;
padding: 0;
}
.post-item {
padding: 12px 0;
border-bottom: 1px solid #eee;
font-size: 17px;
}
.post-date {
color: #888;
font-family: monospace;
font-size: 14px;
margin-right: 12px;
}

/* 모바일 대응 */
@media (max-width: 768px) {
.wrapper { padding: 0 16px !important; }
h1 { font-size: 28px; }
h2.section-title { font-size: 22px; margin-top: 50px; }
.intro-container { padding: 24px; }
}
</style>

<!-- 본문 시작 -->

<div class="intro-container">
<div class="intro-title">💸 Money Flow & Code Vibe 👋</div>
<p class="intro-desc">
안녕하세요, <strong>"돈의 흐름을 추적하는 바이브 코딩"</strong>으로




핀테크 도구 <a href="https://sudanghelp.co.kr/" target="_blank">[수당헬프]</a>를 개발하는 <strong>Seansble</strong>입니다.






이곳은 서비스를 개발하며 겪은 기술적인 경험(PWA, SEO),




그리고 복잡한 금융 로직을 웹으로 구현한 과정을 기록합니다.
</p>
</div>

<h2 class="section-title">🗺️ Service Architecture</h2>
<p>
수당헬프는 단순한 계산기를 넘어,




<strong>소득 · 지출 · 자산</strong>을 아우르는 3가지 핵심 축으로 구성되어 있습니다.
</p>

<h3>1. 💵 소득 & 보장 (Income & Security)</h3>
<p style="margin-bottom: 10px; font-size: 16px; color: #666;">국가에서 보장하는 권리와 혜택을 놓치지 않도록 돕습니다.</p>
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

<h3>2. 💸 비용 & 지출 (Expense & Spending)</h3>
<p style="margin-bottom: 10px; font-size: 16px; color: #666;">새는 돈을 막고, 합리적인 소비를 지원하는 도구입니다.</p>
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

<h3>3. 💰 자산 형성 (Asset Building)</h3>
<p style="margin-bottom: 10px; font-size: 16px; color: #666;">미래를 위한 자산 증식 시뮬레이션을 제공합니다.</p>
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
<span class="tech-label">Core</span> Vanilla JS (Performance), Cloudflare Workers
</div>
<div class="tech-row">
<span class="tech-label">PWA</span> Service Worker (Offline Support), Manifest
</div>
<div class="tech-row">
<span class="tech-label">SEO</span> JSON-LD, Meta Tag Optimization, Sitemap
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
