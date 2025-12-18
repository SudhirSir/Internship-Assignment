## 📌 Project Overview

This project demonstrates a **production-style backend deployment** using **Flask**, **MongoDB**, **Docker**, and **Kubernetes (Minikube)**.

The objective of this assignment was to:

* Build a Flask REST API
* Connect it with MongoDB using authentication
* Containerize the application using Docker
* Deploy both services on Kubernetes
* Use persistent storage for MongoDB
* Apply resource limits and autoscaling
* Expose the application externally
* Document and verify the complete setup

---

## 🧰 Tech Stack Used

* **Backend:** Flask (Python)
* **Database:** MongoDB
* **Containerization:** Docker
* **Orchestration:** Kubernetes (Minikube)
* **Storage:** Persistent Volumes (PVC)
* **Autoscaling:** Horizontal Pod Autoscaler (HPA)

---

## ⚙️ Environment & Versions

* Operating System: Windows 11
* Docker Version: Docker Desktop
* Kubernetes Version: v1.30.0
* Minikube Version: v1.33.x
* Python Version: 3.9
* MongoDB Version: 6

---

## 📁 Project Structure

```
flask-mongodb-app/
│
├── app.py
├── Dockerfile
├── requirements.txt
│
├── k8s/
│   ├── flask-deployment.yaml
│   ├── flask-service.yaml
│   ├── mongo-secret.yaml
│   ├── mongo-pvc.yaml
│   ├── mongo-service.yaml
│   ├── mongo-statefulset.yaml
│   └── hpa.yaml
│
├── screenshots/
│   ├── pods.png
│   ├── services.png
│   ├── browser-output.png
│   └── api-data.png
│
└── README.md
```

---

## 🏗️ Architecture Overview

```
Client / Browser
        |
        |  NodePort (30007)
        v
Flask Service (NodePort)
        |
        v
Flask Deployment (2+ replicas)
        |
        v
MongoDB Service (ClusterIP / DNS)
        |
        v
MongoDB StatefulSet + PVC
```

---

## 🚀 Application Features

* `/` endpoint – basic response with timestamp
* `/data` endpoint

  * `POST` → insert data into MongoDB
  * `GET` → retrieve data from MongoDB

---

## 🐳 Dockerization

The Flask application is containerized using a Dockerfile based on `python:3.9-slim`.

Docker image is built locally and loaded into Minikube for Kubernetes deployment.

---

## ☸️ Kubernetes Deployment

### 🔹 Flask Application

* Deployed using **Deployment**
* Runs with **minimum 2 replicas**
* Resource requests and limits configured
* Exposed using **NodePort Service**

### 🔹 MongoDB

* Deployed using **StatefulSet**
* Authentication enabled using **Kubernetes Secrets**
* Persistent storage provided using **PVC**
* Resource requests and limits configured

---

## 🔐 MongoDB Authentication

MongoDB credentials are stored securely using Kubernetes Secrets.

Connection string used by Flask:

```
mongodb://admin:password123@mongo-service:27017/flask_db
```

---

## 🌐 Kubernetes DNS Resolution

Kubernetes provides an internal DNS system for service discovery.

In this project:

* Flask connects to MongoDB using the service name `mongo-service`
* Kubernetes automatically resolves this name to the MongoDB pod IP
* This ensures reliable communication even if pods restart or IPs change

This DNS-based communication is a core Kubernetes feature.

---

## 📈 Horizontal Pod Autoscaling (HPA)

Horizontal Pod Autoscaler is configured for the Flask application.

### Configuration:

* Minimum replicas: 2
* Maximum replicas: 5
* CPU utilization threshold: 70%

When CPU usage exceeds 70%, Kubernetes automatically scales up the Flask pods.
When load decreases, pods are scaled down.

This improves availability and efficient resource usage.

---

## 📊 Resource Requests & Limits

Both Flask and MongoDB have CPU and memory constraints configured.

### MongoDB Example:

* Requests:

  * CPU: 200m
  * Memory: 256Mi
* Limits:

  * CPU: 500m
  * Memory: 512Mi

This prevents resource starvation and ensures stable scheduling.

---

## 🧪 Testing & Verification

* Pods status verified using `kubectl get pods`
* Services verified using `kubectl get svc`
* Application accessed via browser using NodePort
* API tested using `/data` endpoint
* MongoDB connectivity verified end-to-end

Sample API response:

```json
[
  {
    "name": "Sudhir",
    "stage": "Docker network working"
  }
]
```

---

## 📸 Screenshots

Screenshots demonstrating successful deployment are included:

* Pods running (Flask + MongoDB)
* Services configuration
* Browser access
* API response from `/data`

All screenshots are available in the `screenshots/` folder.

---

## 🎯 Key Learnings

* Containerizing backend applications
* Deploying stateful and stateless services on Kubernetes
* Using StatefulSets with persistent storage
* Managing secrets securely
* Implementing autoscaling
* Debugging Kubernetes immutability constraints
* Production-style deployment practices

---

## 🏁 Conclusion

This project implements a complete, production-style backend system using Docker and Kubernetes.
All assignment requirements have been implemented, tested, and documented.

---

## 👤 Author

**Sudhir**
 
