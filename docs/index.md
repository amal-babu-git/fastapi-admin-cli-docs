# FastAPI Admin CLI

A Django-inspired CLI tool for managing FastAPI applications with a modular structure and best practices.

- 🚀 Project scaffolding with batteries included
- 📦 Modular app structure like Django
- 🐳 Built-in Docker integration
- 🔄 Database migrations with Alembic 
- 🔐 Authentication with FastAPI-Users
- 👤 Admin panel with SQLAdmin

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
- [Start Project](reference/startproject.md) 

## License

MIT License - see [LICENSE](https://github.com/amal-babu-git/fastapi-admin-cli/blob/main/LICENSE)
