# ALX Travel App

## About the Project

The **alx_travel_app** project is a real-world Django application that serves as the foundation for a travel listing platform. This milestone focuses on setting up the initial project structure, configuring a robust database, and integrating tools to ensure API documentation and maintainable configurations. The aim is to equip learners with industry-standard best practices for starting and managing Django-based projects efficiently.

This milestone will teach you to set up a scalable backend, integrate MySQL for database management, and use Swagger for automated API documentation. These foundational steps are critical in preparing the application for future features and seamless team collaboration.

## Learning Objectives

As a professional developer, this task will enable you to:

1. **Master Advanced Project Initialization**:

   - Learn to bootstrap Django projects with modular, production-ready configurations
   - Employ environment variable management for secure and scalable settings

2. **Integrate Key Developer Tools**:

   - Set up and use Swagger (via drf-yasg) for API documentation
   - Implement CORS headers and MySQL configurations for robust API interactions

3. **Collaborate Effectively Using Git**:

   - Structure your projects for team collaboration with a version-controlled setup

4. **Adopt Industry Best Practices**:
   - Follow best practices in managing dependencies, database configurations, and application structure

## Requirements

To successfully complete this milestone, ensure you meet the following prerequisites:

- Familiarity with Django and Django REST Framework
- Knowledge of MySQL and database management
- Understanding of version control using Git
- A basic grasp of environment variable management using `django-environ`

## Project Structure

```
alx_travel_app/
├── alx_travel_app/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── listings/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── migrations/
├── requirements.txt
├── .env.example
├── .env
├── .gitignore
├── manage.py
└── README.md
```

## Key Highlights

### 1. Project Initialization

- Django project named **alx_travel_app**
- App named **listings** to encapsulate core functionalities

### 2. Dependency Management

Essential packages installed:

- `django`: Core framework for application development
- `djangorestframework`: REST API development
- `django-cors-headers`: Cross-Origin Resource Sharing setup
- `drf-yasg`: Swagger API documentation
- `celery` and `rabbitmq`: For future task queuing and background processes
- `django-environ`: Environment variable management
- `mysqlclient`: MySQL database connector

### 3. Settings Configuration

- Use `django-environ` to securely handle environment variables in `.env` files
- Configure MySQL as the primary database with proper connection handling
- Set up REST framework and CORS headers for API support

### 4. Swagger Integration

- Comprehensive API documentation
- Automatically documented APIs accessible at `/swagger/`
- Interactive API testing interface

### 5. Version Control

- Git repository initialized with proper `.gitignore`
- Clean commit history with meaningful messages

## Installation and Setup

### Prerequisites

1. **Python 3.8+** installed on your system
2. **MySQL** server running
3. **Git** for version control
4. **Virtual environment** (recommended)

### Step-by-Step Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/Nissau96/alx_travel_app.git
   cd alx_travel_app
   ```

2. **Create and activate virtual environment**:

   ```bash
   python -m venv venv

   # On Windows
   venv\Scripts\activate

   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**:

   ```bash
   cp .env.example .env
   ```

   Edit `.env` file with your configuration:

   ```env
   DEBUG=True
   SECRET_KEY=your-secret-key-here
   DB_NAME=alx_travel_app_db
   DB_USER=your-mysql-username
   DB_PASSWORD=your-mysql-password
   DB_HOST=localhost
   DB_PORT=3306
   ```

5. **Set up MySQL database**:

   ```sql
   CREATE DATABASE alx_travel_app_db;
   CREATE USER 'your-username'@'localhost' IDENTIFIED BY 'your-password';
   GRANT ALL PRIVILEGES ON alx_travel_app_db.* TO 'your-username'@'localhost';
   FLUSH PRIVILEGES;
   ```

6. **Run migrations**:

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

7. **Create superuser** (optional):

   ```bash
   python manage.py createsuperuser
   ```

8. **Start the development server**:
   ```bash
   python manage.py runserver
   ```

## Configuration Details

### Database Configuration

The project uses MySQL as the primary database. Configuration is handled through environment variables:

```python
# settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': env('DB_NAME'),
        'USER': env('DB_USER'),
        'PASSWORD': env('DB_PASSWORD'),
        'HOST': env('DB_HOST', default='localhost'),
        'PORT': env('DB_PORT', default='3306'),
    }
}
```

### REST Framework Configuration

```python
# settings.py
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.TokenAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 20,
}
```

### CORS Configuration

```python
# settings.py
CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
    "http://127.0.0.1:3000",
]

CORS_ALLOW_CREDENTIALS = True
```

### Swagger Configuration

```python
# settings.py
SWAGGER_SETTINGS = {
    'SECURITY_DEFINITIONS': {
        'Token': {
            'type': 'apiKey',
            'name': 'Authorization',
            'in': 'header'
        }
    }
}
```

## API Documentation

### Swagger UI

Access the interactive API documentation at:

- **Swagger UI**: `http://127.0.0.1:8000/swagger/`
- **ReDoc**: `http://127.0.0.1:8000/redoc/`

### API Endpoints

| Method | Endpoint         | Description                               |
| ------ | ---------------- | ----------------------------------------- |
| GET    | `/swagger/`      | Swagger UI documentation                  |
| GET    | `/redoc/`        | ReDoc documentation                       |
| GET    | `/admin/`        | Django admin interface                    |
| GET    | `/api/listings/` | List all listings (future implementation) |

## Dependencies

### Core Dependencies

```
Django>=4.2.0
djangorestframework>=3.14.0
django-cors-headers>=4.0.0
drf-yasg>=1.21.0
django-environ>=0.10.0
mysqlclient>=2.1.0
celery>=5.2.0
```

### Development Dependencies

```
pytest-django>=4.5.0
black>=23.0.0
flake8>=6.0.0
isort>=5.12.0
```

## Environment Variables

Create a `.env` file in the project root with the following variables:

```env
# Django Settings
DEBUG=True
SECRET_KEY=your-very-secret-key-here
ALLOWED_HOSTS=localhost,127.0.0.1

# Database Configuration
DB_NAME=alx_travel_app_db
DB_USER=your-mysql-username
DB_PASSWORD=your-mysql-password
DB_HOST=localhost
DB_PORT=3306

# Email Configuration (optional)
EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password

# Celery Configuration (for future use)
CELERY_BROKER_URL=redis://localhost:6379/0
CELERY_RESULT_BACKEND=redis://localhost:6379/0
```

## Development Workflow

### Running the Application

1. **Start MySQL server**
2. **Activate virtual environment**:
   ```bash
   source venv/bin/activate  # Linux/macOS
   venv\Scripts\activate     # Windows
   ```
3. **Start Django development server**:
   ```bash
   python manage.py runserver
   ```

### Code Quality

The project follows Django best practices:

- **PEP 8** code style
- **Environment-based configuration**
- **Proper error handling**
- **Security best practices**

### Testing

Run tests using:

```bash
python manage.py test
```

### Database Management

Common database operations:

```bash
# Create migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Create superuser
python manage.py createsuperuser

# Load sample data (when available)
python manage.py loaddata fixtures/sample_data.json
```

## Future Enhancements

This project is designed to be extended with:

1. **Listing Management**: Create, read, update, delete travel listings
2. **User Authentication**: JWT-based authentication system
3. **Search & Filtering**: Advanced search capabilities
4. **Booking System**: Reservation and booking functionality
5. **Payment Integration**: Stripe or PayPal integration
6. **Email Notifications**: Celery-based email system
7. **Image Management**: AWS S3 integration for media files
8. **API Rate Limiting**: Django REST framework throttling
9. **Caching**: Redis-based caching system
10. **Monitoring**: Application performance monitoring

## Troubleshooting

### Common Issues

1. **MySQL Connection Error**:

   - Ensure MySQL server is running
   - Check database credentials in `.env`
   - Verify database exists

2. **Migration Issues**:

   ```bash
   python manage.py makemigrations --empty listings
   python manage.py migrate --fake-initial
   ```

3. **Swagger Not Loading**:

   - Check `ALLOWED_HOSTS` in settings
   - Verify `drf-yasg` is in `INSTALLED_APPS`

4. **CORS Issues**:
   - Update `CORS_ALLOWED_ORIGINS` in settings
   - Check frontend URL configuration

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-feature`
3. Commit your changes: `git commit -am 'Add new feature'`
4. Push to the branch: `git push origin feature/new-feature`
5. Submit a pull request

### Code Style

- Follow PEP 8 guidelines
- Use meaningful variable and function names
- Add docstrings to functions and classes
- Write unit tests for new features

## License

This project is part of the ALX Backend curriculum and is intended for educational purposes.

## Support

For support and questions:

- Create an issue in the GitHub repository
- Check the Django documentation: https://docs.djangoproject.com/
- Check Django REST Framework documentation: https://www.django-rest-framework.org/

## Author

**Nissau96** - [GitHub Profile](https://github.com/Nissau96)

---

_This project demonstrates industry-standard practices for Django application development, including proper configuration management, API documentation, and database integration._
