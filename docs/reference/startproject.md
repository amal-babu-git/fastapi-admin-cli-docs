# Start Project Command

The `startproject` command creates a new FastAPI project with a modular structure.

## Basic Usage

```bash
fastapi-admin startproject myproject
```
```bash
cd myproject
```
> update .env

```bash
fastapi-admin docker build
```
```bash
fastapi-admin docker run
```

## Arguments

| Argument | Description | Required |
|----------|-------------|----------|
| project_name | Name of your project | Yes |

## Project Structure

```
myproject/
├── .env                        # Environment variables configuration
├── alembic.ini                 # Alembic configuration for database migrations
├── env.txt                     # Example environment variables file
├── manage.py                   # CLI management script
├── pyproject.toml              # Project dependencies and configuration
├── README.md                   # Project documentation
├── uv.lock                     # Package lock file
├── app/                        # Main application package
│   ├── main.py                 # Application entry point
│   ├── auth/                   # Authentication module
│   │   ├── __init__.py
│   │   ├── admin.py            # Admin interface for auth models
│   │   ├── auth.py             # Auth core functionality
│   │   ├── email.py            # Email service for auth
│   │   ├── models.py           # Auth data models
│   │   ├── routes.py           # Auth API endpoints
│   │   ├── schemas.py          # Auth data schemas
│   └── core/                   # Core application module
│       ├── __init__.py
│       ├── admin_auth.py       # Admin authentication
│       ├── db.py               # Database configuration
│       ├── main_admin.py       # Admin interface setup
│       ├── main_models.py      # Core data models
│       ├── main_routes.py      # Main API routes
│       ├── settings.py         # Application settings
├── docker/                     # Docker configuration
│   ├── Dockerfile              # Main Dockerfile
│   ├── compose/                # Docker Compose configurations
│   │   ├── docker-compose.yml  # Development compose file
│   │   └── docker-compose.prod.yml # Production compose file
│   └── traefik/                # Traefik reverse proxy configuration
│       └── traefik.yml         # Traefik configuration
├── migrations/                 # Database migrations
│   ├── env.py                  # Alembic environment setup
│   ├── README                  # Migrations documentation
│   ├── script.py.mako          # Migration template    
│   └── versions/               # Migration versions
│       ├── __init__.py
└── scripts/                    # Utility scripts
    └── create_superuser.py     # Script to create admin users
```

## Common Issues

- **Project name validation**: Use lowercase letters, numbers, underscores
- **Directory exists**: Choose different name or remove existing directory
- **Permission denied**: Run from a directory where you have write access