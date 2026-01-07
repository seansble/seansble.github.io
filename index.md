layout: default title: 수당헬프 개발 기술 블로그

<!-- 🎨 스타일 정의 -->

<style>
/* 전체 레이아웃 - 너비 확장 (900px -> 1200px) */
.wrapper {
max-width: 1200px !important;
padding: 0 40px !important;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif !important;
}

/* 인트로 박스 */
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
margin-bottom: 20px;
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

/* 섹션 제목 */
h2.section-title {
font-size: 28px;
font-weight: 700;
color: #1e293b;
border-bottom: 2px solid #e2e8f0;
padding-bottom: 16px;
margin-top: 80px;
margin-bottom: 32px;
}

/* 서비스 목록 스타일 */
.service-list {
list-style: none;
padding: 0;
margin: 0;
display: grid;
grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
gap: 20px;
}

.service-item {
margin-bottom: 0;
padding: 20px;
background: #fff;
border: 1px solid #e2e8f0;
border-radius: 12px;
font-size: 17px;
color: #334155;
line-height: 1.6;
transition: transform 0.2s, box-shadow 0.2s;
}

.service-item:hover {
transform: translateY(-2px);
box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
border-color: #cbd5e1;
}

/* 링크 스타일 */
a {
color: #2563eb;
text-decoration: none;
font-weight: 600;
transition: all 0.2s;
}
a:hover {
text-decoration: underline;
color: #1d4ed8;
}

/* 기술 스택 박스 */
.tech-box {
background: #1e293b;
color: #fff;
border-radius: 16px;
padding: 32px;
margin-top: 24px;
display: grid;
grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
gap: 24px;
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
}

/* 최신 글 목록 */
.post-list {
list-style: none;
padding: 0;
}

.post-item {
padding: 20px 0;
border-bottom: 1px solid #f1f5f9;
display: flex;
align-items: baseline;
}

.post-date {
font-family: monospace;
color: #64748b;
font-size: 15px;
margin-right: 24px;
flex-shrink: 0;
}

.post-link {
font-size: 20px;
color: #1e293b;
font-weight: 600;
}
.post-link:hover {
color: #2563eb;
}

/* 모바일 대응 */
@media (max-width: 768px) {
.wrapper { padding: 0 20px !important; }
.post-item { flex-direction: column; gap: 4px; }
.post-date { margin-bottom: 4px; }
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
<li class="service-item"><strong>출산/육아:</strong>



<a href="https://sudanghelp.co.kr/parents/" target="_blank">부모급여 통합 계산기</a>, 아동수당 가이드</li>
<li class="service-item"><strong>군인/장병:</strong>



<a href="https://sudanghelp.co.kr/military/salary/" target="_blank">2026 군인 월급/적금 계산기</a>, 공군 점수 계산</li>
<li class="service-item"><strong>사회안전망:</strong>



<a href="https://sudanghelp.co.kr/unemployment/" target="_blank">실업급여 모의계산</a>, 4대보험, 청년지원금</li>
</ul>

<h3>2. 💸 비용 & 지출 (Expense & Spending)</h3>
<p style="color: #64748b; margin-bottom: 16px;">새는 돈을 막고, 합리적인 소비를 지원하는 도구입니다.</p>
<ul class="service-list">
<li class="service-item"><strong>여행/환전:</strong>



<a href="https://sudanghelp.co.kr/travel/exchange-calculator/" target="_blank">PWA 환율 계산기 (오프라인 지원)</a>, 여행 가계부</li>
<li class="service-item"><strong>대출/이자:</strong>



<a href="https://sudanghelp.co.kr/creditcalc/prepay-calc/" target="_blank">중도상환수수료 계산</a>, 체증식 상환, 비상금 대출</li>
<li class="service-item"><strong>세금/공과금:</strong>



<a href="https://sudanghelp.co.kr/additionaltax/supply-calc/" target="_blank">부가세/공급가액 계산</a>, 전기요금 누진세 측정</li>
</ul>

<h3>3. 💰 자산 형성 (Asset Building)</h3>
<p style="color: #64748b; margin-bottom: 16px;">미래를 위한 자산 증식 시뮬레이션을 제공합니다.</p>
<ul class="service-list">
<li class="service-item"><strong>투자 설계:</strong>



<a href="https://sudanghelp.co.kr/compoundcalc/" target="_blank">복리(예금/적금) 계산기</a>, 1억 만들기 플랜</li>
<li class="service-item"><strong>크립토:</strong>



<a href="https://sudanghelp.co.kr/coinmore/" target="_blank">코인 물타기 계산기</a></li>
</ul>

<h2 class="section-title">🛠️ Tech Stack</h2>
<div class="tech-box">
<div class="tech-item"><span class="tech-label">Core</span>Vanilla JS (Performance), Cloudflare Workers (Edge Computing)</div>
<div class="tech-item"><span class="tech-label">PWA</span>Service Worker (Offline Support), Manifest (Installable)</div>
<div class="tech-item"><span class="tech-label">SEO</span>JSON-LD Structure, Meta Tag Optimization, Sitemap Clustering</div>
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
