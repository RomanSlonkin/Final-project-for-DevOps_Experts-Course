![Screenshot of QuakeWatch](static/experts-logo.svg)

# QuakeWatch

**QuakeWatch** is a Flask-based web application designed to display real-time and historical earthquake data. It visualizes earthquake statistics with interactive graphs and provides detailed information sourced from the USGS Earthquake API. Built using an object‑oriented design and modular structure, QuakeWatch separates templates, utility functions, and route definitions, making it both scalable and maintainable. The application is also containerized with Docker for easy deployment.

## Features

- **Real-Time & Historical Data:** Fetches earthquake data from the USGS API.
- **Interactive Graphs:** Displays earthquake counts over various time periods (e.g., last 30 days, 5-year view) using Matplotlib.
- **Top Earthquake Events:** Shows the top 5 worldwide earthquakes (last 30 days) by magnitude.
- **Recent Earthquake Details:** Highlights the most recent earthquake event.
- **RESTful Endpoints:** Provides endpoints for health checks, status, connectivity tests, and raw data.
- **Clean UI:** Built with Bootstrap 5, featuring a professional navigation bar with a logo.
- **Dockerized:** Easily containerized for streamlined deployment.

## Project Structure

```
QuakeWatch/
├── app.py                  # Application factory and entry point
├── dashboard.py            # Blueprint & route definitions using OOP style
├── utils.py                # Helper functions and custom Jinja2 filters
├── requirements.txt        # Python dependencies
├── static/
│   └── experts-logo.svg    # Logo file used in the UI
└── templates/              # Jinja2 HTML templates
    ├── base.html           # Base template with common layout and navigation
    ├── main_page.html      # Home page content
    └── graph_dashboard.html# Dashboard view with graphs and earthquake details
```

# Phase1 Flask Application

## How to Build and Run the Containerized Application

### 1. Build the Docker Image

Open a terminal in the project directory (where the Dockerfile is located) and run:

```sh
docker build -t phase1-flask-app .
```

### 2. Run the Docker Container

```sh
docker run -d -p 5000:5000 --name phase1-flask-app phase1-flask-app
```

This will start your Flask application inside a Docker container, accessible at [http://localhost:5000](http://localhost:5000).

### 3. Stopping the Container

To stop the running container:

```sh
docker stop phase1-flask-app
```

To remove the container:

```sh
docker rm phase1-flask-app
```

---

## Optional: Using Docker Compose

If you prefer to use Docker Compose, run:

```sh
docker compose up --build
```
or (for older versions):
```sh
docker-compose up --build
```

This will build the image (if needed) and start the container as defined in `docker-compose.yml`.

---

## Notes

- Ensure you have a `requirements.txt` file in the project directory listing your Python dependencies.
- Make sure Docker is installed and running on your machine.