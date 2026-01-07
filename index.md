layout: default title: 수당헬프 개발 기술 블로그

<!-- 🎨 스타일 정의 -->

<style>
/* 1. 전체 레이아웃 & 기본 폰트 */
.wrapper {
max-width: 1200px !important;
padding: 0 40px !important;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif !important;
line-height: 1.7;
color: #334155;
}

/* 2. 타이포그래피 & 여백 규칙 */
h1 {
font-size: 32px;
font-weight: 800;
margin-top: 60px;
margin-bottom: 24px;
color: #1e293b;
}

h2.section-title {
font-size: 28px;
font-weight: 700;
color: #1e293b;
border-bottom: 2px solid #e2e8f0;
padding-bottom: 12px;
margin-top: 80px;
margin-bottom: 32px;
}

h3 {
font-size: 22px;
font-weight: 600;
color: #334155;
margin-top: 40px;
margin-bottom: 16px;
}

p {
font-size: 17px;
margin-bottom: 24px;
word-break: keep-all;
}

ul { margin-bottom: 24px; padding-left: 20px; }
li { margin-bottom: 8px; font-size: 17px; }

/* 3. 인트로 박스 */
.intro-container {
background: #f8fafc;
border: 1px solid #e2e8f0;
border-radius: 16px;
padding: 60px 40px;
text-align: center;
margin-bottom: 80px;
}

.intro-title {
font-size: 36px;
font-weight: 800;
margin-bottom: 24px;
background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
display: inline-block;
}

.intro-desc {
font-size: 20px;
line-height: 1.6;
color: #475569;
margin: 0;
}

/* 4. 서비스 카드 그리드 */
.service-list {
list-style: none;
padding: 0;
margin: 0;
display: grid;
grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
gap: 24px;
}

.service-item {
margin-bottom: 0;
padding: 24px;
background: #fff;
border: 1px solid #e2e8f0;
border-radius: 12px;
font-size: 17px;
color: #334155;
line-height: 1.6;
transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s;
}

.service-item:hover {
transform: translateY(-4px);
box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
border-color: #cbd5e1;
}

.service-item strong {
display: block;
color: #1e293b;
font-size: 18px;
margin-bottom: 8px;
}

/* 5. 링크 스타일 */
a {
color: #2563eb;
text-decoration: none;
font-weight: 600;
transition: all 0.2s;
border-bottom: 1px solid transparent;
}
a:hover {
color: #1d4ed8;
border-bottom-color: #1d4ed8;
}

/* 6. 기술 스택 박스 */
.tech-box {
background: #1e293b;
color: #f1f5f9;
border-radius: 16px;
padding: 32px;
margin-top: 24px;
display: grid;
grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
gap: 24px;
box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

.tech-item {
display: flex;
flex-direction: column;
font-size: 16px;
}

.tech-label {
font-weight: 700;
color: #60a5fa;
margin-bottom: 8px;
font-size: 18px;
display: block;
border-bottom: 1px solid #334155;
padding-bottom: 4px;
width: fit-content;
}

.tech-content { color: #e2e8f0; line-height: 1.6; }
.tech-keyword { color: #fcd34d; font-weight: 600; }
.tech-sub { color: #94a3b8; font-size: 0.9em; }

/* 7. 최신 글 목록 */
.post-list {
list-style: none;
padding: 0;
margin-top: 24px;
}

.post-item {
padding: 20px 0;
border-bottom: 1px solid #f1f5f9;
display: flex;
align-items: baseline;
transition: background-color 0.2s;
}
.post-item:hover {
background-color: #f8fafc;
padding-left: 10px;
border-radius: 8px;
}

.post-date {
font-family: 'Consolas', monospace;
color: #64748b;
font-size: 15px;
margin-right: 24px;
flex-shrink: 0;
min-width: 100px;
}

.post-link {
font-size: 20px;
color: #1e293b;
font-weight: 600;
border-bottom: none;
}
.post-link:hover {
color: #2563eb;
border-bottom: none;
}

/* 모바일 대응 */
@media (max-width: 768px) {
.wrapper { padding: 0 20px !important; }
.intro-container { padding: 40px 20px; margin-bottom: 40px; }
.intro-title { font-size: 28px; }
.intro-desc { font-size: 16px; }
h2.section-title { font-size: 24px; margin-top: 60px; }
.post-item { flex-direction: column; gap: 4px; }
.post-date { margin-bottom: 4px; font-size: 13px; }
.post-link { font-size: 18px; }
}
</style>

<!-- 본문 시작 -->

<div class="intro-container">
<h1 class="intro-title">💸 Money Flow & Code Vibe 👋</h1>
<p class="intro-desc">
안녕하세요, <strong>"돈의 흐름을 추적하는 바이브 코딩"</strong>으로




핀테크 도구 <a href="https://sudanghelp.co.kr/" target="_blank">[수당헬프]</a>를 개발하는 <strong>Seansble</strong>입니다.






이곳은 서비스를 개발하며 겪은 기술적인 경험(PWA, SEO),




그리고 복잡한 금융 로직을 웹으로 구현한 과정을 기록합니다.
</p>
</div>

<h2 class="section-title">🗺️ Service Architecture</h2>
<p style="font-size: 18px; color: #475569; margin-bottom: 40px; text-align: center;">
수당헬프는 단순한 계산기를 넘어, <strong>소득·지출·자산</strong>을 아우르는 3가지 핵심 축으로 구성되어 있습니다.
</p>

<h3>1. 💵 소득 & 보장 (Income & Security)</h3>
<p style="color: #64748b; margin-bottom: 16px;">국가에서 보장하는 권리와 혜택을 놓치지 않도록 돕습니다.</p>
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
<p style="color: #64748b; margin-bottom: 16px;">새는 돈을 막고, 합리적인 소비를 지원하는 도구입니다.</p>
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
<p style="color: #64748b; margin-bottom: 16px;">미래를 위한 자산 증식 시뮬레이션을 제공합니다.</p>
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
<span class="tech-keyword">Vanilla JS</span> <span class="tech-sub">(Performance)</span>,
<span class="tech-keyword">Cloudflare Workers</span> <span class="tech-sub">(Edge Computing)</span>
</div>
</div>
<div class="tech-item">
<span class="tech-label">PWA</span>
<div class="tech-content">
<span class="tech-keyword">Service Worker</span> <span class="tech-sub">(Offline Support)</span>,
<span class="tech-keyword">Manifest</span> <span class="tech-sub">(Installable)</span>
</div>
</div>
<div class="tech-item">
<span class="tech-label">SEO</span>
<div class="tech-content">
<span class="tech-keyword">JSON-LD Structure</span>,
<span class="tech-keyword">Meta Tag Optimization</span>,
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
