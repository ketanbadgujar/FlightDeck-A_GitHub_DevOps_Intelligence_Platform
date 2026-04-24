FROM python:3.12-slim

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY services/collector/ ./services/collector/
COPY services/metrics/ ./services/metrics/

ENV PYTHONPATH=/app/services/collector:/app/services/metrics

WORKDIR /app/services/metrics

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8002"]
