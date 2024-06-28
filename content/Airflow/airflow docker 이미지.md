---
title: airflow docker 이미지
created: 2024-05-08
modified: 2024-05-08 00:41
cssclasses:
  - max
tags:
  - airflow
  - airflow/docker
  - docker/image
---
[youtube](https://www.youtube.com/watch?v=0UepvC9X4HY)
[사이트](https://heekng.tistory.com/117)

`docker build --tag [태그명]:[tag] .`
> [!hint] 목적
> **Airflow 내 특정 python 패키지 설치**
## 이미지란?(작성필요)

## 1. requirements.txt 생성
- 프로젝트 파일에서 생성
- 설치할 패키지 버전 목록 작성
```txt file:requirements.txt
mojito2==0.1.6
PyJWT==2.1.0
```

## 2. Dockerfile 생성
- 프로젝트 파일에서 `Dockerfile` 생성
- 로컬의 requirements.txt을 docker 이미지로 복사
- 여기서 `apache/airflow:2.9.1`는 기존 image 이름
```docker file:Dockerfile
FROM apache/airflow:2.9.1
COPY requirements.txt /requirements.txt
RUN pip install --upgrade pip
RUN pip install -r /requirements.txt
```

## 3. 이미지 생성
- 새롭게 적용할 이미지를 생성
- 이때, Dockerfile을 참고함
- 여기서 `extending-airflow:latest`는 새롭게 생성할 이미지 이름
	- Name: `extending-airflow`
	- Tag : `latest`
- **단, 기존 이미지를 계속 사용할 경우 기존 이미지 이름 설정하여 빌드**
```bash file:도커파일빌드
docker build --tag extending-airflow:latest
```
- docker desktop 내 Images
![[도커 파일 빌드.png]]

#### 4. docker-compose.yaml 수정
- `apache/airflow:2.9.1` -> `extending-airflow:latest`
- 단, 기존 이미지를 사용할 경우에는 수정 안해도 됨
![[Pasted image 20240508013912.png]]

#### 5. docker compose up
