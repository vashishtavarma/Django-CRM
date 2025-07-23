# Django-CRM Project

Django-based Customer Record Management System. It enables users to register, log in, and manage customer records through a secure interface. Authenticated users can view, add, update, and delete customer data stored in the database. The system uses Django’s built-in authentication, form handling, and messaging framework to provide a smooth user experience within a single web interface.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [API Reference](#api-reference)
- [Templates](#templates)
- [Setup Instructions](#setup-instructions)
- [Environment Variables](#environment-variables)
- [Usage Examples](#usage-examples)
- [Workflow Instructions](#workflow-instructions)

---

## Project Overview

**Django-CRM** is a web-based customer record management system built with Django. It allows users to securely register, log in, and manage customer records (CRUD operations). The project leverages Django's authentication, forms, messaging, and admin interface for a robust user experience.

**Main Features:**
- User registration and authentication
- Add, update, delete, and view customer records
- Secure access (only authenticated users can manage records)
- Django admin for record management
- Responsive HTML templates

**Tech Stack:**
- Python 3.x
- Django 5.1.6
- MySQL (via `mysqlclient`)

---

## Architecture

- **Project Root**: `DCRM/` (Django project)
- **Main App**: `WEBSITE/`
- **Database**: MySQL (configured in `DCRM/settings.py`)
- **Templates**: Located in `WEBSITE/templates/`
- **Custom Scripts**: `mydb.py` (for DB creation)

### Django Apps
- `WEBSITE`: Contains models, forms, views, templates, and URLs for customer record management.

### Key Files
- `manage.py`: Django management utility
- `requirements.txt`: Python dependencies
- `mydb.py`: Script to create the MySQL database
- `DCRM/settings.py`: Project settings, DB config, installed apps
- `DCRM/urls.py`: Root URL routing
- `WEBSITE/models.py`: Customer record model
- `WEBSITE/forms.py`: User registration and record forms
- `WEBSITE/views.py`: Business logic for all main workflows
- `WEBSITE/urls.py`: App-specific routes
- `WEBSITE/templates/`: All HTML templates

---

## API Reference

### Models
#### `Record` (`WEBSITE/models.py`)
- Fields: `created_at`, `first_name`, `last_name`, `email`, `phone`, `city`, `address`, `state`, `zipcode`
- `__str__`: Returns "FirstName LastName"

### Forms
- `SignUpForm`: Extends `UserCreationForm` for user registration
- `AddRecordForm`: Model form for adding/editing records

### Views (`WEBSITE/views.py`)
- `home(request)`: Home page, login logic, record list
- `logout_user(request)`: Logs out user
- `register_user(request)`: Handles registration
- `customer_record(request, pk)`: View a single record
- `delete_record(request, pk)`: Delete a record
- `add_record(request)`: Add a new record
- `update_record(request, pk)`: Update a record

### URL Patterns (`WEBSITE/urls.py`)
- `/` : Home (login & record list)
- `/logout/` : Logout
- `/register/` : Register
- `/record/<pk>` : View record
- `/delete_record/<pk>` : Delete record
- `/add_record/` : Add record
- `/update_record/<pk>` : Update record

---

## Templates
Located in `WEBSITE/templates/`:
- `home.html`, `add_record.html`, `update_record.html`, `record.html`, `register.html`, `navbar.html`, `base.html`

---

## Setup Instructions

### 1. Clone the Repository
```sh
git clone https://github.com/vashishtavarma/Django-CRM.git
cd Django-CRM
```

### 2. Set Up Virtual Environment
```sh
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```sh
pip install -r requirements.txt
```

### 4. Configure MySQL Database
- Ensure MySQL is running.
- Update DB credentials in `DCRM/settings.py` if needed.
- Create the database:
```sh
python mydb.py
```

### 5. Run Migrations
```sh
python manage.py makemigrations
python manage.py migrate
```

### 6. Create Superuser (for admin)
```sh
python manage.py createsuperuser
```

### 7. Start the Development Server
```sh
python manage.py runserver
```

---

## Environment Variables
- `DJANGO_SECRET_KEY`: (Set in `DCRM/settings.py`)
- MySQL credentials: Set in `DCRM/settings.py` under `DATABASES`

---

## Usage Examples
- Visit `http://127.0.0.1:8000/` to use the CRM.
- Register a new user or log in.
- Add, update, or delete customer records.
- Access Django admin at `/admin/`.

---

## Workflow Instructions

- **Development:**
  - Activate your virtual environment before running any commands.
  - Use `python manage.py runserver` to start the dev server.
  - Use Django admin to manage records or users.

- **Database:**
  - Use `mydb.py` to create the initial database if it does not exist.
  - All models are migrated via Django's migration system.

- **Testing:**
  - Add tests in `WEBSITE/tests.py` and run with `python manage.py test WEBSITE`.

- **Deployment:**
  - Set `DEBUG = False` and configure allowed hosts in `DCRM/settings.py` for production.
  - Use a production-ready DB and web server.

---

> **Note:**
> - Do not commit secrets or credentials to version control.
> - For any issues, check Django and MySQL documentation.
