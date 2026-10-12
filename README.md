# Smart Hostel Backend

The Spring Boot REST API for Smart Hostel. It manages staff accounts, student records, room assignments, audit history, and the student portal. Data is stored in MySQL.

## Run locally

Requirements: Java 21 or newer, Maven 3.9 or newer, and MySQL 8 or newer.

Create a database and a limited application user, then configure `DB_URL`, `DB_USERNAME`, and `DB_PASSWORD` in the environment where Maven runs. Configure a unique `STAFF_INVITE_CODE` if you need to bootstrap the first administrator.

```bash
mvn spring-boot:run
```

The API listens on port 8080 by default. Run the separate frontend repository to use the web interface. Never commit database passwords or administrator invite codes.

## Deploy on Railway

Create a Railway service from this repository and use the repository root as its service root. Railway builds the included `Dockerfile`. Add a managed MySQL service and configure `DB_URL`, `DB_USERNAME`, and `DB_PASSWORD` with Railway variable references. Set `SESSION_COOKIE_SECURE=true` and `CORS_ALLOWED_ORIGINS` to the exact HTTPS origin of the frontend service. Keep the backend and database private; publish only the frontend service.

Railway supplies `PORT`. The backend exposes `/healthz` for health checks and `/api` for application requests. Session data is stored in MySQL so sign-ins remain valid across backend restarts.

## CI

GitHub Actions runs `mvn --batch-mode verify` for pushes and pull requests.
