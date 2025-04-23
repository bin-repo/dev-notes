# docker-compose

## instructions

```sh
# compose.yaml
docker compose up -d --build
docker compose stop
docker compose down # 清相关容器和镜像，保留卷
docker compose down --volumes # 同时清相关卷
docker compose logs
docker compose ps
docker compose watch
docker compose up --watch
```
