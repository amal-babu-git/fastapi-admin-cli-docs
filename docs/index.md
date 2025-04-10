# FastAPI Admin CLI

A Django-inspired CLI tool for managing FastAPI applications with a modular structure and best practices.

> I've been using Django in almost all the projects I've worked on, typically combining Django REST Framework (DRF) for APIs and React or Next.js for the frontend.
>
> Over the last three years, I've read a lot about FastAPI—its modern, Pythonic development style, excellent performance, asynchronous support, and great documentation. I finally gave it a try recently, and it's awesome.
>
> However, I prefer following a proper modular structure in my projects. Django's app system and its manage.py CLI are very developer-friendly. So, I adopted a Django-style modular approach in FastAPI using SQLAdmin for the admin panel, Alembic for database migrations and FastAPI-Users for authentication.
>
> While this setup works well, creating modules and setting up authentication repeatedly for new projects became tedious. To streamline my workflow, I built fastapi-admin-cli—a CLI tool with commonly used Django-like commands for FastAPI. It supports startproject (with auth and admin panel) and startapp, making project setup easier and faster.
> 
>  [amal-babu-git](https://github.com/amal-babu-git)

## Quick Install

```bash
pip install fastapi-admin-cli
```

## Available Commands

| Command | Description |
|---------|-------------|
| `startproject` | Create a new FastAPI project |
| `startapp` | Create a new app within the project |
| `docker build` | Build Docker containers |
| `docker run` | Run Docker containers |
| `docker down` | Stop and remove containers |
| `docker cmd "command"` | Run custom docker-compose commands |
| `db makemigrations` | Create database migrations |
| `db migrate` | Apply migrations (using alembic) |
| `db shell` | Open API container shell |
| `createsuperuser` | Create admin user |
| `shell` | Launch container shell |

## Features

- 🚀 Project scaffolding with batteries included
- 📦 Modular app structure like Django
- 🐳 Built-in Docker integration
- 🔄 Database migrations with Alembic 
- 🔐 Authentication with FastAPI-Users
- 👤 Admin panel with SQLAdmin

## Quick Start

1. Create a new project:
   ```bash
   fastapi-admin startproject myproject
   cd myproject
   ```

2. Set up environment:
   ```bash 
   cp env.txt .env
   ```

3. Launch with Docker:
   ```bash
   fastapi-admin docker build
   fastapi-admin docker run
   ```

4. Create migrations:
   ```bash
   fastapi-admin db makemigrations
   fastapi-admin db migrate 
   ```

5. Create admin user:
   ```bash
   fastapi-admin createsuperuser admin@example.com password123
   ```

See the [Quick Start Guide](getting-started/quickstart.md) for more details.

## Documentation

- [Installation](getting-started/installation.md)
- [Command Reference](reference/cli-commands.md) 

## License

MIT License - see [LICENSE](https://github.com/amal-babu-git/fastapi-admin-cli/blob/main/LICENSE)
