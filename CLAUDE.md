# CLAUDE.md

이 파일은 이 저장소에서 작업할 때 Claude Code (claude.ai/code)에게 가이드를 제공합니다.

## 프로젝트 개요

Dolpha는 세 가지 주요 구성 요소로 이루어진 주식 거래 애플리케이션입니다:
- **Frontend**: Material-UI 프레임워크를 사용한 React 애플리케이션
- **Backend**: MySQL 데이터베이스를 사용한 Django REST API
- **Autobot**: 주식 데이터 관리 및 자동 거래를 위한 FastAPI 서비스

## 아키텍처

### Frontend (React)
- Creative Tim의 Material Kit 2 React 템플릿을 기반으로 구축
- 네비게이션에 React Router, 금융 데이터 시각화에 Chart.js 사용
- JWT 토큰을 사용한 Google OAuth 인증 구현
- 주요 디렉터리:
  - `src/pages/`: 주요 애플리케이션 페이지 (Presentation, MyPage, SignIn)
  - `src/components/`: 재사용 가능한 UI 컴포넌트
  - `src/contexts/`: 상태 관리를 위한 React 컨텍스트
  - `src/hooks/`: 비즈니스 로직을 위한 커스텀 React 훅

### Backend (Django)
- Simple JWT 인증을 사용한 Django REST Framework
- 커스텀 User 모델(`myweb.User`)을 사용한 MySQL 데이터베이스
- 백그라운드 작업을 위한 APScheduler
- React 프론트엔드와의 통신을 위한 CORS 활성화
- 주요 모듈:
  - `dolpha/api.py`: Django Ninja를 사용한 주요 API 엔드포인트
  - `myweb/models.py`: 데이터베이스 모델
  - `dolpha/settings.py`: 환경별 데이터베이스 설정이 포함된 구성

### Autobot (FastAPI)
- 주식 관리 및 자동 거래를 위한 FastAPI 서비스
- 주식 정보 및 자동 거래 구성 관리
- 데이터 지속성을 위한 로컬 JSON 파일 사용
- 프론트엔드 통합을 위한 CORS 활성화

## 개발 명령어

### Frontend
```bash
cd frontend
npm install              # 의존성 설치
npm start               # 개발 서버 시작 (http://localhost:3000)
npm run build           # 프로덕션 빌드
npm test                # 테스트 실행
npm run lint            # ESLint 실행
npm run prettify        # Prettier로 코드 포맷팅
```

### Backend
```bash
cd backend
pip install -r requirements.txt    # 의존성 설치
python manage.py makemigrations    # 데이터베이스 마이그레이션 생성
python manage.py migrate           # 마이그레이션 적용
python manage.py runserver         # 개발 서버 시작 (http://localhost:8000)
```

### Autobot
```bash
cd autobot
pip install -r requirements.txt    # 의존성 설치
python main.py                     # FastAPI 서버 시작
# 또는
uvicorn main:app --reload          # 자동 리로드로 시작
```

## 데이터베이스 구성

백엔드는 환경별 설정을 가진 MySQL을 사용합니다:
- **개발 환경 (Windows/macOS)**: 218.152.32.218의 원격 MySQL 서버에 연결
- **프로덕션 환경 (Ubuntu/Docker)**: 로컬 MariaDB 컨테이너에 연결
- 데이터베이스 이름: `dolpha_db`
- 커스텀 사용자 모델: `myweb.User`

## 인증

- 사용자 인증을 위한 Google OAuth2 통합
- Simple JWT 라이브러리로 관리되는 JWT 토큰
- React 컨텍스트에 인증 상태 저장
- 프론트엔드와 백엔드 간 크로스 오리진 요청을 위한 CORS 구성

## 주요 기능

- 주식 포트폴리오 관리 및 시각화
- 터틀 트레이딩 전략을 사용한 자동 거래 구성
- 실시간 금융 데이터 통합
- 사용자 프로필 및 서버 설정 관리
- 반응형 Material-UI 디자인

## 파일 구조 참고사항

- `privateFiles/`: 민감한 구성 파일 포함 (버전 관리에서 제외)
- `frontend/build/`: 프로덕션 빌드 출력
- `backend/cookies.txt`: 세션 지속성 파일
- 백엔드와 autobot 모두 별도의 `requirements.txt` 파일을 가지고 있음