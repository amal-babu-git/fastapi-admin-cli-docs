# Database Migration Commands

The Database migration commands provide an easy way to manage your database schema changes using Alembic.

## Basic Usage

```bash
fastapi-admin db makemigrations -m "initial migration"
fastapi-admin db migrate
```

This will create and apply migrations to your database based on your SQLModel models.

## Available Commands

| Command | Description |
|---------|-------------|
| `makemigrations` | Create new database migrations |
| `migrate` | Apply pending database migrations |
| `shell` | Open a shell in the API container |
| `env_check` | Check for missing environment variables |

## Command Details

### Makemigrations

Creates new database migration files based on detected changes in your SQLModel models.

```bash
fastapi-admin db makemigrations -m "message"
```

Options:

| Option | Short | Description |
|--------|-------|-------------|
| `--message` | `-m` | Message describing the migration (default: "init") |

<p>This command will:</p>
1. Detect changes in your SQLModel models
2. Generate migration files in the `migrations/versions` directory
3. Each migration file contains upgrade and downgrade functions

### Migrate

Applies all pending database migrations to bring your database schema up to date.

```bash
fastapi-admin db migrate
```

<p>This command will:</p>
1. Run all pending migrations in sequence
2. Apply schema changes to your database
3. Update the Alembic version table to track applied migrations

### Shell

Opens a shell in the API Docker container for direct access to the environment.

```bash
fastapi-admin db shell
```

<p>This shell allows you to:</p>
1. Run Python code with access to your models and environment
2. Execute direct Alembic commands for advanced operations
3. Access the database directly

Example shell usage:
```bash
# Once in the shell
alembic current      # Show current migration version
alembic history      # Show migration history
alembic downgrade -1 # Downgrade one version
```

## How It Works

The migration commands work through the following process:

1. **Model Detection**:
   - Migrations scan the models defined in `app/core/main_models.py`
   - All imported SQLModel classes are detected for changes

2. **Migration Storage**:
   - Migration files are stored in `migrations/versions/`
   - Each migration is tracked with a unique revision ID

3. **Docker Integration**:
   - Commands run through Docker Compose to ensure consistent environments
   - Uses the API container defined in your docker-compose.yml

## Common Issues

- **Model Not Found**: Ensure models are imported in `app/core/main_models.py`
- **Migration Conflicts**: If multiple developers create migrations, merge them carefully
- **Failed Migrations**: Use the shell to downgrade to a previous version
- **Empty Migrations**: No changes detected in models since last migration
- **Database Connection Issues**: Check database URL in settings or environment variables

## Troubleshooting

If you encounter issues with migration commands:

1. **Migration Creation Failed**:
   - Ensure all models are properly imported in main_models.py
   - Check for syntax errors in your model definitions
   - Verify database connection settings

2. **Migration Application Failed**:
   - Check the migration files for complex operations that might fail
   - Look at database logs for specific SQL errors
   - Try running specific migrations directly in the shell

3. **No Changes Detected**:
   - Confirm your model changes are in the right files
   - Make sure changes are significant (adding fields, changing types, etc.)

4. **Advanced Fixes**:
   - Use the shell to run specific Alembic commands
   - Check Alembic's current version with `alembic current`
   - Execute SQL directly if needed for complex situations
   - Use `fastapi-admin shell` to access the container's environment

## Best Practices

1. **Meaningful Messages**: Use descriptive -m messages for each migration
2. **Regular Migrations**: Create small, focused migrations rather than large changes
3. **Test Migrations**: Always test migrations in development before production
4. **Version Control**: Commit migration files to your version control system
5. **Database Backups**: Always backup your database before applying migrations in production

For more information on Alembic and SQLModel, refer to their official documentation.
