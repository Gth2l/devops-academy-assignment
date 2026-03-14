# Section 1 – Task B: Dockerize a Python Web App

## Summary

This task contains a simple Python web application built with Flask and packaged into a Docker container.

The implementation demonstrates:
- a basic Flask web application,
- Docker-based containerization,
- exposed application port,
- local execution with Docker Compose,
- basic verification through HTTP requests.

## Project Files

- `app.py` – Flask application source code
- `requirements.txt` – Python dependencies
- `Dockerfile` – Docker image definition
- `docker-compose.yml` – local container startup configuration
- `.dockerignore` – excluded files from Docker build context

## Application Endpoints

- `/` – returns a JSON response confirming the application is running
- `/healthz` – returns a simple health status response

## How to Run

Run the application from the `task-b-docker-flask` directory:

```bash
docker compose up --build
```
## How to Verify

```
curl http://localhost:5000
curl http://localhost:5000/healthz
```
Expected responses:
```
{"message":"Flask app is running inside Docker","status":"ok"}
```
```
{"status":"healthy"}
```

Port Exposure
The application runs on port 5000 inside the container.

Gunicorn

Gunicorn is used as the application server instead of the Flask development server.

Multi-Stage Build

A multi-stage build was not necessary for this implementation because the application is small and already uses the lightweight python:3.12-slim base image.

