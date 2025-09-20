# 🐳Docker and Commands
**Docker -** Docker is a platform used to develop, ship, and run applications inside lightweight, portable, and isolated environments called containers.

## 🧠 Why Docker ?
- Lightweight: No need for full virtual machines. Uses less memory.
- Portable:- Runs the same way on any machine (local, server, cloud).
- Isolated:- Each container is separate. No conflicts.
- Fast Deployment:- Easily test and deploy apps.
- Consistency:- “It works on my machine” problem is solved

## 🐳  🛠️ Dockerfile → 🧱 Image → 🚢 Container → 📁Volume/🌐Network → 📦 docker-compos


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

7 Registries
8 Docker Contexts
9 docker-compose.yml
  
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




# 🔧🐳 Build and run a Simple python and Django backend app in Docker. This is a real-world setup you’ll often use as a backend developer.
# 1. Project: Dockerize a Simple python App
We’ll set up:
- A basic python project
- Dockerfile

## 📁 Folder Structure (after setup)
my-python-app/
├── Dockerfile
├── requirements.txt
├── app.py


# ✅ Step-by-Step Guide
## 1. Create Simple Project Locally (optional)
Skip if you already have a python project.

- `mkdir my-python-app && cd my-python-app`
- python -m venv venv && source venv/bin/activate
- `pip install django`  # if django used
- django-admin startproject myproject.
- pip freeze > requirements.txt

## 2. Create Dockerfile  
## `nano Dockerfile`  - #  Paste this code:-
- `FROM python:3.11`   # Use official Python base image
- `WORKDIR /app`   # Set working directory
- `COPY requirements.txt .`   # Copy requirements & install
- `RUN pip install --no-cache-dir -r requirements.txt`
- `COPY . .`    # Copy entire project
- `EXPOSE 8000`    # Expose port 8000
- `CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]`   # Run python dev serve


## 3. Build the Docker Image
`docker build -t my-python-app .`    # ( -t  or --tag :- Tag/naming the Docker Image )

## 4. Run the Django Container
- `docker run -d -p 8000:8000 my-python-app`    # ( -d 0r --detach :- Run container in background	Web servers, APIs, services)
- `docker run -d -p 8000:8000 --name python-app-container my-python-app`   # --name: gives your container a readable, custom name (Python-app-container)

Open in browser: http://localhost:8000
You should see the Django welcome page 🎉

# 2. Project: Dockerize a Django App
## ✅ Best for: Multi-file Projects like Django, with volumes, ports, and services. ( Or if allredy create app in vs code )
We’ll set up:
- A basic Django project
- `Dockerfile`
- `docker-compose.yml` (optional, for DB later)
- `requirements.txt`

# ✅ Step-by-Step Guide
- same as simple python app
## Automatically builds the Dockerfile and runs the app
`docker compose up --build`
- Open in browser: http://localhost:8000
You should see the Django welcome page 🎉

## Stop and remove services, networks, and volumes
`docker compose down`
## Won't see the logs/output directly in your terminal.
`docker logs container-id-or-name`

---
---

# ⚓ Orchestration (Kubernetes) in DevOps
---
##  1.🔹 What is Orchestration?
- **Orchestration** = Automating deployment, management, scaling, and networking of applications.  
- In DevOps, orchestration tools (like **Kubernetes**) help manage **containers** across multiple servers.  
---

##  2.🔹 What is Kubernetes (K8s) ?
- **Kubernetes (K8s)** is an **open-source container orchestration platform**.  
- Originally developed by Google, now maintained by CNCF.  
- It automates:
  - Deployment of containers  
  - Scaling up/down apps  
  - Load balancing traffic  
  - Self-healing (restart failed containers)
---  
##  3.🔹 Flow
📝 YAML Manifest → 📦 Pod → 🗂️ ReplicaSet → 🏷️ Deployment → 🌐 Service → 🌍 Ingress → ☁️ Cluster
---

##  4.📌 Core Concepts
- **📦 Pod** → Smallest deployable unit (runs one or more containers).
- **🗂️ ReplicaSet** → Ensures the desired number of Pods are running.
- **🏷️ Deployment** → Manages ReplicaSets & updates (rolling updates, rollback).
- **🌐 Service** → Stable networking to access Pods (ClusterIP, NodePort, LoadBalancer).
- **🌍 Ingress** → Routes external traffic into services (works with Nginx ingress controller).
- **☁️ Cluster** → A group of nodes (Master + Workers).
- **🖥️ Node** → A machine (VM/physical) in the cluster.
- **🔄 Scheduler** → Decides which Node runs which Pod.
- **⚙️ ConfigMap** → Store non-sensitive configs.
- **🔑 Secret** → Store sensitive data (passwords, tokens).
- **📦 Volume** → Persistent storage for Pods.
- **🔧 kubelet** → Agent running on each node, ensures Pods run.
---

##  5.📌 Example Workflow
- 📝 Write Deployment YAML (app + replicas).
- 📦 Pods created automatically via ReplicaSet.
- 🌐 Expose app with a Service.
- 🌍 Use Ingress + Nginx to manage external traffic.
- 📊 Monitor with Prometheus + Grafana.

---
##  6.🔹 Key Kubernetes Components
1. **Cluster** → Group of machines (nodes) running containers.  
2. **Node** → A worker machine (VM or physical server).  
3. **Pod** → Smallest unit in K8s, contains one or more containers.  
4. **Deployment** → Defines how many replicas of pods to run.  
5. **Service** → Exposes pods to the network (internal/external).  
6. **ConfigMap & Secret** → Store app configuration & sensitive data.  
7. **Ingress** → Manages external access (like Nginx reverse proxy).  

---

##  7.🔹 Why Kubernetes is Important in DevOps?
- Automates container lifecycle.
- Provides scalability (scale apps up/down easily).
- High availability with self-healing.
- Load balancing across multiple pods.
- Works seamlessly with Docker & cloud providers (AWS, Azure, GCP).
---

##  8.🔹 Basic Kubernetes Commands
```bash
kubectl cluster-info                                         # Check cluster info
kubectl get nodes                                            # Get all node
kubectl get pods                                             # Get all pods
kubectl create deployment myapp --image=nginx                # Deploy an app
kubectl expose deployment myapp --port=80 --type=NodePort    # Expose deployment as a service
kubectl scale deployment myapp --replicas=3                  # Scale deployment
kubectl delete deployment myapp                              # Delete deployment
```




