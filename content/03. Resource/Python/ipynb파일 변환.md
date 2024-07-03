---
title: ipynb파일 변환
created: 2023-01-15
modified: 2023-01-15 17:13
tags: python, ipynb, python/파일변환
---
## .ipynb 파일 txt로 변환

### 1. 패키지 설치
```terminal
conda install nbconvert
```

### 2. 파일 변환
- terminal 경로 확인 : `pwd`
- 경로 안에 `.ipynb`파일을 `txt`파일로 변환
```terminal 
jupyter nbconvert --to script file_name.ipynb
```
- 아래와 같은 문구 뜨면 변환 성공
```terminal 
[NbConvertApp] Converting notebook lec1.ipynb to script
[NbConvertApp] Writing 14802 bytes to file_name.txt
```
