# 📝 나의 기여 내역 — illiterate

> 프론트엔드 전반을 담당하였습니다. React + TypeScript 기반으로 전체 UI 구조 설계부터 페이지 개발, 컴포넌트 구성, 인증 플로우 구현까지 전담하였습니다.

---

## 🛠 기술 스택

`React` `TypeScript` `React Router v6` `Tailwind CSS`

---

## 📁 작업 내역

### 1. 전체 라우팅 설계 (App.tsx)
- React Router v6 기반 SPA 라우팅 구성
- Header / Footer를 Layout Route로 분리하여 공통 레이아웃 적용
- 메인 페이지(/)에서만 scroll overflow hidden 처리
- 전체 14개 라우트 구성

### 2. 페이지 개발

| 페이지 | 경로 | 설명 |
|---|---|---|
| 메인 | / | 서비스 소개 랜딩 페이지 |
| OCR 신청 | /application | 이미지 업로드 및 OCR 변환 신청 |
| OCR 결과 | /result | OCR 처리 결과 확인 페이지 |
| 내 문서 | /mydocument | 변환된 문서 목록 |
| 문서 상세 | /mydocument/detail/:ocrId | OCR 문서 상세 보기 |
| 문서 수정 | /mydocument/edit/:ocrId | 에디터 기반 문서 수정 |
| 고객센터 | /servicecenter | 공지 목록 |
| 공지 상세 | /servicecenter/detail/:boardIdx | 공지 내용 상세 |
| 서비스 안내 | /service | 서비스 이용 가이드 |
| 프로필 | /profile | 사용자 정보 수정 |
| 문서 타입 관리 | /documenttype | (관리자) OCR 지원 문서 타입 등록 |

### 3. 인증 플로우 구현 (/auth)
- 로그인 / 회원가입
- 계정 찾기 (FindAccount)
- 비밀번호 재설정 (ResetPassword, 토큰 기반)
- AccessToken 컴포넌트를 통한 토큰 예외 처리

### 4. 공통 컴포넌트
- Header.tsx — 네비게이션 포함 전체 헤더, 로그인 상태에 따른 UI 분기
- footer.tsx — 푸터 레이아웃
- Navigation — 카테고리별 네비게이션, 관리자 로그인 시 문서 타입 등록 버튼 활성화
- OCR — OCR API 연동 컴포넌트
- ImageUpload — 이미지 업로드 UI (화면 사이즈 반응형 대응)
- Logo — 서비스 로고 컴포넌트

### 5. 기타 작업
- Tailwind CSS 기반 전체 UI 스타일링
- 화면 사이즈별 레이아웃 조정 (반응형 대응)
- API 연동 실패 / 비정상 출력 등 전반적인 예외 처리
- 사용자 타입 정의 (types/)와 커스텀 훅 (hooks/) 구성

---

## 🚧 문제 상황과 해결

### 1. 라우팅 설계 개념 부족

**상황**
프로젝트 초반, 페이지마다 Header와 Footer를 각각 import해서 렌더링하는 구조로 작성했습니다.
화면이 늘어날수록 중복 코드가 쌓이고 유지보수가 어려워지는 문제가 발생했습니다.

**해결**
React Router v6의 Layout Route 개념을 학습하여, Header/Footer를 공통 부모 Route로 분리했습니다.
중첩 Route 구조로 리팩토링함으로써 코드 중복을 제거하고 전체 라우팅을 일관성 있게 관리할 수 있었습니다.

**배운 점**
단순히 동작하는 코드보다 구조적으로 확장 가능한 설계의 중요성을 체감했습니다.

---

### 2. 액세스 토큰 만료로 인한 백엔드 통신 실패

**상황**
로그인 후 일정 시간이 지나면 API 요청이 401 에러로 실패하는 문제가 발생했습니다.
매 요청마다 토큰 유효성을 수동으로 확인하는 방식은 비효율적이고 누락이 생길 수 있었습니다.

**해결**
AccessToken 컴포넌트를 별도로 만들어, 토큰 만료 시 자동으로 재발급 요청을 처리하는 구조를 구현했습니다.
공통 처리 레이어를 두어 각 페이지 컴포넌트에서는 토큰을 신경 쓰지 않아도 되도록 분리했습니다.

**배운 점**
인증 로직은 개별 컴포넌트가 아닌 공통 레이어에서 처리해야 한다는 것을 실무적으로 경험했습니다.
