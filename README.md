# goMicroServices

Based on: https://levelup.gitconnected.com/microservices-with-go-grpc-api-gateway-and-authentication-part-1-2-393ad9fc9d30

```bash
docker-compose up
docker exec -it gomicroservice_database_1 /bin/sh
psql --host=gomicroservice_database_1 --username=superuser --dbname=micro_service_db

CREATE DATABASE auth_svc;
CREATE DATABASE order_svc;
CREATE DATABASE product_svc;
\l
\q

// use database: auth_svc.
\c auth_svc

// show tables from current db.
\d

// describe table: users.
\d users;

// select * from users;

// from each path containing .proto files.
protoc *.proto -I. --go_out=.

// from goMicroService\go-grpc-api-gateway
go run cmd/main.go

//  from goMicroService\go-grpc-auth-svc
go run cmd/main.go
go run cmd/main.go

// Register new user.
// linux curl version:
curl --request POST --url "http://localhost:3000/auth/register" --header "Content-Type: application/json" --data "{"email": "elon@musk.com","password": "1234567"}"

// windows curl version:
curl --request POST --url "http://localhost:3000/auth/register" --header "Content-Type: application/json" --data "{\"email\":\"elon@musk.com\",\"password\":\"1234567\"}"

// Login user.
// windows curl version:
curl --request POST --url "http://localhost:3000/auth/login" --header "Content-Type: application/json" --data "{\"email\": \"elon@musk.com\",\"password\": \"1234567\"}"
```
