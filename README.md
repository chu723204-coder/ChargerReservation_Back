# ⚡ ChargeNow - 전기차 충전소 예약 관리 시스템

**전기차 충전소 예약부터 관리자 시스템까지 통합 관리하는 풀스택 웹 플랫폼**

> 7인 팀 프로젝트 | 담당: 관리자 페이지 백엔드 + 프론트엔드 전담 개발

---

## 🛠 Tech Stack

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

## 📌 프로젝트 개요

전기차 보급 확대에 따른 충전 인프라 관리의 필요성을 배경으로,
사용자가 충전소를 예약하고 관리자가 전체 시스템을 효율적으로 운영할 수 있는
통합 플랫폼을 개발했습니다.

---

## 👤 담당 파트 - 관리자 페이지 전담 개발

### 🔐 JWT + RBAC 권한 체계 설계
- 일반 사용자와 관리자 인증 프로세스 분리
- **SUPER / MANAGER** 역할 기반 접근 제어(RBAC) 구현
- 파트별 접근 권한 세분화 (회원 / 충전기 / 예약 / 패널티 / 문의)
- 불필요한 데이터 접근 차단으로 보안성 확보

### 👥 관리자 등록/해제 로직
- 관리자 등록/해제 시 MEMBER_GRADE 자동 변경 처리
- 등록/해제와 등급 변경을 하나의 **@Transactional**로 묶어 데이터 일관성 확보
- **본인 해제 불가** 예외처리 구현 (운영 환경 고려 로직)

### 📊 관리자 기능 구현 (8개 파트)
| 파트 | 주요 기능 |
|------|----------|
| 회원 관리 | 회원 조회 / 정지 / 해제 / 탈퇴 처리 |
| 충전기 관리 | 충전기 등록 / 상태 변경 / 삭제 |
| 예약 관리 | 예약 현황 조회 / 강제 취소 처리 |
| 패널티 관리 | 패널티 부여 / 해제 / 이력 조회 |
| 공지사항 관리 | 공지 등록 / 수정 / 삭제 |
| 문의 관리 | 1:1 문의 답변 처리 |
| 대시보드 | 실시간 통계 조회 |
| 관리자 계정 | 관리자 등록 / 해제 |

### 🗄 데이터베이스 설계
- Oracle DB 기반 직접 Entity 설계
- 시퀀스를 활용한 기본키 자동 증가 처리
- 권한 체계를 DB 레벨에서도 반영 (MEMBER_GRADE 컬럼)

### 🖥 프론트엔드 연동
- React + TypeScript 기반 관리자 UI 구현
- 백엔드 API와 직접 연동하여 전체 플로우 완성

---

## 🤝 팀 협업 규칙

- `main` / `dev` 브랜치 직접 Push 금지
- 개인 브랜치 `dev-이니셜` 형식으로 작업
- 모든 PR은 최소 1명 이상 리뷰 후 머지
- 공통 컴포넌트 수정 시 팀원 사전 공유

---

## 🤖 AI 활용 원칙

- AI 도구 적극 활용 (ChatGPT, Claude 등)
- AI가 제시한 코드는 로직 흐름과 함수별 역할을 직접 이해한 뒤 적용
- 여러 AI 교차 검증 + 공식 문서 확인 후 적용하는 방식 유지
