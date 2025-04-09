
# FastAPI + PostgreSQL on Kubernetes (Minikube & Rancher)

This project demonstrates how to deploy a FastAPI microservice backed by a PostgreSQL database on a Kubernetes cluster using Minikube and Rancher. The deployment includes persistent storage, secrets management, and internal networking.

## 🧰 Tech Stack
- **FastAPI** (Python web framework)
- **PostgreSQL** (Relational Database)
- **Kubernetes** (Minikube / Rancher)
- **Docker** (for containerization)
- **kubectl** (Kubernetes CLI)
- **YAML** (for Kubernetes manifests)

## 📁 Project Structure

```
fastapi-k8s-project/
├── fastapi/
│   ├── deployment.yaml        # FastAPI Deployment configuration
│   ├── service.yaml           # FastAPI Service for exposing API
│   └── fastapi-logs.txt       # Log sample from FastAPI
│   └── ingress.yaml           # Exposing the app via traefik ingress controller
├── postgres/
│   ├── statefulset.yaml       # PostgreSQL StatefulSet with volume
│   ├── service.yaml           # Internal ClusterIP Service for DB
│   └── pvc.yaml               # Rancher's default storage class(StorageClass)
│   └── postgresql-logs.txt    # Log sample from Postgresql
├── images/
│   ├── fastapi-docs.png
│   ├── fastapi-modify-users.png
│   └── fastapi-users.png
│   └── fastapi-userscount.png
│   └── fastapi.png
│   └── postman.png
├── Dockerfile                 # FastAPI container build config
├── requirements.txt           # Python dependencies for FastAPI
├── namespace.yaml             # Namespace to isolate project
├── pvc.yaml                   # PersistentVolumeClaim for DB
```

## 🚀 How It Works

1. **Namespace**: All objects are deployed under a dedicated namespace.
2. **PostgreSQL**: Deployed as a StatefulSet with persistent storage.
3. **Secrets**: Used to manage database credentials securely.
4. **FastAPI**: Built into a Docker image and deployed with environment variables for DB connection.
5. **Services**: PostgreSQL is exposed via a `ClusterIP`, and FastAPI via `NodePort` (default: `30000`).
6. **pgAdmin** (Optional): GUI to connect to the database using exposed ports.

## 🐳 Docker Image

The FastAPI service is built using a custom Dockerfile and pushed to Docker Hub:

```
docker build -t ranjithakj/fastapi:latest .
docker push ranjithakj/fastapi:latest
```

## 🛠 How to Deploy on Kubernetes

```bash
kubectl apply -f namespace.yaml
kubectl apply -f pvc.yaml
kubectl apply -f postgres/secret.yaml
kubectl apply -f postgres/statefulset.yaml
kubectl apply -f postgres/service.yaml
kubectl apply -f fastapi/deployment.yaml
kubectl apply -f fastapi/service.yaml
```

## 🌐 Accessing FastAPI

Access the API at:

```
http://localhost:30000/users
```

## 📸 Screenshots

![Pods Running](images/Screenshot_pods.png)
![Logs Output](images/Screenshot_logs.png)
![pgAdmin Access](images/Screenshot_pgadmin.png)

---

📝 Project created as part of a DevOps learning journey. Contributions, feedback, and stars are welcome!
