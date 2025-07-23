# Jenkins CI/CD 설치 및 운영 가이드

## 1. 개요

Jenkins를 Docker로 실행하여 GitHub 저장소와 연동, Docker 이미지로 빌드 및 배포하는 방법을 안내합니다.

---

## 2. Ubuntu 환경

### 2.1 Docker 설치

```bash
# 기존 패키지 업데이트
sudo apt-get update

# 필수 패키지 설치
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

# Docker 공식 GPG 키 추가
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Docker 저장소 추가
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Docker 설치
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Docker 서비스 시작 및 활성화
sudo systemctl start docker
sudo systemctl enable docker

# Docker 버전 확인
docker --version
```

### 2.2 Docker 그룹 설정

```bash
sudo usermod -aG docker $USER
# 적용을 위해 로그아웃 후 재로그인
```

### 2.3 Jenkins Docker 컨테이너 실행

```bash
docker pull jenkins/jenkins:lts
docker run -d --name jenkins --restart=always -p 8080:8080 -p 50000:50000 -v /your/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts
```

---

## 3. Windows 환경

### 3.1 Docker Desktop 설치

- Docker 공식 홈페이지에서 Docker Desktop 다운로드 및 설치

### 3.2 Jenkins Docker 이미지 다운로드

```powershell
docker pull jenkins/jenkins:lts
```

### 3.3 Jenkins Docker 컨테이너 실행

```powershell
docker run -d --name jenkins --restart=always -p 8080:8080 -p 50000:50000 -v C:/Users/yourname/jenkins_home:/var/jenkins_home -v //var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts-jdk17
```

### 3.4 Docker 자동 실행 설정

- PowerShell에서 관리자 권한으로 다음 명령 실행:
```powershell
sc.exe create DockerEngine binPath= "C:\Program Files\Docker\Docker\resources\dockerd.exe" start= auto
```
- 또는 작업 스케줄러(Task Scheduler)에서 Docker Desktop 자동 실행 등록

---

## 4. Jenkins 접속 및 초기 설정

- 브라우저에서 `http://localhost:8080` 접속
- 초기 관리자 비밀번호 확인 및 플러그인 설치

---

> 이 문서는 Ubuntu와 Windows 환경에서 Jenkins CI/CD를 Docker로 손쉽게 구축할 수 있도록 정리되었습니다. 추가적인 설정이나 고급 사용법은 공식 문서를 참고하세요.
