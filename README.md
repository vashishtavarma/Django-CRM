# Django-CRM Project

A secure Django-based Customer Record Management System that enables users to register, log in, and manage customer records through an authenticated interface. Features comprehensive CRUD operations with proper security measures and environment-based configuration.

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
git clone https://github.com/vashishtavarma/django-crm.git
cd django-crm
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

### 4. Configure Environment Variables
- Edit `.env` and set your actual values:
  - Set your database credentials
  - Configure other environment variables as needed

### 5. Configure MySQL Database
- Ensure MySQL is running.
- Create the database:
```sh
python mydb.py
```

### 6. Run Migrations
```sh
python manage.py makemigrations
python manage.py migrate
```

### 7. Create Superuser (for admin)
```sh
python manage.py createsuperuser
```

### 8. Start the Development Server
```sh
python manage.py runserver
```

---

## Environment Variables

Create a `.env` file in the project root with the following variables:

```env
# Django Configuration
DJANGO_SECRET_KEY=your-unique-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

# Database Configuration
DB_NAME=dcrmdatabase
DB_USER=root
DB_PASSWORD=your-secure-password
DB_HOST=localhost
DB_PORT=3306
```

**⚠️ Security Notes:**
- **Never commit `.env` files to version control**
- Generate a strong, unique `DJANGO_SECRET_KEY` for production
- Use strong database passwords
- Set `DEBUG=False` in production
- Configure appropriate `ALLOWED_HOSTS` for production

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
