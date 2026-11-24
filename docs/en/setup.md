# Setup and configuration

[Versión en español](../setup.md) · [README](../../README.md)

## Requirements

Java 21, Maven, Node.js 20+ and PostgreSQL or Docker.

## 1. Database

From the repository root, start a local development database:

```bash
docker run -d --name stockapi-pg -e POSTGRES_PASSWORD=stockapi -p 5434:5432 postgres:16-alpine
```

These values are for local development only. An external PostgreSQL instance such as Supabase may also be configured.

## 2. Backend

```bash
cd backend
cp src/main/resources/application-local.properties.example src/main/resources/application-local.properties
```

Edit the local configuration. For the container above:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5434/postgres
spring.datasource.username=postgres
spring.datasource.password=stockapi
jwt.secret=<random-secret-of-at-least-32-characters>
```

```bash
mvn spring-boot:run -Dspring-boot.run.profiles=local
```

Flyway applies migrations at startup. API: http://localhost:8080. Swagger: http://localhost:8080/swagger-ui.html.

## 3. Frontend

In a separate terminal, from the root:

```bash
cd frontend
npm install
npm run dev
```

Open http://localhost:5173. The Vite proxy forwards /api to the backend.

## 4. Initial access

The original configuration documents a development account `admin@stockapi.com` with password `Admin123`. Change it immediately and never reuse these values in a public environment. Do not publish real credentials.

## Deployment configuration

The backend uses `DATABASE_URL`, `DATABASE_USERNAME`, `DATABASE_PASSWORD` and `JWT_SECRET` environment variables. The `application-local.properties` file is excluded from version control.

For schema changes, create a new `V<n>__description.sql` migration. Hibernate runs in `validate` mode.

These steps reproduce the documented project setup; installation was not executed during this review.
