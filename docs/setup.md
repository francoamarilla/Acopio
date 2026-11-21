# Instalación y configuración

[English version](en/setup.md) · [README](../README.md)

## Requisitos

Java 21, Maven, Node.js 20+ y PostgreSQL o Docker.

## 1. Base de datos

Desde la raíz del repositorio, para una base de desarrollo local:

```bash
docker run -d --name stockapi-pg -e POSTGRES_PASSWORD=stockapi -p 5434:5432 postgres:16-alpine
```

Los valores anteriores son exclusivamente de desarrollo local. También se puede configurar una instancia PostgreSQL externa, como Supabase.

## 2. Backend

```bash
cd backend
cp src/main/resources/application-local.properties.example src/main/resources/application-local.properties
```

Editar el archivo local con la configuración de PostgreSQL. Para el contenedor anterior:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5434/postgres
spring.datasource.username=postgres
spring.datasource.password=stockapi
jwt.secret=<clave-aleatoria-secreta-de-32-o-mas-caracteres>
```

```bash
mvn spring-boot:run -Dspring-boot.run.profiles=local
```

Flyway aplica las migraciones al iniciar. API: http://localhost:8080. Swagger: http://localhost:8080/swagger-ui.html.

## 3. Frontend

En otra terminal, desde la raíz:

```bash
cd frontend
npm install
npm run dev
```

Abrir http://localhost:5173. El proxy de Vite reenvía /api al backend.

## 4. Primer acceso

La configuración original documenta un usuario inicial de desarrollo `admin@stockapi.com` con contraseña `Admin123`. Cambiarla inmediatamente y nunca reutilizar estos valores en un entorno público. No publicar credenciales reales.

## Configuración de despliegue

El backend utiliza estas variables de entorno: `DATABASE_URL`, `DATABASE_USERNAME`, `DATABASE_PASSWORD` y `JWT_SECRET`. El archivo `application-local.properties` está excluido del control de versiones.

Para modificar el esquema, crear una migración nueva `V<n>__descripcion.sql`. Hibernate utiliza `validate`.

Los pasos reproducen la configuración documentada del proyecto; no se ejecutó una instalación durante esta revisión.
