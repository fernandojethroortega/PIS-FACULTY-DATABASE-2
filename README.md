# PIS Faculty Management System

A secure, full-stack, HTTPS-ready Faculty Management System for Pagudpud Integrated School and Philippine public schools.

## Core Features
- Administrator and Teacher role-based access control
- Secure teacher registration, login, password hashing, CSRF protection, XSS-safe Django templates, ORM-based SQL injection prevention, secure sessions
- Admin approval for teacher accounts
- Teacher profile management with employee number, complete name, sex, birth date, age, address, contact, email, position, department, specialization, advisory class, grade level, years in service, and employment status
- Teaching load and class schedule encoding
- Automatic teacher schedule conflict detection
- Automatic room conflict detection
- Real-Time Vacant Teacher Tracking System with Available Now, Currently Teaching, Teaching-Related Task, On Break, Without Schedule, Next Class, Last Class, free teacher count, and busy teacher count
- Teacher directory, search, filters, CSV export, audit trail, dark mode, live clock, responsive DepEd-inspired interface
- Admin console with import/export support for Excel/CSV through django-import-export

## Local Setup
```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Open: `http://127.0.0.1:8000`

## Production HTTPS Notes
Set these in `.env`:
```env
DEBUG=False
SECRET_KEY=your-long-random-secret
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com
CSRF_TRUSTED_ORIGINS=https://yourdomain.com,https://www.yourdomain.com
DATABASE_URL=postgres://user:password@host:5432/dbname
SECURE_SSL_REDIRECT=True
```
Use Nginx or your hosting provider SSL/TLS certificate. On Railway, Render, Azure, AWS, or VPS, put the app behind HTTPS and run with Gunicorn.

## Render/Railway Start Command
```bash
python manage.py migrate && python manage.py collectstatic --noinput && gunicorn config.wsgi:application
```

## Recommended Production Database
PostgreSQL is recommended. SQLite is acceptable only for local testing.

## Security Checklist
- Use strong SECRET_KEY
- Set DEBUG=False
- Use HTTPS
- Use PostgreSQL
- Restrict admin access
- Approve teacher accounts manually
- Use strong passwords
- Back up database and media uploads regularly

## Future Integrations
The project is structured for future OAuth/SSO integration with Google Workspace, Microsoft 365, and DepEd-related systems.
