# VISA FLOW AI 🦦

외교부·한국산업인력공단·한국장학재단·한국수출입은행 공공데이터 기반 AI 통합 비자 안내 플랫폼

여행 · 워킹홀리데이 · 해외취업 · 유학, 4가지 목적별 맞춤 비자 안내를 제공합니다.

## 미리보기

GitHub Pages 배포 후 아래 주소에서 바로 볼 수 있습니다.

```
https://<본인-github-아이디>.github.io/<저장소-이름>/
```

## 로컬에서 열어보기

별도 빌드 과정이 필요 없는 순수 HTML/CSS/JS 단일 파일입니다.
`index.html`을 더블클릭해서 브라우저로 열면 바로 실행됩니다.

## 주요 기능

- **목적별 맞춤 안내**: 여행 · 워킹홀리데이 · 해외취업 · 유학 × 국가별 비자 요건, 여행경보, 환율, 재외공관·한인회 정보
- **국가 비교**: 최대 3개국을 골라 비자유형·연령·체류기간·쿼터·비용·난이도를 한 표에서 비교, 목적별 공통 준비서류도 함께 표시
- **준비 서류 체크리스트**: 4개 목적 전부 제공, 결과 화면·국가비교·마이 대시보드에서 체크 상태가 서로 연동됨
- **마이 대시보드**: 진행률(%), D-DAY 가로 타임라인, 목적지 정보, 실시간 구글맵, 체크리스트(필수/상황별/참고 분류), AI 맞춤 조언을 한 화면에 정리
- **AI 챗봇 "비비(BIBI)"**: 문장에서 국가명을 우선 인식해 실데이터(연령기준·환율·여행경보·한인회 등) 기반으로 답변, 관련 질문 3개 자동 추천
- **국가 검색 자동완성 + 실시간 인기 검색어**
- **공지사항**: 최근 3개월 실제 공지 17건(워킹홀리데이·여행·취업·유학·설명회) + 실제 발행처 링크로 바로 연결, 새 공지 발생 시 팝업 알림(세션당 1회)
- **제출서류 · 공식 서식 모음** 페이지: 국가별 공식 신청서/서식 페이지 바로가기
- **D-DAY 출국 준비 타임라인 + 이메일 발송**: 체크리스트·타임라인 내용을 실제 이메일로 받아볼 수 있음 (아래 설정 참고)

## 이메일 자동발송 활성화 (선택)

정적 HTML 파일은 자체 서버가 없어서, 발송 계정을 연결해야 실제로 자동 발송됩니다. 아래 두 가지 중 하나를 설정하면 활성화되고, 아무것도 설정하지 않으면 메일 작성창(mailto)이 열리는 방식으로 대체 동작합니다.

`index.html`에서 `GAS_WEBAPP_URL` 또는 `EMAILJS_SERVICE_ID` 등을 검색하면 아래 코드를 바로 찾을 수 있습니다.

**방법 1) Google Apps Script (구글 계정만 있으면 됨, 별도 가입 불필요, 우선 적용)**
```js
const GAS_WEBAPP_URL=''; // script.google.com에서 배포한 웹앱 URL
```
1. [script.google.com](https://script.google.com) → 새 프로젝트 → 아래 코드 붙여넣기
   ```js
   function doPost(e) {
     const data = JSON.parse(e.postData.contents);
     MailApp.sendEmail(data.to, data.subject, data.message);
     return ContentService.createTextOutput(JSON.stringify({result:"success"}))
       .setMimeType(ContentService.MimeType.JSON);
   }
   ```
2. 배포 → 새 배포 → 유형: 웹 앱 → 액세스 권한: **모든 사용자(Anyone)** → 배포
3. 생성된 URL을 `GAS_WEBAPP_URL`에 붙여넣기

**방법 2) EmailJS (무료 가입 필요, GAS_WEBAPP_URL이 비어있을 때만 사용)**
```js
const EMAILJS_SERVICE_ID='';   // emailjs.com에서 발급
const EMAILJS_TEMPLATE_ID='';
const EMAILJS_PUBLIC_KEY='';
```
[emailjs.com](https://www.emailjs.com) 가입 → Email Services에서 Gmail 연결 → Service ID 복사 → Email Templates에서 템플릿 생성(변수: `to_email`, `subject`, `message`) → Template ID 복사 → Account → API Keys → Public Key 복사

## 폴더 구조

이미지(마스코트 등)가 전부 `index.html` 안에 base64로 인코딩되어 있어서, 별도 이미지 폴더 없이 파일 하나만 올리면 됩니다.

```
index.html   ← 이 파일 하나가 사이트 전체입니다
README.md
```

## 수정 후 재배포

```bash
git add index.html
git commit -m "수정 내용"
git push
```
1~2분 후 GitHub Pages에 자동 반영됩니다 (저장소의 `Actions` 탭에서 배포 진행 상황 확인 가능).

## 팀

최가은 · 배소현 — 2026 외교 공공데이터·AI 활용 경진대회
