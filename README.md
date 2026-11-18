# Bank API

A REST API that simulates a small multi-bank system: users, bank accounts, deposits, withdrawals, transfers and a Mobile Money withdrawal flow. Built with Spring Boot as a university project (INF352, University of Yaoundé I).

Version française plus bas.

## What it does

- Users sign up, receive a 4-digit code by email, and verify their account before using the API.
- Several banks can coexist, each with its own settings (for example a profit rate).
- Each user can open accounts of different types (savings, current) in different banks.
- Operations: deposit, withdrawal, transfer between accounts, and a simulated withdrawal to Mobile Money (MTN MoMo, Orange Money) with a configurable limit.
- Protected endpoints require a JWT token.
- Swagger UI documents every endpoint.

## Tech stack

| Area | Tools |
|---|---|
| Language | Java 21 |
| Framework | Spring Boot 3 (Web, Data JPA, Validation, Security, Mail) |
| Auth | JWT (jjwt) |
| Database | PostgreSQL (hosted on Neon) |
| API docs | springdoc-openapi (Swagger UI) |
| Build | Maven |
| Container | Docker (multi-stage build) |

## Project structure

```
src/main/java/com/inf352/bankapi
├── config        CORS, security, data initializer
├── controller    REST endpoints (auth, users, accounts, banks, transactions)
├── exception     custom exceptions and global error handler
├── model         JPA entities (BankUser, Bank, BankAccount, AccountType, BankTransaction)
├── repository    Spring Data repositories
└── service       business rules (balance checks, transfers, verification)
```

The `docs/` folder contains the technical sheet, the test report and control flow graphs for the main services. The `CFG/` folder has the activity diagrams as images.

## Run it locally

You need Java 21 and a PostgreSQL database.

1. Set the environment variables:

```bash
export NEON_JDBC_URL="jdbc:postgresql://<host>/<database>?sslmode=require"
export NEON_DB_USERNAME="<user>"
export NEON_DB_PASSWORD="<password>"
# optional, only needed for verification emails
export MAIL_USERNAME="<gmail address>"
export MAIL_PASSWORD="<gmail app password>"
```

2. Start the API:

```bash
./mvnw spring-boot:run
```

3. Open Swagger UI at `http://localhost:8080/swagger-ui.html`.

With Docker:

```bash
docker build -t bank-api .
docker run -p 8080:8080 -e NEON_JDBC_URL=... -e NEON_DB_USERNAME=... -e NEON_DB_PASSWORD=... bank-api
```

## Tests

```bash
./mvnw test
```

Controller tests are in `src/test/java`. Helper scripts for Windows and Linux are in `scripts/`.

---

## Version française

API REST qui simule un petit système bancaire multi-banques : utilisateurs, comptes, dépôts, retraits, virements et retrait vers Mobile Money. Projet universitaire (INF352, Université de Yaoundé I) réalisé avec Spring Boot.

Fonctionnalités principales : inscription avec code de vérification envoyé par email, plusieurs banques avec leurs propres paramètres, plusieurs types de comptes, authentification par JWT, documentation Swagger.

Pour lancer le projet : définir les variables d'environnement de la base de données (voir plus haut), puis `./mvnw spring-boot:run`, et ouvrir `http://localhost:8080/swagger-ui.html`.

La fiche technique complète et le rapport de tests sont dans le dossier `docs/`.
