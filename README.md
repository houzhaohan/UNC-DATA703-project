# Backend — Product Marketplace API

Flask-based REST API for a second-hand product marketplace. Provides user authentication, product management, and image upload/download endpoints.

## Tech Stack

| Component | Version |
|---|---|
| Python | ≥ 3.10 |
| Flask | ≥ 3.1 |
| Flask-SQLAlchemy | ≥ 3.1 |
| Flask-JWT-Extended | ≥ 4.7 |
| Flask-CORS | ≥ 5.0 |
| psycopg2-binary | ≥ 2.9 |
| Database | PostgreSQL (Neon) |

## Directory Layout

```
backend/
├── app.py            # Application entry point: create_app() + Blueprint registration
├── config.py         # Configuration class (DB URI, JWT secret, etc.)
├── extensions.py     # Shared extensions: db, jwt
├── models.py         # SQLAlchemy models: User, Product, Image
├── routes/           # Route blueprints
│   ├── auth.py       # Register / login / change password
│   ├── products.py   # Product CRUD + search & filter
│   ├── admin.py      # Admin-only endpoints
│   └── images.py     # Image upload / download
├── utils/            # Helpers (response format, auth utilities)
└── requirements.txt
```

## Prerequisites

**No virtual environment required** — install dependencies directly into your system Python.

```bash
python --version      # Make sure Python ≥ 3.10
pip install -r requirements.txt
```

## Database Configuration

The default database is a [Neon](https://neon.tech) hosted PostgreSQL instance, with the connection string defined in `config.py`.

To point to a different database, set the `DATABASE_URL` environment variable — it takes precedence over the built-in default:

```bash
# Local PostgreSQL
set DATABASE_URL=postgresql://user:pass@localhost:5432/mydb

# Or SQLite for quick debugging
set DATABASE_URL=sqlite:///app.db
```

## Run

```bash
python app.py
```

The server starts at `http://0.0.0.0:3031`. On first launch it automatically creates all tables and seeds a default admin account:

| Username | Password |
|---|---|
| admin | admin123 |

Health check: `GET http://localhost:3031/api/health`

## API Overview

All endpoints are prefixed with `/api`. Authenticated endpoints require `Authorization: Bearer <token>` in the request header.

### Authentication `/auth`
| Method | Path | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login, returns a JWT |
| POST | `/api/auth/change-password` | Change password (auth required) |

### Products `/products`
| Method | Path | Description |
|---|---|---|
| GET | `/api/products` | List products, supports keyword / category / price_min / price_max filters |
| GET | `/api/products/<id>` | Product detail |
| POST | `/api/products` | Create a product (auth required) |
| PUT | `/api/products/<id>` | Update your own product (auth required) |
| DELETE | `/api/products/<id>` | Delete your own product (auth required) |

### Images `/images`
| Method | Path | Description |
|---|---|---|
| POST | `/api/images` | Upload an image (multipart/form-data, auth required) |
| GET | `/api/images/<id>` | Fetch raw image bytes |

### Admin `/admin`
| Method | Path | Description |
|---|---|---|
| GET | `/api/admin/users` | List all users (admin role required) |
| DELETE | `/api/admin/users/<id>` | Delete a user (admin role required) |
| GET | `/api/admin/products` | List all products (admin role required) |
| DELETE | `/api/admin/products/<id>` | Delete any product (admin role required) |
