<p align="center"><img src="branding/logo-claro.png" alt="Acopio — gestión de inventario" width="320"></p>

# Acopio

Gestión de inventario para talleres mecánicos: stock de repuestos y lubricantes, ventas, compras a proveedores, clientes con sus vehículos y cierre de caja.

> Antes se llamaba **StockAPI Manager**.

## Funcionalidades

- **Productos y stock:** alertas de stock mínimo, historial de movimientos y baja lógica.
- **Ventas:** mano de obra, medio de pago, cliente y vehículo. Descuentan stock al crearse y lo devuelven si se anulan.
- **Compras:** a proveedores, con sugerencias de reposición. Suman stock al recibirse.
- **Caja:** cierres diarios por medio de pago.
- **Dashboard y reportes:** se actualizan solos cada 30 s.
- **Roles:** `ADMIN` y `OPERADOR`.
- **Tema:** claro y oscuro.

## Stack

| Capa | Tecnología |
|---|---|
| Backend | Java 21, Spring Boot 3.2, Spring Security + JWT, JPA, Flyway |
| Base de datos | PostgreSQL (Supabase o Docker) |
| Frontend | React 18, TypeScript, Vite, TanStack Query |

## Correr en local

Requisitos: Java 21, Maven, Node 20+ y PostgreSQL (o Docker).

```bash
# 1. Base de datos (Flyway crea el esquema al arrancar)
docker run -d --name stockapi-pg -e POSTGRES_PASSWORD=stockapi -p 5434:5432 postgres:16-alpine

# 2. Backend → http://localhost:8080 (Swagger en /swagger-ui.html)
cd backend
cp src/main/resources/application-local.properties.example src/main/resources/application-local.properties
# editar: URL jdbc:postgresql://localhost:5434/postgres, usuario postgres, password y jwt.secret (32+ caracteres)
mvn spring-boot:run -Dspring-boot.run.profiles=local

# 3. Frontend → http://localhost:5173 (proxy /api → :8080)
cd frontend && npm install && npm run dev
```

En el primer arranque se crea el usuario `admin@stockapi.com` / `Admin123`. Cambiá la contraseña.

En producción, el backend lee `DATABASE_URL`, `DATABASE_USERNAME`, `DATABASE_PASSWORD` y `JWT_SECRET` desde el entorno. `application-local.properties` está en `.gitignore`: no commitees credenciales.

## Estructura

```
backend/    Spring Boot (controller, service, repository, model, security)
            └─ src/main/resources/db/migration/   migraciones Flyway
frontend/   React + TS (pages, components, hooks, styles/tokens.css)
branding/   logo, isotipo, favicon y paleta de Acopio
docs/       diseño y scripts SQL de referencia
```

## API

La documentación completa de los endpoints está en Swagger: `http://localhost:8080/swagger-ui.html`. Salvo `/api/auth/login`, todos los endpoints requieren `Authorization: Bearer <token>`.

## Reglas de negocio

- El stock solo cambia con ventas, compras recibidas o movimientos manuales, y cada cambio queda registrado como movimiento.
- Anular una venta devuelve el stock.
- Los ajustes usan un delta con signo: positivo suma, negativo resta.
- `OPERADOR` puede operar el día a día. No puede borrar productos, administrar usuarios o proveedores, ni anular compras.

## Para cambiar el esquema

Agregá una migración `V<n>__descripcion.sql` nueva y nunca edites una ya aplicada. Hibernate corre en modo `validate`.
