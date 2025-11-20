# Use Python base image
FROM python:3.11-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update && \
    apt-get install -y build-essential libpq-dev --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# Copy requirements first
COPY requirements.txt /app/requirements.txt

# Install python dependencies
RUN pip install --no-cache-dir -r /app/requirements.txt

# Copy everything inside the build context (which is app/)
COPY . /app

ENV FLASK_ENV=production

EXPOSE 5000

CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]
