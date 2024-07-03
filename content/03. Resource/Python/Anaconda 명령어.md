---
title: Python Anaconda
created: 2022-12-23
modified: 2022-12-23 19:50
tags:
  - python
  - anaconda
  - 설치
  - 세팅
  - python/anaconda
  - python/아나콘다
---

## 설정

기본적으로 맥은 `zsh` 쉘 이용하므로 환경변수 설정이 필요
- 여기서 쉘(Shell)이란?
	- 커널과 사용자간의 다리역할을 하는 것
	- 사용자로부터 명령을 받아 그것을 해석하고 프로그램을 실행하는 역항

1. Terminal 창 열기
- anacoda가 설치된 폴더에 환경변수 설정
```shell
export PATH="/Users/haejun/opt/anaconda3/bin:$PATH"
```

## 자주쓰는 커맨드

### 1. 목록 확인
- `conda list` : 설치된 모든 라이브러리 목록 확인
- `conda env list` : 존재하는 작업환경 목록 확인
- `conda --version` : 아나콘다 버전 확인
- `python --version` : 파이썬 버전 확인

### 2. 작업환경
가상환경을 설정해서 작업을 진행함
Why? 
- 독립적인 작업환경에서 작업할 수 있음
- 프로젝트 진행시 여러 라이브러리, 패키지 다운로드 하는데 각 라이브러리들이 충돌을 일으킴

- `conda create -n env_name python=version` : 새로운 작업환경 이름(*env_name*)을 생성하고 해당 환경의 파이썬 버전도 임의 설정 가능
- `conda env remove -n env_name` : 작업환경 삭제
- `conda activate env_name` : 특정 작업환경(*env_name*)으로 설정
- `conda deactivate` : 현재 작업환경에서 나가기

### 3. 라이브러리 설치
1. (base)에서 설치할 수도 있음
2. 특정 작업환경에 들어가서 라이브러리 설치할 수도 있음
- `conda install numpy pandas` :  해당 작업환경에 *numpy*, *pandas* 설치
- `conda uninstall numpy` : 해당 작업환경에서 *numpy* 삭제