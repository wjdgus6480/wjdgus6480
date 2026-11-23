## Featured Projects

<table>
<tr><td>

### 🚃 다누비 AI — 태종대 관광 코스 판단 서비스

도착 날짜·시각 기준으로 **오늘 태종대에서 실제로 가능한 코스**를 판단해 주는 모바일 웹입니다. 부산관광공사 AI데이터활용 공모전 수상작입니다.

- **해결하려는 문제** — 다누비 시간표가 평일·휴일·성수기마다 다르고 휴무일도 있어서, 현장에 도착한 관광객이 "지금 들어가면 다 보고 나올 수 있나"를 판단하기 어렵습니다.
- **담당 역할** — 1인 진행 (기획 · 데이터 검증 · 추천 엔진 · 화면 · 배포)
- **주요 기술** — JavaScript (ES Modules, 외부 패키지 0개) · Node.js · node:test · SVG · Netlify
- **추천이 동작하는 방식**
  1. 사용자가 질문 4개(체류 시간 · 걷기 정도 · 이동 방식 · 여행 목적)를 고릅니다.
  2. 엔진이 다누비 · 도보 · 차량 3개 플랜을 만들고, 휴관·운휴·막차 같은 제약을 **게이트(통과/불통과)** 로 먼저 거릅니다.
  3. 통과한 플랜만 이동성 · 목적 · 시간 가중치로 점수를 매기고, 시간표로 다시 검증합니다.
  4. 결과는 통과 · 조건부 · 불가 · 자료 부족 4단계로 표시하고, 탈락한 플랜과 그 이유까지 보여 줍니다.
  - LLM을 쓰지 않는 **규칙 기반 엔진 + 템플릿 문장**이며, 서버 없이 브라우저에서 실행됩니다. 사용자가 고른 이동 방식은 임의로 바꾸지 않습니다.
- **주요 구현**
  - 공공데이터 4종을 검증해 3종만 사용 — "운행정보 및 도착시간" 데이터는 실측값이 아니어서 제외
  - 원본 CSV를 sha256으로 고정하고 스크립트로 런타임 데이터 생성
  - 판단 과정 12단계를 로그로 남겨 화면의 "왜 이 결과인가"에 표시 · 한/영/일/중 4개 언어
  - 테스트 105개, 480개 입력 조합 × 3개 시나리오 불변식 테스트

🔗 [Demo](https://prismatic-dasik-d01617.netlify.app/)

</td></tr>
</table>

<table>
<tr><td>

### 🏠 집플랜 — 부산 전월세 × 주거정책 판정 서비스

부산 전월세 매물마다 **내 조건으로 받을 수 있는 주거지원 정책**을 판정해 주는 서비스입니다.

- **해결하려는 문제** — 매물 앱과 정책 포털이 따로 있어서, 계약한 뒤에야 지원 대상이 아니라는 걸 알게 됩니다. 같은 사람도 보증금·면적·주택 유형에 따라 받을 수 있는 정책이 달라집니다.
- **담당 역할** — 1인 개발 (공공데이터 수집 · DB 설계 · 판정 엔진 · API · 화면 · 배포)
- **주요 기술** — Next.js 16 · React 19 · TypeScript · MySQL (배포: TiDB Cloud) · Vitest · GitHub Actions · Vercel
- **주요 구현**
  - 국토부 실거래 · 건축물대장 · 학교 등 공공데이터 수집 스크립트 → 검사 → 트랜잭션 적재
  - 실거래를 건물 필지(PNU)에 연결해 아파트 거래 지도 노출을 **54% → 99.97%** 로 개선
  - 정책 판정은 DB와 분리된 서버 전용 순수 함수 — 충족 · 추가 확인 · 미충족 3단계, 기준일(asOf)로 과거 판정 재현
  - 조회는 Route Handler(GET), 저장·회원 작업은 Server Actions / 테이블 44개 · 마이그레이션 41개
  - CI에서 빈 MySQL 8.4에 마이그레이션부터 다시 만들고 저장소 통합 테스트 → build

🔗 [Demo](https://jipplan-two.vercel.app/)

</td></tr>
</table>

<table>
<tr><td>

### 🧵 Genloom — 검색 데이터 기반 콘텐츠 그로스 시스템

검색 데이터로 기획한 브리프를 **글 · 이미지 · 검토 역할의 AI 모델이 이어받아** 블로그 글 초안을 만드는 개인용 시스템입니다.

- **해결하려는 문제** — AI 글쓰기 도구는 검색 데이터·사실 검증과 끊겨 있어서, 그대로 올리면 틀린 내용이 발행될 수 있습니다.
- **담당 역할** — 1인 개발 및 운영
- **주요 기술** — Python · 네이버 검색/데이터랩 API · LLM API · matplotlib · Playwright · unittest
- **주요 구현**
  - 네이버 API로 키워드 기회지수를 측정하고, 사실·출처·기준일을 담은 브리프 생성
  - 이미지는 AI가 차트 명세(JSON)만 작성하고 프로그램이 그림 (한글·숫자 깨짐 방지)
  - 단계마다 GREEN · YELLOW · RED 규칙 검수, RED면 자동 중단 — **발행은 사람만** (자동 발행 0회)
  - 파이썬 테스트 448개, 테스트 중 네트워크 호출 0회 · 실제 블로그 14편 발행

🔗 [운영 블로그](https://blog.naver.com/wjdgus6480)

</td></tr>
</table>

<br>

<br>

## Tech Stack

<p>
<img src="assets/stack/label-backend.svg" height="38" alt="Backend">
<img src="assets/stack/nodedotjs.svg" height="38" alt="Node.js">
<img src="assets/stack/typescript.svg" height="38" alt="TypeScript">
<img src="assets/stack/api.svg" height="38" alt="REST API">
</p>

<p>
<img src="assets/stack/label-frontend.svg" height="38" alt="Frontend">
<img src="assets/stack/nextdotjs.svg" height="38" alt="Next.js">
<img src="assets/stack/react.svg" height="38" alt="React">
</p>

<p>
<img src="assets/stack/label-database.svg" height="38" alt="Database">
<img src="assets/stack/mysql.svg" height="38" alt="MySQL">
<img src="assets/stack/supabase.svg" height="38" alt="Supabase">
</p>

<p>
<img src="assets/stack/label-ai-data.svg" height="38" alt="AI & Data">
<img src="assets/stack/python.svg" height="38" alt="Python">
<img src="assets/stack/pandas.svg" height="38" alt="Pandas">
<img src="assets/stack/numpy.svg" height="38" alt="NumPy">
<img src="assets/stack/scikitlearn.svg" height="38" alt="scikit-learn (학습 중)">
</p>

<p>
<img src="assets/stack/label-tools.svg" height="38" alt="Tools">
<img src="assets/stack/git.svg" height="38" alt="Git">
<img src="assets/stack/github.svg" height="38" alt="GitHub">
<img src="assets/stack/vitest.svg" height="38" alt="Vitest">
<img src="assets/stack/githubactions.svg" height="38" alt="GitHub Actions">
</p>
