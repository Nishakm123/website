# Dockerfile for Django Application with Gunicorn

# Use the official Python 3.11 image
FROM python:3.11-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory
WORKDIR /app

# Install the PostgreSQL client
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    postgresql-client \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Copy the requirements file
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the project files
COPY . .

# Run migrations and collect static files
CMD ["/bin/sh", "-c", "python manage.py migrate && python manage.py collectstatic --noinput && gunicorn your_project_name.wsgi:application --bind 0.0.0.0:8000"]
