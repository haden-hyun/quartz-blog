---
title: airflow 세팅
created: 2024-04-16
modified: 2024-04-16 22:43
cssclasses:
  - max
tags:
  - airflow
  - airflow/설정
  - airflow/설치
  - airflow/docker-compose
  - airflow/docker
  - docker
  - docker/docker-compose
---
> [!hint] 요약
> - MAC에 Docker Desktop 설치
> 	- 하위 폴더들 생성
> - docker-compose 설치
> - python 내 apache-airflow 설치

# 1. docker 설치

### 1) docker desktop으로 설치

[참고사이트](https://velog.io/@eunhye_/Docker-Mac-OS%EC%97%90-Docker-%EC%84%A4%EC%B9%98)

- 도커 데스크탑 설치[Docker  rDesktop](https://docs.docker.com/desktop/install/mac-install/) 
- 설치 확인
- 
```bash
docker
docker --version
```

###### 2) brew로 설치
- `brew install cask docker`
	- **도커 사전지식 없는 경우 추천**
	- Docker Desktop on Mac 설치
	- docker-compose, docker-machine 설치
	- 포트포워딩 불필요
- `brew install docker`
	- 가상머신 위 도커 띄우는 작업 필요
	- docker-compose, docker-machine 추가 설치 필요
	- 포트포워딩 필요

```bash
brew install cask docker

brew install docker
```

# 2. docker-compose
[참고사이트1](https://devinventory.tistory.com/19) : Docker Desktop 설치시, 기본적으로 docker-compose 설치됨
[참고사이트2](https://wooiljeong.github.io/server/docker-airflow/): **Airflow 공식 문서 내용 정리**

# 3. apache-airflow
- [공식사이트](https://airflow.apache.org/docs/apache-airflow/stable/installation/installing-from-pypi.html) 에서 python library  설치
- 20240506 기준
	- **단, vscode에서 꼭 가상환경(venv) 환경에서 설치하는 거 추천**
	- `Successfully installed` 뜨면 성공!

```bash file:python_airflow
pip install "apache-airflow[celery]==2.9.1" --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.9.1/constraints-3.8.txt"
```


- python 내 `apache-airflow` 설치

### 0) 환경 초기화
> [!warning] 
> 문제 발생 시, 다 지우고 처음부터 다시 시작하는 것을 권장함
> 아래 코드를 통해 다 지우고, 처음부터 재실행


```bash file:환경초기화
# docker-compose.yaml 파일이 있는 경로에서 다음 실행
docker-compose down --volumes --remove-orphans

# docker-compose.yaml 파일 위치한 경로 제거
rm -rf <DIRECTORY>
```

### 1) docker-compose.yaml 다운로드
- airflow 폴더 생성
- 생성한 폴더에 [airflow 사이트](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html) 내 `docker-compose.yaml` 다운로드
- 2024/05/06 기준

```bash file:docker-compose.yaml
mkdir airflow
cd airflow

curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.9.1/docker-compose.yaml'
```

### 2) 초기 설정
- airflow 폴더에 하위폴더 4개 생성(dags, logs, plugins, config)
- 호스트, 컨테이터 파일 권한 설정
	- `.env` 파일 생성
		- `vi .env`로 파일 확인
		- `q`: 현재 세팅된 내 os계정의 UID 가 501
- DB 마이그레이션과 계정 생성
- airflow 서비스 설치
	- `sudo` 입력하여 실행
	- `exited with code 0`: 제대로 설치 완료
	- 최초 계정
		- ID: `airflow`
		- PW: `airflow`

```bash file:airflow설치
pip install apache-airflow

cd airflow
mkdir -p ./dags ./logs ./plugins ./config

# 호스트, 컨테이너 파일 권한 설정
echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env

# DB 마이그레이션과 계정 생성
sudo docker compose up airflow-init
```

### 3) Airflow 실행
- airflow 올리기
	- `-d`: 백그라운드로 실행
	- `sudo`로 실행
- 아래와 같이 계속 실행중인 상황은 **정상!**
	- airflow가 기본적으로 health 체크를 기록
	- 따라서, 2번째 terminal 생성
	- **이때, 기존 터미널 종료시 서비스 내려가므로 꼭 새로운 터미널 열기**
- airflow를 띄우는데 필요한 컨테이너 목록 확인
	- `docker ps`
	- 6개 항목과 필요한 IMAGE 확인 가능2

```bash file:airflow실행
# airflow 올리기
docker compose up -d

# 컨테이너 목록 확인
docker ps
```

### 4) Airflow 계정 및 패스워드 변경

> [!summary] 사이트 내에서 수정
> - Edit User 에서 이름 변경
> - Reset Password에서 비밀번호 변경

- 위에서 생성한 `.env` 파일에 아래 2개 변수 추가
	- `_AIRFLOW_WWW_USER_USERNAME=계정명`
	- `_AIRFLOW_WWW_USER_PASSWORD=패스워드`