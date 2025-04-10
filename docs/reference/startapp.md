# Start App Command

The `startapp` command creates a new application module within your FastAPI project with a consistent structure.

## Basic Usage

```bash
fastapi-admin startapp blog
```

This command will create a new app module in your project's `app` directory.

## Arguments

| Argument | Description | Required |
|----------|-------------|----------|
| app_name | Name of your app | Yes |

## App Structure

```
app/blog/
├── __init__.py          # Python package marker
├── admin.py             # Admin panel configuration
├── models.py            # SQLModel database models
├── routes.py            # FastAPI route definitions
├── schemas.py           # Pydantic data schemas
└── services.py          # Business logic and database operations
```

## Smart App Generation

The `startapp` command automatically:

- Creates the app with proper naming conventions
- Converts plural app names to singular model names when appropriate
- Sets up correctly formatted table names for database models
- Generates CRUD endpoints for your data model
- Creates Pydantic schemas for request/response validation
- Configures an admin interface for the model

## Integration with Main App

After creating your app, you need to complete several integration steps:

### 1. Register the Router

Add these lines to `app/core/main_routes.py`:

```python
from app.blog.routes import router as blog_router
main_router.include_router(
    blog_router,
    prefix=f"/api/{api_version}/blog",
    tags=["blog"]
)
```

### 2. Import the Model for Migrations

For Alembic to detect your models, add an import to `app/core/main_models.py`:

```python
# Import your app-specific models here
from app.blog.models import Post  # Import your new model
```

### 3. Import Admin Configuration

For the admin interface to recognize your model, update the `setup_admin` function in `app/core/main_admin.py`:

```python
def setup_admin(app: FastAPI) -> None:
    # Import admin modules - update these imports based on your app structure
    try:
        # These will be dynamically imported based on your project structure
        # Default authentication admin
        import app.auth.admin
        
        # Your application modules should be imported here
        import app.blog.admin  # Import your new admin module
        
        # Register all views to admin
        for view in admin_views:
            admin.add_view(view)
            logger.info(f"Registered admin view: {view.__name__}")
            
    except ImportError as e:
        logger.warning(f"Error importing admin module: {e}")
```

Once your model is registered in the admin panel, you can create a superuser to access it:

```bash
fastapi-admin createsuperuser admin@example.com password123
```

See the [Createsuperuser Command](createsuperuser.md) documentation for more details.

### 4. Access your API endpoints

<p> Your API will now have the following endpoints</p>
- `GET /api/v1/blog/` - List all blog posts
- `GET /api/v1/blog/{item_id}` - Get a specific blog post
- `POST /api/v1/blog/` - Create a new blog post
- `PUT /api/v1/blog/{item_id}` - Update a blog post
- `DELETE /api/v1/blog/{item_id}` - Delete a blog post

### 5. Access the admin panel

Your blog posts will be automatically available in the admin panel at `/admin`.


## Common Issues

- **App name validation**: Use lowercase letters for app names; the CLI will handle proper case transformation
- **Directory exists**: Choose a different name or remove the existing directory
- **Not in project root**: Make sure to run the command from the project root directory
- **Missing app directory**: The CLI will create the app directory if it doesn't exist
