# ALX Project Nexus

This project uses Django with PostgreSQL as the backing database. The application reads configuration from a `.env` file using `django-environ`.

## Prerequisites

- Python 3.12 or later
- pip (bundled with Python) and `virtualenv` or `venv`
- PostgreSQL 14+ with `psql`
- (macOS) Xcode Command Line Tools for building psycopg dependencies

## Environment Variables

Create a file named `.env` in the project root (`/Users/okpunoremmanuel/Documents/ALX/alx-project-nexus/.env`). Use the sample below as a starting point and adjust the values for your own environment:

```
SECRET_KEY=change-me
DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost
CORS_ALLOWED_ORIGINS=http://localhost:3000

DATABASE_ENGINE=django.db.backends.postgresql
DATABASE_NAME=alx_project_nexus
DATABASE_USER=alx_user
DATABASE_PASSWORD=strong_password
DATABASE_HOST=127.0.0.1
DATABASE_PORT=5432
```

> `ALLOWED_HOSTS` and `CORS_ALLOWED_ORIGINS` accept comma-separated lists. Be sure to change `SECRET_KEY`, `DATABASE_PASSWORD`, and other sensitive values before deploying.

## PostgreSQL Setup

From your terminal, create the PostgreSQL role and database:

```bash
psql postgres
```

```sql
CREATE USER alx_user WITH PASSWORD 'strong_password';
CREATE DATABASE alx_project_nexus OWNER alx_user;
GRANT ALL PRIVILEGES ON DATABASE alx_project_nexus TO alx_user;
```

If you prefer using environment variables instead of editing the `.env` file directly, export them before starting the Django app (e.g. `export DATABASE_PASSWORD=...`). The `.env` file takes priority if both are set.

## Local Development Setup

```bash
git clone https://github.com/<your-org>/alx-project-nexus.git
cd alx-project-nexus
python3 -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

After the dependencies are installed and the database is ready, run the initial migrations:

```bash
python manage.py migrate
python manage.py createsuperuser  # optional, for admin access
```

Finally, start the development server:

```bash
python manage.py runserver
```

The API will be available at `http://127.0.0.1:8000/`.

## Troubleshooting

- If migrations fail, ensure the PostgreSQL service is running and the values in `.env` match your database credentials.
- If `psycopg` fails to install, install the PostgreSQL client libraries (macOS: `brew install postgresql`, Ubuntu: `sudo apt install libpq-dev`).
- Delete or regenerate the `.venv` directory if dependencies become inconsistent.
