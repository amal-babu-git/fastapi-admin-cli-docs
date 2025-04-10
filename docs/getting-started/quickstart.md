# Quick Start Guide

This guide will help you create your first FastAPI Admin project.

## Create a Project

1. Install FastAPI Admin CLI:
   ```bash
   pip install fastapi-admin-cli
   ```

2. Create a new project:
   ```bash
   fastapi-admin startproject myproject
   cd myproject
   ```

## Setup Environment

1. Copy environment template:
   ```bash
   cp env.txt .env
   ```

2. Configure variables in .env:
   ```ini
   # API Settings
   API_TITLE=My API
   API_VERSION=0.1.0
   
   # Database Settings
   POSTGRES_USER=postgres
   POSTGRES_PASSWORD=postgres
   POSTGRES_DB=app_db
   ```

## Launch with Docker

1. Build containers:
   ```bash
   fastapi-admin docker build
   ```

2. Start services:
   ```bash
   fastapi-admin docker run
   ```

## Database Setup

1. Create migrations:
   ```bash
   fastapi-admin db makemigrations -m "initial"
   ```

2. Apply migrations:
   ```bash
   fastapi-admin db migrate
   ```
   > ℹ️ **INFO**  
   > For other db management commands use alembic directly in container shell.
   > ```bash
   > fastapi-admin shell
   > ```
   > Then inside the shell execute alembic commands. Example:  ```alembic upgrade head``` 

## Create Admin User

Create superuser for admin access:

```bash
fastapi-admin createsuperuser admin@example.com password123
```

## Access Your Application

- API Documentation: http://localhost:8000/docs
- Admin Interface: http://localhost:8000/admin
- API Root: http://localhost:8000/api/v1

## Next Steps

1. Create your first app:
   ```bash
   fastapi-admin startapp blog
   ```

2. Add routes to  app/core/<b>main_routes.py </b>:
   ```python
   from app.blog.routes import router as blog_router
   app.include_router(blog_router, prefix="/api/v1/blog", tags=["blogs"])
   ```

3. Create models in app/blog/models.py
4. Make and apply migrations
5. Implement your business logic

## Development Workflow

1. Make model changes
2. Create migrations:
   ```bash
   fastapi-admin db makemigrations
   ```

3. Apply migrations:
   ```bash
   fastapi-admin db migrate
   ```

4. Access shell if needed:
   ```bash
   fastapi-admin shell
   ```

See the [Command Reference](../reference/cli-commands.md) for more details.
