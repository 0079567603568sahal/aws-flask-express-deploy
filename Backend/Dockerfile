# Backend/Dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirement.txt .
RUN pip install --no-cache-dir -r requirement.txt

COPY . .
EXPOSE 5000

CMD ["gunicorn", "-w", "3", "-b", "0.0.0.0:5000", "app:app"]
