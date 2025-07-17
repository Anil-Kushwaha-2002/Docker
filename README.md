# Docker and Commands
**Docker -** Docker is a platform used to develop, ship, and run applications inside lightweight, portable, and isolated environments called containers.

## 🧠 Why Docker ?
✅ Lightweight: No need for full virtual machines. Uses less memory.
✅ Portable:- Runs the same way on any machine (local, server, cloud).
✅ Isolated:- Each container is separate. No conflicts.
✅ Fast Deployment:- Easily test and deploy apps.
✅ Consistency:- “It works on my machine” problem is solved

## 🧱 What is a Container ?
- A container is like a mini virtual machine that holds:
- Your application
- All dependencies
- Configuration files

# 1. Core Docker Concepts
| Concept        | Description                                |
| -------------- | ------------------------------------------ |
| **Image**      | A snapshot of your app and its environment |
| **Container**  | A running instance of an image             |
| **Dockerfile** | Instructions to build a Docker image       |
| **Volume**     | Persistent storage for containers          |
| **Network**    | Allows communication between containers    |



# 2. Essential Docker Skills to Learn
| Skill                   | Why it matters                                  |
| ----------------------- | ----------------------------------------------- |
| Writing `Dockerfile`    | Define how your app runs                        |
| Using `docker-compose`  | Run multi-container apps (API + DB)             |
| Managing volumes        | Store DB/data persistently                      |
| Building/Tagging images | For versioning or pushing to DockerHub          |
| Docker networks         | For internal communication (e.g., `web` ↔ `db`) |



📦 Common Docker Commands

| Command                          | What it does                            |
| -------------------------------- | --------------------------------------- |
| `docker build .`                 | Builds a Docker image from a Dockerfile |
| `docker run IMAGE_NAME`          | Runs a container from an image          |
| `docker ps`                      | Shows running containers                |
| `docker stop CONTAINER_ID`       | Stops a container                       |
| `docker exec -it CONTAINER bash` | Enter into a running container          |



## Build and run a Django backend app in Docker. This is a real-world setup you’ll often use as a backend developer. 🔧🐳
✅ Project: Dockerize a Django App
We’ll set up:
A basic Django project
Dockerfile
docker-compose.yml (optional, for DB later)

📁 Folder Structure (after setup)

my-django-app/
├── Dockerfile
├── requirements.txt
├── manage.py
├── myproject/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py


✅ Step-by-Step Guide
🔹 1. Create Django Project Locally (optional)
Skip if you already have a Django project.

mkdir my-django-app && cd my-django-app
python -m venv venv && source venv/bin/activate
pip install django
django-admin startproject myproject .
pip freeze > requirements.txt

🔹 2. Create Dockerfile
# Use official Python base image
FROM python:3.11

# Set working directory
WORKDIR /app

# Copy requirements & install
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy entire Django project
COPY . .

# Expose port 8000
EXPOSE 8000

# Run Django dev server
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

🔹 3. Build the Docker Image
docker build -t django-app .

🔹 4. Run the Django Container
docker run -d -p 8000:8000 django-app

Open in browser: http://localhost:8000
You should see the Django welcome page 🎉






