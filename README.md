# Crypto Scraper

This project is a Django application for scraping cryptocurrency data using Celery for task management and Redis as a message broker.

## Features

- Scrapes cryptocurrency data from CoinMarketCap.
- Asynchronous task management using Celery.
- Real-time task status updates.
- REST API endpoints for starting and checking the status of scraping tasks.

## Prerequisites

- Python 3.8+
- Django 3.2+
- Redis
- Google Chrome (for Selenium)
- ChromeDriver

## Setup

### Clone the Repository

```bash
git clone https://github.com/yourusername/crypto_scraper.git
cd crypto_scraper
```

### Create a Virtual Environment

```bash
python -m venv myenv
source myenv/bin/activate # On Windows use `myenv\Scripts\activate`
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Configure Django Settings

Make sure your `crypto_scraper/settings.py` includes the following Celery configuration:

```python
CELERY_BROKER_URL = 'redis://localhost:6379/0'
CELERY_RESULT_BACKEND = 'redis://localhost:6379/0'
```

### Run Migrations

```bash
python manage.py migrate
```

### Start Redis Server

Make sure Redis is installed and running on your system. You can start the Redis server with the following command:

```bash
redis-server
```

### Run Celery Worker

In a separate terminal, navigate to the project directory and start the Celery worker:

```bash
celery -A crypto_scraper worker --loglevel=info
```

### Start Django Development Server

```bash
python manage.py runserver
```

## Project Structure

```plaintext
crypto_scraper/
├── crypto_scraper/
│   ├── __init__.py
│   ├── asgi.py
│   ├── celery.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
├── taskmanager/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tasks.py
│   ├── tests.py
│   ├── urls.py
│   ├── utils.py
│   ├── views.py
└── manage.py
```

## Usage

### API Endpoints

- **Start Scraping**: `POST /api/taskmanager/start/`
- **Check Scraping Status**: `GET /api/taskmanager/status/<task_id>/`

### Example Request

```bash
curl -X POST http://127.0.0.1:8000/api/taskmanager/start/
```

```bash
curl -X GET http://127.0.0.1:8000/api/taskmanager/status/<task_id>/
```

Replace `<task_id>` with the task ID received from the start endpoint.

## Contributing

1. Fork the repository.
2. Create your feature branch: `git checkout -b my-new-feature`.
3. Commit your changes: `git commit -am 'Add some feature'`.
4. Push to the branch: `git push origin my-new-feature`.
5. Submit a pull request.

## License

This project is licensed under the MIT License.
```

### Save the File

Save this content in a file named `README.md` in the root directory of your project. This file provides a comprehensive guide on setting up and running your Django project with Celery and Redis for scraping cryptocurrency data.
