BASE_VOLUME=
OP_DB_DATA_VOLUME=${BASE_VOLUME}/db
OP_APP_DATA_VOLUME=${BASE_VOLUME}/openproject
OP_DB_HOST=host.docker.internal
OP_DB_PORT=
OP_DB_NAME=openproject
OP_DB_USER=openproject
OP_DB_PWD=
OP_APP_PORT=
OP_SECRET_KEY_BASE=


up:
	DB_DATA_VOLUME=${OP_DB_DATA_VOLUME} \
	DB_NAME=${OP_DB_NAME} \
	DB_USER=${OP_DB_USER} \
	DB_PWD=${OP_DB_PWD} \
	APP_DATA_VOLUME=${OP_APP_DATA_VOLUME} \
	APP_PORT=${OP_APP_PORT} \
	SECRET_KEY_BASE=${OP_SECRET_KEY_BASE} \
	docker-compose up

down:
	DB_DATA_VOLUME=${OP_DB_DATA_VOLUME} \
	DB_NAME=${OP_DB_NAME} \
	DB_USER=${OP_DB_USER} \
	DB_PWD=${OP_DB_PWD} \
	APP_DATA_VOLUME=${OP_APP_DATA_VOLUME} \
	APP_PORT=${OP_APP_PORT} \
	SECRET_KEY_BASE=${OP_SECRET_KEY_BASE} \
	docker-compose down

docker_db:
	docker run -it \
		--name op_postgres10 \
		-v ${OP_DB_VOLUME}:/var/lib/postgresql/data \
		-p ${OP_DB_PORT}:5432 \
		-e POSTGRES_DB=${OP_DB_NAME} \
		-e POSTGRES_USER=${OP_DB_USER} \
		-e POSTGRES_PASSWORD=${OP_DB_PWD} \
		postgres:10

docker_op:
	docker run -it \
		--name openproject10 \
		-v ${OP_DATA_VOLUME}:/var/openproject/assets \
		-p ${OP_APP_PORT}:80 \
		-e SECRET_KEY_BASE=${OP_SECRET_KEY_BASE} \
		-e DATABASE_URL=postgres://${OP_DB_USER}:${OP_DB_PWD}@${OP_DB_HOST}:${OP_DB_PORT}/${OP_DB_NAME} \
		openproject/community:10

