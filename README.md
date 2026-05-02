# 면접 평가표 (Interview Evaluation Tool) - 엠아이텍

GitHub Pages에 배포 가능한 1-파일 HTML 면접 평가 도구. 모든 데이터는 브라우저 `localStorage`에 저장됩니다 (서버 불필요).

## ✨ 주요 기능

### 기본 평가
- 부서별 평가 항목 (영업마케팅·개발·연구·품질인허가·생산·F&C·HR)
- 회사 공통 인재상 4개 (목표지향·팀워크·학습과 도전·혁신추구)
- 5단계 평가 척도 (Strong no / No / Mixed / Yes / Strong yes)
- S-T-A-R 후속 질문 자동 표시
- 면접관 메모, 평가 요약, 분포 차트
- 인쇄/PDF·JSON·CSV 내보내기

### 🤖 AI 기능 (Gemini API)
1. **AI 맞춤 질문 생성**
   - 후보자 이력서 + 채용공고 업로드 → 7-10개 맞춤 질문 자동 생성
   - 후보자 강점/우려사항 요약, 직무 적합도 분석
   - 각 질문별 추천 이유 + STAR 후속 질문 제공
   - 평가표 항목에 한 번의 클릭으로 적용

2. **실시간 답변 분석**
   - 🎤 한국어 음성 인식으로 후보자 답변 받아쓰기 (Web Speech API)
   - 또는 직접 텍스트 입력
   - AI 분석 결과:
     - 추천 평가 등급 (자동 적용 가능)
     - **STAR 프레임워크 충족 분석** (Situation/Task/Action/Result)
     - 강점 및 우려사항 도출
     - 추가 검증을 위한 후속 질문 추천 (평가표에 바로 적용)

### 관리자 기능
- 비밀번호 보호 (기본: `5245`)
- 평가 기록 관리 (검색/삭제/CSV 내보내기)
- 부서별 질문은행 편집
- 비밀번호 변경, 회사명 설정, API 키 관리

## 🚀 GitHub Pages 배포 방법

1. GitHub에서 새 저장소(repository) 생성 (Public)
2. `index.html` 파일을 저장소 루트에 업로드 (필요시 `README.md`도 함께)
3. **Settings → Pages** 메뉴 진입
4. Source: `Deploy from a branch` → Branch: `main` (혹은 `master`) → Folder: `/ (root)` 선택 후 Save
5. 잠시 후 `https://<유저네임>.github.io/<저장소명>/` 주소로 접속

## 🔑 Gemini API 키 설정 (AI 기능 사용 시 필수)

AI 기능(질문 생성·답변 분석)을 사용하려면 무료 Gemini API 키가 필요합니다.

1. [Google AI Studio](https://aistudio.google.com/app/apikey) 접속
2. **Create API key** 클릭 → `AIza...` 형식의 키 복사
3. 평가표 우측 상단 ⚙️ **관리자** → 비밀번호 입력 (기본 `5245`)
4. **🔧 설정** 탭 → **Gemini API 키** 필드에 붙여넣기 → **API 키 저장**

> ⚠️ API 키는 브라우저 `localStorage`에만 저장되며 외부 서버로 전송되지 않습니다. 사용량 한도는 [Gemini 무료 등급 정책](https://ai.google.dev/pricing) 참조.

## 🌐 브라우저 호환성

| 기능 | 권장 브라우저 |
|------|--------------|
| 기본 평가 기능 | Chrome, Edge, Safari, Firefox |
| AI 질문 생성 | Chrome, Edge, Safari, Firefox |
| 🎤 음성 인식 | **Chrome, Edge** (HTTPS 필수, GitHub Pages는 자동 지원) |

> 음성 인식은 Web Speech API를 사용하며, Firefox에서는 작동하지 않을 수 있습니다.

## 💡 사용 팁

### 면접 전 (질문 준비)
1. 헤더의 🤖 **AI 어시스턴트** 클릭
2. **질문 생성** 탭 → 이력서·채용공고 업로드 (PDF·이미지·TXT 지원)
3. 부서·직무 정보가 자동 활용됨
4. 생성된 질문에서 **✓ 평가표에 적용** 클릭 → 항목 번호 입력하여 적용

### 면접 중 (답변 분석)
1. 평가 항목 카드의 🎤 **답변 분석** 버튼 클릭 → 질문 자동 입력
2. 🎤 마이크 버튼으로 받아쓰기 시작 (또는 직접 입력)
3. 🔍 **답변 분석하기** 클릭 → AI가 STAR 분석 + 강약점 + 후속 질문 제공
4. 추천 등급 → **이 등급으로 평가하기** 클릭 시 평가표에 자동 반영
5. 추천 후속 질문 → **적용** 클릭 시 평가표 후속 질문 영역에 추가

## 🔒 보안 참고

- 모든 데이터(평가 기록·API 키·질문은행)는 사용자 **브라우저에만** 저장
- 서버나 데이터베이스 없음
- 다른 기기·브라우저에서 보려면 **JSON 내보내기** 후 옮겨야 함
- 데이터 삭제: 관리자 → 설정 → **전체 데이터 초기화**

## 📂 데이터 구조 (localStorage)

| 키 | 내용 |
|----|------|
| `evaluations` | 저장된 평가 기록 배열 |
| `qb_<부서명>` | 부서별 커스텀 질문은행 |
| `adminPassword` | 관리자 비밀번호 |
| `geminiApiKey` | Gemini API 키 |
| `settings` | 회사명 등 설정 |

## 🛠 기술 스택

- 순수 HTML/CSS/JavaScript (외부 라이브러리 없음, 단일 파일)
- localStorage 기반 영속성
- Web Speech API (음성 인식)
- Google Gemini 2.5 Flash (AI 분석, 멀티모달 PDF/이미지 지원)

---
Made for 엠아이텍 (M.I.Tech) HR Team
