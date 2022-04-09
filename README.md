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
protoc --go_out=. --go-grpc_out=. *.proto

// from goMicroService\go-grpc-api-gateway
go run cmd/main.go

//  from goMicroService\go-grpc-auth-svc
go run cmd/main.go

//  from goMicroService\go-grpc-product-svc
go run cmd/main.go

//  from goMicroService\go-grpc-order-svc
go run cmd/main.go

// Register New User.
// linux curl version:
curl --request POST --url "http://localhost:3000/auth/register" --header "Content-Type: application/json" --data "{"email": "elon@musk.com","password": "1234567"}"

// Register New User.
// windows curl version:
curl --request POST --url "http://localhost:3000/auth/register" --header "Content-Type: application/json" --data "{\"email\":\"elon@musk.com\",\"password\":\"1234567\"}"

// Login User.
// windows curl version:
curl --request POST --url "http://localhost:3000/auth/login" --header "Content-Type: application/json" --data "{\"email\": \"elon@musk.com\",\"password\": \"1234567\"}"

// Create Product (replace bearer token with response from login user).
curl --location --request POST "http://localhost:3000/product" --header "Content-Type: application/json" --header "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2ODEwNzIwMTksImlzcyI6ImdvLWdycGMtYXV0aC1zdmMiLCJJZCI6MSwiRW1haWwiOiJlbG9uQG11c2suY29tIn0.2QNf4rh2gTm9bYkouzChLmsbdCek1HUYxF6_GcIlskE" --data "{\"name\": \"Product A\",\"stock\": 6,\"price\": 15}"

// Find Product (replace bearer token with response from login user).
curl --request GET --url http://localhost:3000/product/1 --header "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2ODEwNzIwMTksImlzcyI6ImdvLWdycGMtYXV0aC1zdmMiLCJJZCI6MSwiRW1haWwiOiJlbG9uQG11c2suY29tIn0.2QNf4rh2gTm9bYkouzChLmsbdCek1HUYxF6_GcIlskE"

// Create Order (replace bearer token with response from login user).
curl --location --request POST --url "http://localhost:3000/order" --header "Content-Type: application/json" --header "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2ODEwNzIwMTksImlzcyI6ImdvLWdycGMtYXV0aC1zdmMiLCJJZCI6MSwiRW1haWwiOiJlbG9uQG11c2suY29tIn0.2QNf4rh2gTm9bYkouzChLmsbdCek1HUYxF6_GcIlskE" --data "{\"productId\": 1,\"quantity\": 1}"
```
