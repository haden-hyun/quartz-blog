---
title: op_args 파라미터
created: 2024-09-08
tags:
  - airflow/python
  - airflow/python/operator/op_args
  - airflow/python/args
  - airflow/python/kwargs
  - airflow/python/operator/op_kwargs
---
> ![summary] 요약
> - airflow 내 args 결과는 `set`으로 반환


---
# 1. op_args 파라미터 이해

## 1) 함수에 일반 변수만 있는 경우
> 함수
```python
def regist(name, sex):
	print(f'이름은 {name}이고 성별은 {sex}입니다')
```
> Task
- `op_args`
	- 리스트로 작성됨
	- 해당 값이 함수 호출시 파라미터로 들어감
```python
python_task = PythonOperator(
		task_id = 'python_task',
		python_callable = regist,
		op_args = ['hyun','male']
)
```
## 2) 함수에 일반 변수 + args도 있는 경우
>함수
```python
def regist(name, sex, *args):
	print(name)
	print(sex)
	print(args)
```
> Task
```python
python_task = PythonOperator(
		task_id = 'python_task',
		python_callable = regist,
		op_args =  ['hyun','male', 'kr', 'seoul']
)
```
## 3) 함수에 args만 있는 경우
> 함수
```python
def regist(*args):
	print(args)
```
> Task
```python
python_task = PythonOperator(
		task_id = 'python_task',
		python_callable = regist,
		op_args = ['hjkim','male','kr','seoul']
)
```

---
# 2. op_kwargs로 변수 할당
- `op_kwargs`
	- 딕셔너리로 작성됨
	- 해당 값이 함수 호출시 파라미터로 들어감
	- key값에 해당하는 value값이 캡쳐됨
## 1) 함수에 일반 변수만 있는 경우
> 함수
```python
def regist(name, sex):
	print(f'이름은 {name}이고 성별은 {sex}입니다')
```

> Task
```python
python_task = PythonOperator(
		task_id = 'python_task',
		python_callable = regist,
		op_kwargs = {'name':'hyun', 'sex':'male'}
)
```
## 2) 함수에 일반 변수 + kwargs도 있는 경우
- key값이 명시되지 않는 arguments는 `kwargs`로 캡쳐됨
	- 딕셔너리 형태로 출력됨
> 함수
```python
def regist(name, sex, **kwargs):
	print(name)
	print(sex)
	print(kwargs)
```
> Task
```python
python_task = PythonOperator(
		task_id = 'python_task',
		python_callable = regist,
		op_kwargs = {'name':'hyun', 'sex':'male',
					'country':'kr','city':'seoul'}
)
```
## 3) 함수에 kwargs만 있는 경우
> 함수
```python
def regist(**kwargs):
	name = kwargs['name'] or ''
	sex = kwargs['sex'] or ''
	country = kwargs['country'] or ''
	city = kwargs['city'] or ''
```
> Task
```python
python_task = PythonOperator(
		task_id = 'python_task',
		python_callable = regist,
		op_kwargs = {'name':'hyun', 'sex':'male',
					'country':'kr','city':'seoul'}
)
```
## 4) 함수에 일반 변수 + args + kwargs 모두 있는 경우
- 명시된 변수는 해당 값이 캡쳐
- 그 외는 남은 `args` 값이 캡쳐
- 딕셔너리는 `kwargs`에 캡쳐¡
> 함수
```python
def regist(name, sex, *args, **kwargs):
```
> Task
```python
python_task = PythonOperator(
		task_id = 'python_task',
		python_callable = regist,
		op_args = ['hyun','male','kr','seoul']
		op_kwargs = {'phone': 010, 'mail':'hyun@naver.com'}
)
```
