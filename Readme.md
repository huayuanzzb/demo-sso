# 配置 keycloak
#### 通过 docker 安装 keycloak, 并使用数据库存储数据
```bash
net_name=demo-sso

docker network create ${net_name}

docker run -d --name postgres --net ${net_name} -e POSTGRES_DB=keycloak -e POSTGRES_USER=keycloak -e POSTGRES_PASSWORD=password postgres

docker run -d -p 8180:8080 --name keycloak --net ${net_name} -e DB_USER=keycloak -e DB_PASSWORD=password -e KEYCLOAK_USER=admin -e KEYCLOAK_PASSWORD=admin -e DB_VENDOR=postgres -e DB_ADDR=postgres -e DB_PORT=5432 jboss/keycloak:16.1.1
```
#### 通过 User Storage SPI 配置 keycloak 读取外部的用户
