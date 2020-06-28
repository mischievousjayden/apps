PG_VERSION=10
OP_VERSION=10

BASE_VOLUME=
OP_DB_VOLUME=${BASE_VOLUME}/db
OP_APP_VOLUME=${BASE_VOLUME}/app

OP_DB_HOST=host.docker.internal
OP_DB_PORT=
OP_DB_NAME=openproject
OP_DB_USER=openproject
OP_DB_PWD=
OP_APP_PORT=
OP_SECRET_KEY_BASE=


cluster_up:
	POSTGRES_VERSION=${PG_VERSION} \
	OPENPROJECT_VERSION=${OP_VERSION} \
	DB_VOLUME=${OP_DB_VOLUME} \
	DB_NAME=${OP_DB_NAME} \
	DB_USER=${OP_DB_USER} \
	DB_PWD=${OP_DB_PWD} \
	APP_VOLUME=${OP_APP_VOLUME} \
	APP_PORT=${OP_APP_PORT} \
	SECRET_KEY_BASE=${OP_SECRET_KEY_BASE} \
	docker-compose up -d

cluster_down:
	POSTGRES_VERSION=${PG_VERSION} \
	OPENPROJECT_VERSION=${OP_VERSION} \
	DB_VOLUME=${OP_DB_VOLUME} \
	DB_NAME=${OP_DB_NAME} \
	DB_USER=${OP_DB_USER} \
	DB_PWD=${OP_DB_PWD} \
	APP_VOLUME=${OP_APP_VOLUME} \
	APP_PORT=${OP_APP_PORT} \
	SECRET_KEY_BASE=${OP_SECRET_KEY_BASE} \
	docker-compose down

run_db:
	docker run --rm -it \
		--name openproject_db \
		-v ${OP_DB_VOLUME}:/var/lib/postgresql/data \
		-p ${OP_DB_PORT}:5432 \
		-e POSTGRES_DB=${OP_DB_NAME} \
		-e POSTGRES_USER=${OP_DB_USER} \
		-e POSTGRES_PASSWORD=${OP_DB_PWD} \
		postgres:${PG_VERSION}

run_app:
	docker run --rm -it \
		--name openproject_app \
		-v ${OP_DATA_VOLUME}:/var/openproject/assets \
		-p ${OP_APP_PORT}:80 \
		-e SECRET_KEY_BASE=${OP_SECRET_KEY_BASE} \
		-e DATABASE_URL=postgres://${OP_DB_USER}:${OP_DB_PWD}@${OP_DB_HOST}:${OP_DB_PORT}/${OP_DB_NAME} \
		openproject/community:${OP_VERSION}

