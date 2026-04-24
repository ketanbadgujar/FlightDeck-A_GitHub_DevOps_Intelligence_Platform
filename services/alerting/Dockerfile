FROM python:3.12-slim

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/libs/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY services/collector/ ./services/collector/
COPY services/alerting/ ./services/alerting/

ENV PYTHONPATH=/app/services/collector:/app/services/alerting

WORKDIR /app/services/alerting

CMD ["python", "main.py"]
