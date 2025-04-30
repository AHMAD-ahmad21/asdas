## sky_pulse

**A Django REST API for fetching current weather and forecast data with JWT authentication.**

---

### Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)
  - [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Screenshots](#screenshots)

---

## Features

- User authentication with JSON Web Tokens (JWT)
- Retrieve current weather by location
- Retrieve 6-day forecast and hourly forecast
- Automatic fallback to client IP-based location lookup
- Interactive API documentation via Swagger/OpenAPI

## Tech Stack

- **Framework:** Django 4.2, Django REST Framework
- **Authentication:** djangorestframework-simplejwt
- **Schema & Docs:** drf-spectacular (OpenAPI + Swagger UI)
- **Weather Data:** weatherapi.com (live), ipinfo.io for geo-lookup
- **Database:** SQLite (default)
- **Testing:** Django test framework

## Getting Started

### Prerequisites

- Python 3.10+
- pip

### Installation

1. **Clone the repository**:

git clone https://github.com/yourusername/sky_pulse.git  
cd sky_pulse

2. **Create & activate a virtual environment**:

python3 -m venv venv  
source venv/bin/activate    # macOS/Linux  
venv\Scripts\activate     # Windows

3. **Install dependencies**:

pip install -r requirements.txt

### Environment Variables

Create a `.env` file in the project root with the following:

```dotenv
SECRET_KEY=your-django-secret-key
DEBUG=True
WEATHER_API_KEY=your-weatherapi-key
IPINFO_API_TOKEN=your-ipinfo-token
```

### Running the Application

1. **Apply migrations**:

python3 manage.py migrate

2. **Create a superuser** (for Django admin, optional):

python3 manage.py createsuperuser

3. **Run the development server**:

python3 manage.py runserver

4. **Browse API docs**: http://localhost:8000/api-docs/swagger-ui/

## API Endpoints

| Method | Endpoint                                | Description                                         |
| ------ | --------------------------------------- | --------------------------------------------------- |
| POST   | `/accounts/login/`                      | Obtain JWT access & refresh tokens                  |
| POST   | `/accounts/refresh/`                    | Refresh JWT access token                            |
| GET    | `/weather/?location=City`               | Current weather for `City` (auth required)          |
| GET    | `/weather/forecast/?location=City`      | 6-day & hourly forecast for `City` (auth required)  |

_All weather endpoints require an `Authorization: Bearer <access_token>` header._

## Usage Examples

1. **Login to get tokens**:

curl -X POST http://localhost:8000/accounts/login/ \  
  -H "Content-Type: application/json" \  
  -d '{"username": "user", "password": "pass"}'

2. **Get current weather**:

curl -H "Authorization: Bearer <ACCESS_TOKEN>" \  
  "http://localhost:8000/weather/?location=Amman"

3. **Get forecast**:

curl -H "Authorization: Bearer <ACCESS_TOKEN>" \  
  "http://localhost:8000/weather/forecast/?location=Amman"

## Screenshots

![Current Weather Example](.png)  
![Forecast Example](forecast.png)



