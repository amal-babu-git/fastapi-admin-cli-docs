# Createsuperuser Command

The `createsuperuser` command creates an admin user account with full permissions for accessing the admin panel.

## Basic Usage

```bash
fastapi-admin createsuperuser admin@example.com password123
```

This will create a new superuser with the given email and password.

## Arguments

| Argument | Description | Required |
|----------|-------------|----------|
| email | Email address for the superuser | Yes |
| password | Password for the superuser | Yes |

## Options

| Option | Description | Default |
|--------|-------------|---------|
| `--first-name` | First name of the superuser | None |
| `--last-name` | Last name of the superuser | None |

## Example Commands

Basic usage:
```bash
fastapi-admin createsuperuser admin@example.com password123
```

With name details:
```bash
fastapi-admin createsuperuser admin@example.com password123 --first-name Admin --last-name User
```

## How It Works

The `createsuperuser` command:

1. Executes the `create_superuser.py` script inside your Docker container
2. Creates a user with superuser status (`is_superuser=True`) and verified status (`is_verified=True`)
3. If the user already exists, updates the user to have superuser privileges

## Admin Configuration Guide

To use the admin panel effectively with your custom models, you need to:

### 1. Create an Admin View Class

Each model you want to manage in the admin interface needs its own Admin View class:

```python
from sqladmin import ModelView
from .models import YourModel
from app.core.main_admin import register_admin

@register_admin
class YourModelAdmin(ModelView, model=YourModel):
    """Admin interface for YourModel."""
    
    name = "YourModel"
    name_plural = "YourModels"
    icon = "fa-solid fa-list"
    
    column_list = [
        YourModel.id,
        # Your model fields here
        YourModel.created_at
    ]
    
    column_searchable_list = [
        # Fields for the search functionality
    ]
    
    column_sortable_list = [
        # Fields that can be sorted
    ]
    
    can_create = True
    can_edit = True
    can_delete = True
    can_view_details = True
```

### 2. Register the Admin View

Update the `setup_admin` function in `app/core/main_admin.py` to import your admin module:

```python
def setup_admin(app: FastAPI) -> None:
    # Import admin modules
    try:
        # Default authentication admin
        import app.auth.admin
        
        # Your application modules
        import app.your_app.admin  # Import your admin module
        
        # Register all views
        for view in admin_views:
            admin.add_view(view)
            logger.info(f"Registered admin view: {view.__name__}")
            
    except ImportError as e:
        logger.warning(f"Error importing admin module: {e}")
```

### 3. Customize Admin Features

You can customize various aspects of your admin interface:

- **Permissions**: Control create, edit, delete, and view permissions
- **Display Fields**: Choose which fields appear in list views
- **Search**: Configure which fields are searchable
- **Filtering**: Add column filters for data filtering
- **Formatting**: Customize how data is displayed

For example, to add custom filters and formatters:

```python
@register_admin
class UserAdmin(ModelView, model=User):
    # ...existing configuration...
    
    column_formatters = {
        User.created_at: lambda m, a: m.created_at.strftime("%Y-%m-%d %H:%M")
    }
    
    column_filters = [
        User.is_active,
        User.is_superuser,
        User.created_at
    ]
```

## User Types

The FastAPI Admin template includes several user permission levels:

| User Type | Description | Access |
|-----------|-------------|--------|
| Regular User | Basic application user | API endpoints |
| Active User | User with confirmed active status | API endpoints requiring active status |
| Verified User | User with verified email | API endpoints requiring verification |
| Superuser | Administrator with full permissions | All endpoints + Admin panel |

## Common Issues

### Container Not Running

If you get a "Container not running" error, start your containers first:

```bash
fastapi-admin docker run
```

### Environment Variables

If you get environment variable warnings, ensure you've created a `.env` file:

```bash
cp env.txt .env
```

### Database Errors

Database connection errors may occur if:
- The database service isn't running
- The database hasn't been initialized with migrations

Run migrations before creating a superuser:

```bash
fastapi-admin db migrate
```

## Admin Panel Access

Once you've created a superuser, you can access the admin panel at:

```
http://localhost:8000/admin
```

Log in with the email and password you provided to the createsuperuser command.

## Related Commands

- [Docker Commands](docker.md) - Manage Docker containers
- [DB Migrations](db-migrations.md) - Database migration commands
