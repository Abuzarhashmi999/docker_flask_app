# docker_flask_app

A minimal Flask web application packaged with Docker — hands-on practice in **containerization**: taking an app plus everything it needs and sealing it into a portable image that runs identically on any machine.

## What it does
A single-route Flask server that returns a greeting at `/`. The app is intentionally tiny — the point of the project is the **packaging**, not the app.

## Tech stack
- Python 3.12 (slim base image)
- Flask
- Docker

## The Dockerfile, explained
```dockerfile
FROM python:3.12-slim      # start from a lightweight Python base image
WORKDIR /app               # set the working directory inside the container
COPY app.py .              # copy the app into the image
RUN pip install flask      # install dependencies inside the image
EXPOSE 5000                # document the port the app listens on
CMD ["python", "app.py"]   # command that runs when the container starts
```

## Run it yourself
```bash
# build the image from the Dockerfile
docker build -t cloud-health-app .

# run it, mapping your port 5000 to the container's port 5000
docker run -p 5000:5000 cloud-health-app
```
Then open http://localhost:5000 in a browser.

## Key concepts demonstrated
- **Image vs container** — an image is the blueprint; a container is a running instance of it
- **Port mapping** (`-p`) to reach a service running inside an isolated container
- **Reproducibility** — the Dockerfile regenerates the exact environment on any machine, so the image itself is disposable; the recipe is the real asset

---
*Part of my cloud & DevOps learning portfolio.*
