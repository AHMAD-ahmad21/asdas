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
- [Usage Examples](#usage-examples)
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
- **Testing:** pytest, Django test framework
- **Containerization:** Docker (optional)

## Getting Started

### Prerequisites

- Python 3.10+
- pip

### Installation

1. **Clone the repository**:

```bash
git clone https://github.com/yourusername/sky_pulse.git
cd sky_pulse
```

2. **Create & activate a virtual environment**:

```bash
python3 -m venv venv
source venv/bin/activate    # macOS/Linux
venv\Scripts\activate       # Windows
```

3. **Install dependencies**:

```bash
pip install -r requirements.txt
```

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

```bash
python3 manage.py migrate
```

2. **Create a superuser** (for Django admin, optional):

```bash
python3 manage.py createsuperuser
```

3. **Run the development server**:

```bash
python3 manage.py runserver
```

4. **Browse API docs**:  
   [http://localhost:8000/api-docs/swagger-ui/](http://localhost:8000/api-docs/swagger-ui/)

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

2. **Take the `access` token from the response**, then open your browser and go to:  
   [http://localhost:8000/api-docs/swagger-ui/](http://localhost:8000/api-docs/swagger-ui/)

3. **Authorize Swagger UI**:
   - Click on the **"Authorize"** button at the top right.
   - Paste your token like this:  
     ```
     Bearer <your_access_token>
     ```
   - Click **"Authorize"** again and close the dialog.

4. **Test the Weather APIs**:
   - Scroll down to the `/weather/` and `/weather/forecast/` sections.
   - Click **"Try it out"**, enter a city name (e.g., `Amman`), and execute the request.

## Screenshots

![Current Weather Example](current.png)  
![Forecast Example](forecast.png)
