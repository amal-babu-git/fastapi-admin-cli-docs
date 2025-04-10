# Command Reference

Detailed documentation for all FastAPI Admin CLI commands.

## Project Commands

### `startproject`

Create a new FastAPI project with a complete project structure.

```bash
fastapi-admin startproject myproject
```

Options: None

Creates project structure with:
- Docker configuration
- Database migrations
- Authentication
- Admin panel
- Environment configs

### `startapp`

Generate a new application module within your project.

```bash 
fastapi-admin startapp users
```

Options: None

Creates app with:
- models.py - Database models
- schemas.py - Pydantic schemas
- routes.py - API endpoints
- services.py - Business logic
- admin.py - Admin interface

## Docker Commands

### `docker build`

Build Docker containers for the project.

```bash
fastapi-admin docker build
```

Options: None

Actions:
- Copies env.txt to .env if needed
- Builds API container
- Builds PostgreSQL container

### `docker run`

Start the Docker containers.

```bash
fastapi-admin docker run
```

Options: None

Actions:
- Starts API container
- Starts PostgreSQL container
- Sets up networking

### `docker down`

Stop and remove containers.

```bash
fastapi-admin docker down [--volumes/-v]
```

Options:
- `--volumes/-v` - Also remove volumes

### `docker cmd` 

Run any Docker Compose command.

```bash
fastapi-admin docker cmd "ps"
```

Arguments:
- command: Docker Compose command to run

## Database Commands

### `db makemigrations`

Create new database migrations.

```bash
fastapi-admin db makemigrations -m "message"
```

Options:
- `-m/--message` - Migration description

Actions:
- Detects model changes
- Creates migration files
- Stores in versions/

### `db migrate`

Apply database migrations.

```bash
fastapi-admin db migrate
```

Options: None

Actions:
- Runs pending migrations
- Updates database schema

### `db shell`

Open shell in API container.

```bash
fastapi-admin db shell
```

Provides access to:
- Python shell
- Database
- Project environment

## Development Commands

### `shell`

Launch shell in a container.

```bash
fastapi-admin shell [--container-name NAME]
```

Options:
- `--container-name` - Target container (default: fastapi-app)

### `createsuperuser`

Create admin user account.

```bash
fastapi-admin createsuperuser <email> <password> [--first-name NAME] [--last-name NAME]
```

Arguments:
- email: Admin email
- password: Admin password

Options:  
- `--first-name` - First name
- `--last-name` - Last name

Creates superuser with:
- Admin panel access
- Full permissions
