Briefly describe the steps taken to configure your Hasura GraphQL Engine

Step 1:
Installed necessary things required to complete the assessment - 
a) Docker desktop
b) PostgreSQL

Step 2:
Created a docker-compose.yml file
with following input - 

version: "3.6"
services:
  redis:
    image: redis:latest
    restart: always
    ports:
      - "6379:6379"
  postgres:
    image: postgres:15
    restart: always
    ports:
      - "5432:5432"
    volumes:
      - db_data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: postgrespassword
      POSTGRES_USER: postgresuser
      POSTGRES_DB: chinook
  graphql-engine:
    image: hasura/graphql-engine:v2.14.1
    ports:
      - "8080:8080"
    restart: always
    environment:
      HASURA_GRAPHQL_ADMIN_SECRET: myadminsecretkey
      HASURA_GRAPHQL_METADATA_DATABASE_URL: postgres://postgresuser:postgrespassword@postgres:5432/chinook
      HASURA_GRAPHQL_ENABLE_CONSOLE: "true"
      HASURA_GRAPHQL_DEV_MODE: "true"
      HASURA_GRAPHQL_REDIS_URL: "redis://redis:6379"
      HASURA_GRAPHQL_RATE_LIMIT_REDIS_URL: "redis://redis:6379"
      PG_DATABASE_URL: postgres://postgres:postgrespassword@postgres:5432/postgres
volumes:
  db_data:


Step 3:
Started the docker container using docker-compose up -d

Step 4: 
Cloned the chinook database - git clone https://github.com/lerocha/chinook-database

Step 5:
psql -h localhost -p 5432 -U postgresuser -d chinook -f Chinook_PostgreSql.sql

Step 6:
Opened the localhost - http://localhost:8080 and entered the admin_secret_key to open the Hasura console.

Step 7:
Open up the hasura console and under Data tab, Connected postgreSQL database which we import earlier.

Step 8:
Ran all the GraphQL queries that were there in the assignment


