# 🔬 EAIM 과학 놀이터

> 감정과 이야기로 배우는 과학 교과 AI 도구 모음
> Emotion · Artscape · Interactive · Musicalization

중학교 과학 수업에서 사용하는 AI 기반 학습 도구 3종을 모은 놀이터입니다. 국어 놀이터(`eaim-korean-play`)와 같은 Firebase 교실 구조를 공유하며, 교사가 반/모둠과 API 키를 한 번 설정해두면 학생들은 QR코드나 링크로 바로 접속해 수업에 참여할 수 있습니다.

🔗 배포 주소: https://eaim-science-lap.vercel.app

---

## 📚 포함된 앱

| 앱 | 설명 | 파일 |
|---|---|---|
| 🕵️‍♂️ **EAIM 생활 과학 공감 톡** | 교사가 정한 단원으로 AI가 감정 이입되는 일상 이야기와 과학 퀴즈를 생성. 학생은 정답 + 과학적 근거 + 등장인물 공감을 적고 AI 피드백을 받음 | `science.html` |
| 🌌 **EAIM 태양계 오디세이** | 3D 태양계 공전·자전 시뮬레이터. 학생이 조작한 속도·크기 상태를 바탕으로 AI가 관측 질문을 생성하고, 서술형 답변에 피드백 제공 | `space.html` |
| 🔭 **EAIM 천문대 관측소** | NASA 텍스처 기반 9개 천체(태양·달 포함) 정밀 3D 관측. 학생이 쓴 관찰일지에 AI가 피드백하고 기록을 누적 | `observatory.html` |

허브 페이지(`index.html`)에서 세 앱으로 이동할 수 있습니다.

---

## 🏗️ 구조

모든 앱은 하나의 Firebase 프로젝트(`eaim-classroom`)를 공유합니다.

```
teachers/{교사UID}/
├── meta/settings        # API 키, 수업 ON/OFF, (공감톡은) 오늘의 단원
├── groups/               # 반/모둠 이름 목록
├── students/             # 학생별 최신 활동 현황 요약
├── scienceMissions/      # 공감 톡 미션 기록 전체 이력
├── odysseyMissions/      # 태양계 오디세이 관측 미션 기록 전체 이력
└── observatoryLogs/      # 천문대 관측 일지 기록 전체 이력
```

- **교사**: 구글 계정으로 로그인 → API 키·반/모둠·수업 ON/OFF 설정 → 학생 초대 QR/링크 공유
- **학생**: 교사가 준 링크(`?role=student&teacher={uid}`)로 접속 → 이름 + 반/모둠 선택 → 바로 활동 시작 (API 키를 직접 입력할 필요 없음)

---

## ⚙️ 사용 준비 (교사)

1. **Gemini API 키 발급**
   [Google AI Studio](https://aistudio.google.com) → `Get API key` → `Create API key`
2. **앱 접속 후 구글 로그인**
   `science.html`, `space.html`, `observatory.html` 중 아무 곳이나 열어 구글 계정으로 로그인
3. **교사 대시보드에서 설정**
   - API 키 입력 (3개 앱 중 한 곳에서만 입력하면 나머지 앱에도 자동 반영)
   - 반/모둠 이름 추가
   - 수업 진행 상태 ON
   - 학생 초대 링크·QR 복사
4. **생활 과학 공감 톡만 추가로**: "오늘의 단원"을 입력해두면 학생 화면에 자동 표시됩니다.

무료 티어(분당 15회, 하루 1,500회)로 수업 활용에는 충분합니다.

---

## 🚀 배포 (GitHub Pages / Vercel)

파일명을 그대로 유지해서 업로드해야 앱 간 이동 링크(`index.html` 등)가 깨지지 않습니다.

```
📁 eaim-science-lap/
├── index.html          ← 과학 놀이터 허브
├── science.html         ← 생활 과학 공감 톡
├── space.html            ← 태양계 오디세이
└── observatory.html      ← 천문대 관측소
```

GitHub Pages는 Settings → Pages → Source를 `main` / `(root)`로 지정하면 됩니다.
Vercel은 프로젝트 루트에 위 파일들이 그대로 있으면 별도 설정 없이 배포됩니다.

---

## ❓ 자주 묻는 질문

**Q. AI 기능이 작동하지 않아요.**
교사 대시보드에서 API 키가 `AIzaSy...`로 시작하는지, 앞뒤 공백은 없는지 확인해주세요.

**Q. 학생 로그인 화면에 반/모둠이 안 보여요.**
교사가 아직 반/모둠을 하나도 만들지 않은 상태입니다. 대시보드에서 먼저 추가해주세요.

**Q. 학생 활동 기록이 안 보여요.**
`students` 컬렉션에 최신 요약이, 각 앱의 전체 이력 컬렉션(`scienceMissions` 등)에 상세 기록이 쌓입니다. Firestore 콘솔에서 직접 확인할 수 있습니다.

---

© 2026 EAIM Studio · 박성애 선생님 제작
