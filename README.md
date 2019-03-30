
# 개발환경 설정
## MYSQL
```sh
docker-compose -f dev-mysql.yml up -d
```
## MONGO
```sh
docker-compose -f dev-mongo.yml up -d
```
## node
```sh
npm install && npm run watch
```

# 배포
## Dockerizing
```sh
docker build -t first_node_app:version .
```
## Docker-compose
```yaml
version: '3.7'
services:
  mysql:
    networks:
      - app
    ports:
      - "3306:3306"
    image: mysql:5.7
    volumes:
      - ./db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: your_password
      MYSQL_DATABASE: your_database
      MYSQL_USER: your_user
      MYSQL_PASSWORD: your_passoword
  app:
    networks:
      - app
    depends_on:
      - mysql
    image: first_node_app:version
    ports:
      - "80:3000"
    restart: always
    environment:
      MYSQL_HOST: mysql
networks:
  app:
```