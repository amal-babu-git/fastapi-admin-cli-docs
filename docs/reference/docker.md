# Docker Commands

The Docker commands provide an easy way to manage Docker containers for your FastAPI project.

## Basic Usage

```bash
fastapi-admin docker build
fastapi-admin docker run
```

This will build and start your Docker containers defined in your project's docker-compose.yml file.

## Available Commands

| Command | Description |
|---------|-------------|
| `build` | Build Docker containers |
| `run` | Start Docker containers |
| `down` | Stop and remove Docker containers |
| `cmd "command"` | Run any Docker Compose command |

## Command Details

### Build

Builds the Docker containers defined in your project's docker-compose.yml file.

```bash
fastapi-admin docker build
```

<p>This command will:</p>
1. Check if a `.env` file exists and create one from `env.txt` if needed
2. Build all containers defined in `docker/compose/docker-compose.yml`

### Run

Starts the Docker containers in detached mode.

```bash
fastapi-admin docker run
```

<p>This command will:</p>
1. Start all containers defined in `docker/compose/docker-compose.yml`
2. Run in detached mode (`-d` flag)
3. Set up necessary networking

### Down

Stops and removes running Docker containers.

```bash
fastapi-admin docker down
```

Options:

| Option | Short | Description |
|--------|-------|-------------|
| `--volumes` | `-v` | Also remove volumes |

Example to remove containers and volumes:
```bash
fastapi-admin docker down -v
```

### Cmd

Runs any arbitrary docker-compose command.

```bash
fastapi-admin docker cmd "COMMAND"
```

Examples:
```bash
fastapi-admin docker cmd "ps"
fastapi-admin docker cmd "logs api"
fastapi-admin docker cmd "restart api"
```

## Integration with Project

The Docker commands are designed to work with the project structure created by the `startproject` command. The commands expect:

1. A `docker/compose/docker-compose.yml` file in your project
2. A compatible Dockerfile that defines your API service
3. PostgreSQL database service configuration

## Common Issues

- **Docker not installed**: Ensure Docker and docker-compose are installed and running
- **Port conflicts**: If ports are already in use, update the port mappings in your docker-compose.yml
- **Permission issues**: On Linux/Mac systems, you might need to run with sudo or add your user to the docker group
- **Environment variables**: If the container fails to start, check your `.env` file for missing required variables
- **Resource limitations**: Ensure Docker has sufficient CPU/memory allocated (especially on Docker Desktop)

## Troubleshooting

If you encounter issues with Docker commands:

1. Check Docker logs: `fastapi-admin docker cmd "logs"`
2. Verify all containers are running: `fastapi-admin docker cmd "ps"`
3. Ensure your `.env` file has all required environment variables
4. Try rebuilding the containers: `fastapi-admin docker build`
5. Check connectivity between containers with: `fastapi-admin docker cmd "exec api ping postgres"`

For more advanced Docker issues, refer to the Docker and docker-compose documentation.
