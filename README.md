# ⚡ ChargeNow - 전기차 충전소 예약 관리 시스템 (Backend)

> 사용자 중심의 스마트 전기차 충전 솔루션 - 백엔드 서버

[![Frontend Repo](https://img.shields.io/badge/Frontend-Repository-blue?style=for-the-badge)](https://github.com/chu723204-coder/ChargerReservation_Front)

---

## 📌 1. 프로젝트 소개

전기차 충전기 보급은 늘었지만 사용자 경험은 제자리걸음인 문제를 해결하기 위해 기획된 프로젝트입니다.

**해결하려는 문제**
- **정보 불일치**: 앱 정보와 실제 충전소 상태의 차이
- **복잡한 절차**: 탐색부터 예약까지 번거로운 유저 플로우
- **관리 부재**: 충전기 고장 및 점유 상태 확인의 어려움

이를 해결하기 위해 실시간 충전소 탐색, 예약, 관리자 시스템을 통합한 플랫폼을 개발했습니다.

---

## 🗓 2. 프로젝트 정보

| 항목 | 내용 |
|------|------|
| 개발 기간 | 2026.04 (약 1개월) |
| 팀 규모 | 7인 팀 프로젝트 |
| 담당 역할 | 관리자 페이지 백엔드 + 프론트엔드 전담 개발 |

---

## 🛠 3. 기술 스택

### Backend
![Spring Boot](https://img.shields.io/badge/springboot-3.x-%236DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/spring%20security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white)
![JPA/Hibernate](https://img.shields.io/badge/jpa-hibernate-59666C?style=for-the-badge&logo=hibernate&logoColor=white)
![Oracle DB](https://img.shields.io/badge/oracle%20db-F80000?style=for-the-badge&logo=oracle&logoColor=white)
![JWT](https://img.shields.io/badge/jwt-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)

### Frontend
![React](https://img.shields.io/badge/react-19-%2361DAFB?style=for-the-badge&logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/typescript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/tailwindcss-v4-%2306B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Zustand](https://img.shields.io/badge/zustand-pink?style=for-the-badge&logo=react&logoColor=white)
![Axios](https://img.shields.io/badge/axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white)

### Tools
![IntelliJ IDEA](https://img.shields.io/badge/IntelliJ_IDEA-000000.svg?style=for-the-badge&logo=intellij-idea&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)

---

## ⚙️ 4. 주요 기능

### 사용자 기능
| 기능 | 설명 |
|------|------|
| 로그인/회원가입 | 이메일 인증 / 카카오·네이버 소셜 로그인 |
| 충전소 찾기 | 위치 기반 충전소 탐색 / 실시간 현황 확인 |
| 충전소 예약 | 시간대 선택 / 예약 확정 / PIN 발급 |
| 마이페이지 | 예약 내역 / 충전 이력 / 개인정보 수정 |
| 고객센터 | FAQ / 1:1 문의 접수 |
| 공지사항 | 중요 공지 / 일반 공지 구분 |

### 관리자 기능 (담당 파트)
| 기능 | 설명 |
|------|------|
| 대시보드 | 실시간 통계 및 현황 조회 |
| 회원 관리 | 회원 조회 / 정지 / 해제 / 탈퇴 처리 |
| 충전기 관리 | 충전기 등록 / 상태 변경 / 삭제 |
| 예약 관리 | 예약 현황 조회 / 강제 취소 처리 |
| 패널티 관리 | 패널티 부여 / 해제 / 이력 조회 |
| 공지사항 관리 | 공지 등록 / 수정 / 삭제 |
| 문의 관리 | 1:1 문의 답변 처리 |
| 관리자 계정 | 관리자 등록 / 해제 |

---

## 🗄 5. 시스템 구조

### 데이터 흐름
```
클라이언트 요청
    → Spring Security Filter (JWT 검증)
    → Controller
    → Service
    → Repository
    → Oracle DB
    → 응답
```

### API 문서
Swagger UI를 통해 전체 API 문서화 및 테스트 완료

---

## 🔍 6. 핵심 구현 내용

### JWT + RBAC 권한 체계 설계

**왜 이렇게 설계했는가?**

관리자 시스템에서 모든 관리자가 동일한 권한을 갖는 것은 보안상 위험하다고 판단했습니다. 각 관리자가 담당 파트의 데이터에만 접근할 수 있도록 역할 기반 접근 제어(RBAC)를 설계했습니다.

| 역할 | 접근 범위 |
|------|----------|
| SUPER | 시스템 전체 관리 권한 |
| MANAGER | 담당 파트만 접근 가능 |

- 일반 사용자와 관리자 인증 프로세스 분리
- 파트별 접근 권한 세분화 (회원 / 충전기 / 예약 / 패널티 / 문의)
- 불필요한 데이터 접근 차단으로 보안성 확보

---

### 관리자 등록/해제 트랜잭션 처리

관리자 등록/해제 시 MEMBER_GRADE 변경이 함께 이루어져야 데이터 일관성이 유지됩니다.

- 등록/해제와 등급 변경을 하나의 `@Transactional`로 묶어 처리
- 중간에 오류 발생 시 전체 롤백으로 데이터 정합성 확보
- **본인 해제 불가** 예외처리 구현 (운영 환경 고려 로직)

---

## 🔧 7. 트러블슈팅

### ① CORS 오류
- **문제**: 프론트엔드에서 백엔드 API 요청 시 CORS 오류 발생
- **원인**: Spring Boot에서 CORS 설정이 되어있지 않았음
- **해결**: `@CrossOrigin` 설정 추가로 해결

### ② JWT 권한 체계 설계
- **문제**: SUPER / MANAGER 권한에 따라 API 접근을 제한해야 했음
- **원인**: Spring Security에서 역할 기반 접근 제어 설정 필요
- **해결**: SecurityConfig에서 경로별 권한 설정 + JWT 필터에서 권한 추출

### ③ 본인 해제 불가 예외처리
- **문제**: 관리자가 실수로 자기 자신을 해제하는 경우 방지 필요
- **원인**: 운영 환경에서 모든 관리자가 사라지는 상황 방지 필요
- **해결**: 현재 로그인한 관리자 ID와 해제 대상 ID 비교 후 동일 시 예외 처리

---

## 👤 8. 본인 기여

7인 팀 프로젝트에서 관리자 페이지 백엔드를 전담 개발했습니다.

- JWT + Spring Security 기반 인증/인가 체계 설계 및 구현
- SUPER / MANAGER RBAC 권한 체계 설계
- 관리자 등록/해제 시 MEMBER_GRADE 자동 변경 처리
- 본인 해제 불가 운영 예외처리 구현
- 회원/충전기/예약/패널티/공지사항/문의/대시보드 8개 파트 API 구현
- Oracle DB Entity 및 시퀀스 설계
- React + TypeScript 관리자 UI 연동

---

## 🤝 9. 협업 방식

- `main` / `dev` 브랜치 직접 Push 금지
- 개인 브랜치 `dev-이니셜` 형식으로 작업
- 모든 PR은 최소 1명 이상 리뷰 후 머지
- 공통 컴포넌트 수정 시 팀원 사전 공유
- 매일 GitHub 병합으로 충돌 최소화

---

## 🤖 AI 활용 원칙

- AI 도구 적극 활용 (ChatGPT, Claude 등)
- AI가 제시한 코드는 로직 흐름과 함수별 역할을 직접 이해한 뒤 적용
- 여러 AI 교차 검증 + 공식 문서 확인 후 적용하는 방식 유지

---

## 💬 10. 회고

### 잘된 점
- 7인 팀 프로젝트에서 관리자 페이지 전체를 혼자 완성
- RBAC 권한 체계를 처음 설계하고 직접 구현
- 운영 환경을 고려한 예외처리 로직 직접 설계
- 팀원들과 매일 GitHub 병합하며 충돌 최소화

### 아쉬운 점
- 배포 환경 구성 경험 부족
- QueryDSL 도입으로 복잡한 통계 쿼리 최적화 필요
- 테스트 코드 부재

### 향후 계획
- 배포 환경 구성 학습
- QueryDSL 적용으로 대시보드 통계 쿼리 최적화
- 단위 테스트 도입
