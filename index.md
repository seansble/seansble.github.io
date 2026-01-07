layout: default title: 수당헬프 개발 기술 블로그

💸 Money Flow & Code Vibe 👋

안녕하세요, **"돈의 흐름을 추적하는 바이브 코딩"**으로 핀테크 도구 수당헬프를 개발하는 Seansble입니다.
이곳은 서비스를 개발하며 겪은 기술적인 경험(PWA, SEO), 그리고 복잡한 금융 로직을 웹으로 구현한 과정을 기록합니다.

🗺️ Service Architecture

수당헬프는 단순한 계산기를 넘어, 소득·지출·자산을 아우르는 3가지 핵심 축으로 구성되어 있습니다.

1. 💵 소득 & 보장 (Income & Security)

국가에서 보장하는 권리와 혜택을 놓치지 않도록 돕습니다.

출산/육아: 부모급여 통합 계산기, 아동수당 가이드

군인/장병: 2026 군인 월급/적금 계산기, 공군 점수 계산

사회안전망: 실업급여 모의계산, 4대보험, 청년지원금

2. 💸 비용 & 방어 (Expense & Defense)

새는 돈을 막고, 합리적인 소비를 지원하는 도구입니다.

여행/환전: PWA 환율 계산기 (오프라인 지원), 여행 가계부

대출/이자: 중도상환수수료 계산, 체증식 상환, 비상금 대출

세금/공과금: 부가세/공급가액 계산, 전기요금 누진세 측정

3. 💰 자산 형성 (Asset Building)

미래를 위한 자산 증식 시뮬레이션을 제공합니다.

투자 설계: 복리(예금/적금) 계산기, 1억 만들기 플랜

크립토: 코인 물타기 계산기

🛠️ Tech Stack

Core: Vanilla JS (Performance), Cloudflare Workers (Edge Computing)

PWA: Service Worker (Offline Support), Manifest (Installable)

SEO: JSON-LD Structure, Meta Tag Optimization, Sitemap Clustering

📝 Latest Dev Logs (최신 개발기)

<ul>
{% for post in site.posts %}
<li>
<span style="color: #666; font-size: 0.9em; margin-right: 10px;">[{{ post.date | date: "%Y-%m-%d" }}]</span>
<a href="{{ post.url }}" style="font-weight: bold;">{{ post.title }}</a>
</li>
{% endfor %}
</ul>
