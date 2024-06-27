```bash
# 현재 git 상태
git status
# commit할 파일 입력
git add dags/file_name.py
# commit 메시지
git commit -m "comment"
# commit한 파일 push
git push
# docker 업로드
sudo docker compose up
```

## dags 경로 설정
- shell 창에 `vi docker-compose.yaml` 입력
	- `docker-compose.yaml` 수정
	- `volumes:` 에 해당하는 경로 수정
		- `${AIRFLOW_PROJ_DIR:-.}`: 현재 디렉토리
	- python dags 폴더로 경로수정
		- 이전: `${AIRFLOW_PROJ_DIR:-.}/dags:/opt/airflow/dags`
		- **수정**: `${AIRFLOW_PROJ_DIR:-.}/PycharmProjects/airflow/dags:/opt/airflow/dags`
	- `:wq!`: 저장 후 종료
	- 
```yaml
- ${AIRFLOW_PROJ_DIR:-.}/PycharmProjects/airflow/dags:/opt/airflow/dags
- ${AIRFLOW_PROJ_DIR:-.}/logs:/opt/airflow/logs
- ${AIRFLOW_PROJ_DIR:-.}/config:/opt/airflow/config
- ${AIRFLOW_PROJ_DIR:-.}/plugins:/opt/airflow/plugins
```

  
이 Docker Compose 파일의 `volumes` 섹션은 컨테이너와 호스트 간 파일 또는 디렉터리를 공유하기 위해 사용됩니다. 이 부분에서는 호스트의 파일 또는 디렉터리를 컨테이너의 특정 경로로 마운트하는 것을 정의하고 있습니다.

`${AIRFLOW_PROJ_DIR:-.}/PycharmProjects/airflow/dags:/opt/airflow/dags`

- `${AIRFLOW_PROJ_DIR:-.}`: 이는 환경 변수인 `AIRFLOW_PROJ_DIR`의 값을 가져오는 것을 시도합니다. 만약 해당 환경 변수가 설정되어 있지 않거나 비어있다면 (`:-` 뒤의 기본값인 `.`), 현재 디렉터리를 사용합니다.
- `/PycharmProjects/airflow/dags`: 이 부분은 호스트 시스템의 디렉터리 경로입니다. 여기서는 Pycharm에서 작업 중인 프로젝트의 Airflow DAG 파일이 위치한 경로입니다.
- `:`: 호스트와 컨테이너 경로를 구분하는 구분자입니다.
- `/opt/airflow/dags`: 이는 컨테이너 내부의 디렉터리 경로입니다. 호스트에서 마운트한 파일 또는 디렉터리가 이 위치에 들어갑니다. Airflow 컨테이너에서는 DAG 파일들이 보통 이 디렉터리에 저장됩니다.

따라서 이 설정은 호스트의 Pycharm에서 작업 중인 Airflow DAG 파일들을 Airflow 컨테이너의 `/opt/airflow/dags` 디렉터리에 마운트하여, 컨테이너 내에서 DAG 파일을 수정하거나 실행할 수 있도록 해줍니다.