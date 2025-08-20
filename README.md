# 숭실대학교 Flask Hello World

숭실대학교 로고를 참고하여 만든 Flask 기반 Hello World 웹 애플리케이션입니다.

## 특징

- 🎨 숭실대학교 로고 느낌을 살린 현대적인 디자인
- 🌊 애니메이션이 있는 로고 그래픽
- 📱 반응형 웹 디자인
- 🐍 Python Flask 프레임워크 사용
- 🐳 Docker 컨테이너 지원
- 🚀 GitHub Actions 자동 배포 (Docker Hub)

## 로컬 실행

### 1. 가상환경 생성 (권장)
```bash
python -m venv venv
venv\Scripts\activate  # Windows
# source venv/bin/activate  # macOS/Linux
```

### 2. 의존성 설치
```bash
pip install -r requirements.txt
```

### 3. 애플리케이션 실행
```bash
python app.py
```

### 4. 웹브라우저에서 확인
http://localhost:5000 으로 접속하여 결과를 확인하세요.

## Docker 실행

### 1. Docker 이미지 빌드
```bash
docker build -t ssu-flask-app .
```

### 2. Docker 컨테이너 실행
```bash
docker run -p 5000:5000 ssu-flask-app
```

### 3. Docker Compose 사용 (권장)
```bash
# 환경변수 설정
export DOCKER_USERNAME=your-username
docker-compose up
```

## 자동 배포

이 프로젝트는 GitHub Actions를 통해 Docker Hub에 이미지를 push하고, EC2 서버에서 pull하여 배포됩니다.

### 배포 트리거
- `main` 또는 `master` 브랜치에 push
- GitHub Actions에서 수동 실행

### 배포 과정

#### 1단계: 이미지 빌드 및 푸시
1. Docker 이미지 빌드
2. Docker Hub에 로그인
3. 이미지를 Docker Hub에 push
4. GitHub Actions 캐시 활용으로 빌드 속도 향상

#### 2단계: EC2 서버 배포
1. EC2 서버에 SSH 연결
2. 기존 컨테이너 중지 및 제거
3. Docker Hub에서 새 이미지 pull
4. 포트 80에서 애플리케이션 실행

### 설정

#### 워크플로우 환경변수
`.github/workflows/deploy.yml` 파일의 `env` 섹션에서 다음 값들을 설정할 수 있습니다:

```yaml
env:
  DOCKER_IMAGE: ssu-flask-app
  DOCKER_TAG: latest
  DOCKER_USERNAME: your-dockerhub-username  # Docker Hub 사용자명으로 변경
  SSH_USER: ssuuser
  SSH_PASSWORD: ssupassword20250820ec2user
  SERVER_IP: 3.35.69.129
```

#### GitHub Secrets 설정
Docker Hub 로그인을 위해서만 다음 시크릿이 필요합니다:

- `DOCKER_PASSWORD`: Docker Hub 액세스 토큰

### 배포 후 접속
배포가 완료되면 `http://3.35.69.129`에서 애플리케이션에 접속할 수 있습니다.

## 파일 구조

```
ssu-github-sample/
├── app.py                    # Flask 메인 애플리케이션
├── templates/                # HTML 템플릿
│   └── index.html           # 메인 페이지
├── requirements.txt          # Python 의존성
├── Dockerfile               # Docker 이미지 빌드
├── docker-compose.yml       # Docker Compose 설정
├── .dockerignore            # Docker 빌드 제외 파일
├── .github/workflows/       # GitHub Actions
│   └── deploy.yml           # 배포 워크플로우
└── README.md                # 프로젝트 설명
```

## 기술 스택

- **Backend**: Python Flask
- **Frontend**: HTML5, CSS3
- **Container**: Docker, Docker Compose
- **CI/CD**: GitHub Actions
- **Registry**: Docker Hub
- **Deployment**: SSH, EC2
- **Design**: 반응형 웹 디자인, CSS 애니메이션
