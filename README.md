# CLEAN FASTAPI

This project demonstrates a robust implementation of the Clean Architecture pattern using FastAPI. It is designed for maintainability, scalability, and testability, making it suitable for production-grade web applications. The architecture separates concerns across layers, including models, repositories, services, schemas, and API endpoints. Key features include:

- Minimal and focused functionality for ease of understanding and extension.
- Clear separation of concerns, following Clean Architecture principles.
- Readable and well-organized codebase for fast onboarding.
- Compatibility with modern Python (3.9+) and FastAPI (0.78.0).
- Versatile integration with MySQL and PostgreSQL databases.
- Database migrations managed via Alembic.
- Dependency injection using the `dependency-injector` library.
- JWT-based authentication with role-based access control.
- Comprehensive testing setup with pytest, including real database integration.
- Flexible deployment options for containers (Kubernetes, Docker) and raw WAS environments.

The project models a simple blogging platform with users, posts, and tags, supporting various relationship types (1:1, 1:n, n:n). It serves as a reference for building scalable FastAPI applications with clean, maintainable code.

## Concept
1. Minimal functionality.
2. Convincing architecture.
3. Easy to read.
4. Compatibility.
5. Versatility.

## base models
1. user
2. post [user (1 : n) post]
3. tag [post (n : n) tag]

## integrated with
1. Python3.9+
2. Fastapi 0.78.0
3. Database
   1. MySQL5.7+
   2. Migration with alembic
   3. pytest with real DB
   4. Load with two ways (eager, lazy)
   5. Modeling with schema (1:1, 1:n, n:n)
4. dependency-injector
   1. service-repository pattern
5. JWT authentication
   1. role separation each endpoint
6. Deployment
   1. container environment(k8s, docker)
   2. raw WAS(Web Application Server)

## commands

1. python -m venv cleanfastapi

2. db(alembic)
   1. `alembic upgrade head`: apply every migrations
   2. `alembic downgrade base`: rollback every migrations
   3. `alembic revision --autogenerate -m "revision_name"`: create new migration 
   4. `alembic history`: get alembic revision history
3. How to migration
   1. Create or modify models from `app/model/*.py`
   2. `alembic -x ENV=[dev|stage|prod] revision --autogenerate -m "revision_name"`
   3. Check auto generated migration file from `app/migrations/versions/*.py`
   4. `alembic -x ENV=[dev|stage|prod] upgrade head`  
      If ENV does not exist, it will be applied to the test.
4. server
   1. `uvicorn app.main:app --reload`: base
   2. options
      1. host: `--host 0.0.0.0`
      2. port: `--port 8000`
5. test
   1. `pytest`: base 
   2. `pytest --cov=app --cov-report=term-missing`: coverage with stdout
   3. `pytest --cov=app --cov-report=html`: coverage with html

## sample env
```dotenv
# mysql case
ENV=dev
DB=mysql
DB_USER=root
DB_PASSWORD=qwer1234
DB_HOST=localhost
DB_PORT=3306

# postgres case
ENV=dev
DB=postgresql
DB_USER=gyu
DB_PASSWORD=
DB_HOST=localhost
DB_PORT=5432
```

## references
1. [FastAPI official docs](https://fastapi.tiangolo.com/)
2. [alembic official tutorial](https://alembic.sqlalchemy.org/en/latest/tutorial.html)
3. [Dependency Injector](https://python-dependency-injector.ets-labs.org/)
