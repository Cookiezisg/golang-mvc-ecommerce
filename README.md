# Gin Mart

[![Go Version](https://img.shields.io/badge/Go-1.25.5-00ADD8?logo=go&logoColor=white)](#)
[![Framework](https://img.shields.io/badge/Gin-HTTP%20Framework-00ADD8?logo=go&logoColor=white)](#)
[![ORM](https://img.shields.io/badge/Gorm-ORM-7E56C2)](#)
[![Database](https://img.shields.io/badge/MySQL-Database-4479A1?logo=mysql&logoColor=white)](#)
[![Docs](https://img.shields.io/badge/Swagger-API%20Docs-85EA2D?logo=swagger&logoColor=black)](#)

A Gin + Gorm ecommerce backend using a layered MVC structure with JWT auth and Swagger docs.
It covers core flows for users, products, categories, carts, and orders.

## Highlights

- User registration/login with JWT (user vs admin)
- Product CRUD + search with pagination
- Category CRUD with CSV bulk import
- Cart management (add/update/list)
- Order creation, listing, and cancellation
- AutoMigrate schema and seed data on boot
- Swagger API documentation

## Tech Stack

- Go (see `go.mod`)
- Gin
- Gorm + MySQL
- Viper config
- JWT
- Swagger (swag)

## Project Structure

```
.
├── api/                 # HTTP controllers + routing
├── config/              # config loader + defaults
├── docs/                # Swagger docs
├── domain/              # entities / repositories / services
├── utils/               # helpers (JWT, pagination, CSV, DB, etc.)
└── main.go              # entry point
```

## Quick Start

1) Start MySQL and create a database (default `go_database`).
2) Update `config/config.yaml`:

```yaml
DatabaseSettings:
  DatabaseURI: "root:@tcp(127.0.0.1:3306)/go_database?parseTime=True&loc=Local"
JwtSettings:
  SecretKey: "your-secret"
```

3) Run the server:

```bash
go run main.go
```

4) Swagger UI:
`http://localhost:8080/swagger/index.html`

## Default Accounts

Seeded on startup:

- Admin: `admin / admin`
- User: `user / user`

## API Snapshot

> See Swagger for full details.

- `POST /user` Register
- `POST /user/login` Login (JWT)
- `GET /category` List categories
- `POST /category` Create category (admin)
- `POST /category/upload` Bulk import categories (admin)
- `GET /product` List/search products
- `POST /product` Create product (admin)
- `PATCH /product` Update product (admin)
- `DELETE /product` Delete product (admin)
- `GET /cart` List cart items (user)
- `POST /cart/item` Add to cart (user)
- `PATCH /cart/item` Update cart item (user)
- `GET /order` List orders (user)
- `POST /order` Create order (user)
- `DELETE /order` Cancel order (user)

## Auth

Send JWT in headers:

```
Authorization: <token>
```

Admin-only endpoints require `IsAdmin = true` (default `admin` user).
