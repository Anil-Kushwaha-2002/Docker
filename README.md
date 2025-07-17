# 🐳Docker and Commands
**Docker -** Docker is a platform used to develop, ship, and run applications inside lightweight, portable, and isolated environments called containers.

## 🧠 Why Docker ?
- Lightweight: No need for full virtual machines. Uses less memory.
- Portable:- Runs the same way on any machine (local, server, cloud).
- Isolated:- Each container is separate. No conflicts.
- Fast Deployment:- Easily test and deploy apps.
- Consistency:- “It works on my machine” problem is solved

# 🐳  🛠️ Dockerfile → 🧱 Image → 🚢 Container → 📁Volume/🌐Network → 📦 docker-compose

- 🛠️ Dockerfile → 🧱 Image → 🚢 Container
-       ↘        ↘
-        📁 Volume  🌐 Network
-                ↓
-          📦 docker-compose


1️⃣ Dockerfile
🛠️ Define your app and environment
- **A Dockerfile** contains instructions to build a custom Docker image (base image, copy files, install dependencies, etc.).
- 📄 Example:
- Dockerfile
FROM python:3.10
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
- ✅ Command: `docker build -t myapp .`


2️⃣ Images
🧱 Blueprint of your app
- Docker builds an image from a Dockerfile (or pulls from Docker Hub).
- Contains the app code + OS + dependencies.
- ✅ Command: `docker images or docker pull nginx`

3️⃣ Containers
🚢 Running instance of an image
- A container is created from an image and actually runs the app.
- Stateless by default, isolated, and disposable.
- ✅ Command: `docker run -d -p 80:80 myapp`

4️⃣ Volumes
📁 Persistent storage for containers
- Data in containers is lost when they’re deleted — volumes solve that.
- Useful for databases, logs, etc.
- ✅ Command: `docker run -v mydata:/app/data myapp`

5️⃣ Networks
🌐 Communication between containers
- Needed when running multi-container apps (like web + database).
- You can create custom networks to isolate or group services.
- ✅ Command: `docker network create my_network`


6️⃣ docker-compose
📦 Orchestrate multi-container apps
- `docker-compose.yml` file defines multiple services (web, db, etc.).
- Runs everything together with one command.
- ✅ Command: `docker-compose up -d`



## 🚢 What is a Container ?
- A container is like a mini virtual machine that holds:
- Your application
- All dependencies
- Configuration files

## 📘 Core Docker Concepts
| Concept        | Description                                |
| -------------- | ------------------------------------------ |
| **Image**      | A snapshot of your app and its environment |
| **Container**  | A running instance of an image             |
| **Dockerfile** | Instructions to build a Docker image       |
| **Volume**     | Persistent storage for containers          |
| **Network**    | Allows communication between containers    |


## 🔁 Essential Docker Skills to Learn
| Skill                   | Why it matters                                  |
| ----------------------- | ----------------------------------------------- |
| Writing `Dockerfile`    | Define how your app runs                        |
| Using `docker-compose`  | Run multi-container apps (API + DB)             |
| Managing volumes        | Store DB/data persistently                      |
| Building/Tagging images | For versioning or pushing to DockerHub          |
| Docker networks         | For internal communication (e.g., `web` ↔ `db`) |


## 📦 Common Docker Commands
| Command                          | What it does                            |
| -------------------------------- | --------------------------------------- |
| `docker build .`                 | Builds a Docker image from a Dockerfile |
| `docker run IMAGE_NAME`          | Runs a container from an image          |
| `docker ps`                      | Shows running containers                |
| `docker stop CONTAINER_ID`       | Stops a container                       |
| `docker exec -it CONTAINER bash` | Enter into a running container          |

## 🌐 Networking
- `docker network ls`                           # List networks
- `docker network create my_network`            # Create custom network
- `docker network inspect my_network`
- `docker network rm my_network`
- `docker run --network=my_network <image>`




# 🔧🐳 Build and run a Django backend app in Docker. This is a real-world setup you’ll often use as a backend developer.
✅ Project: Dockerize a Django App
We’ll set up:
- A basic Django project
- Dockerfile
- docker-compose.yml (optional, for DB later)

## 📁 Folder Structure (after setup)
my-django-app/
├── Dockerfile
├── requirements.txt
├── manage.py
├── myproject/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py


# ✅ Step-by-Step Guide
# 1. Create Django Project Locally (optional)
Skip if you already have a Django project.

- mkdir my-django-app && cd my-django-app
- python -m venv venv && source venv/bin/activate
- pip install django
- django-admin startproject myproject.
- pip freeze > requirements.txt

# 2. Create Dockerfile
## Use official Python base image
`FROM python:3.11`

## Set working directory
`WORKDIR /app`

## Copy requirements & install
`COPY requirements.txt .`
`RUN pip install --no-cache-dir -r requirements.txt`

## Copy entire Django project
`COPY . .`

## Expose port 8000
`EXPOSE 8000`

## Run Django dev server
`CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]`

# 3. Build the Docker Image
`docker build -t django-app .`

# 4. Run the Django Container
`docker run -d -p 8000:8000 django-app`

Open in browser: http://localhost:8000
You should see the Django welcome page 🎉






