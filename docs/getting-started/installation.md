# Installation

## Prerequisites

Before installing FastAPI Admin CLI, ensure you have:

- Python 3.13 or higher
- pip (Python package installer)
- Docker and docker-compose
- Git
- uv (optional, python package manager)

## Installation Methods

### Using pip (Recommended)

```bash
pip install fastapi-admin-cli
```

### Development Installation

```bash
git clone https://github.com/amal-babu-git/fastapi-admin-cli.git
cd fastapi-admin-cli
pip install -e .
```

<!-- ## Verify Installation -->

<!-- After installation, verify that the CLI is working: -->

<!-- ```bash
fastapi-admin --version
``` -->

## Environment Setup

### Virtual Environment (Recommended)

We recommend using a virtual environment. You can choose either method:

#### Using uv (Recommended)
```bash
# Create and setup project
fastapi-admin startproject myproject
cd myproject
uv sync

# Create and activate virtual environment
# On Windows:
.venv\Scripts\activate

# On Unix or MacOS:
source .venv/bin/activate
```

#### Using Python's venv
```bash
# Create and setup project
fastapi-admin startproject myproject
cd myproject

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On Unix or MacOS:
source venv/bin/activate

# Install dependencies
pip install -e .
```

After activating the virtual environment, your project is ready for development.

## Next Steps

Once installed, you can:

1. Create your first project: `fastapi-admin startproject myproject`
2. Review the [Quick Start Guide](quickstart.md)
3. Explore the [Command Reference](../reference/cli-commands.md)
