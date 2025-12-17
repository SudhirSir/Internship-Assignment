## 📌 Project Overview

This project demonstrates an **end-to-end containerized backend system** using **Flask**, **MongoDB**, **Docker**, and **Kubernetes (Minikube)**.

The goal was to:

* Containerize a Flask REST API
* Deploy it on Kubernetes with multiple replicas
* Deploy MongoDB as a **StatefulSet** with persistent storage
* Secure database credentials using **Kubernetes Secrets**
* Expose the application externally using a **NodePort Service**
* Validate end-to-end communication between Flask and MongoDB

This setup closely resembles **real-world production architecture**.

---

## 🏗️ Architecture Overview (Text Diagram)

```
Browser / Client
       |
       |  NodePort (30007)
       v
+---------------------+
|  Flask Service      |
|  (NodePort)         |
+---------------------+
          |
          | Kubernetes Service (DNS)
          v
+---------------------+
| Flask Deployment    |
| 2 Replicas          |
+---------------------+
          |
          | Internal ClusterIP
          v
+---------------------+
| MongoDB Service     |
| (Headless)          |
+---------------------+
          |
          v
+---------------------+
| MongoDB StatefulSet |
| Persistent Volume   |
+---------------------+
```

---

## 🧰 Tech Stack Used

* **Backend:** Flask (Python)
* **Database:** MongoDB
* **Containerization:** Docker
* **Orchestration:** Kubernetes (Minikube)
* **Storage:** Persistent Volumes (PVC)
* **Secrets:** Kubernetes Secrets

 ---
 
 ## ⚙️ Environment & Versions

- Operating System: Windows 11
- Docker Version: Docker Desktop (latest)
- Kubernetes Version: v1.30.0
- Minikube Version: v1.33.1
- Python Version: 3.9
- MongoDB Version: 6


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
│
└── README.md
```

---

## 🚀 Setup & Deployment Steps

### 1️⃣ Build Docker Image

```bash
docker build -t sudhir/flask-mongo-app:latest .
```

### 2️⃣ Start Minikube

```bash
minikube start --driver=docker
```

### 3️⃣ Load Image into Minikube

```bash
minikube image load sudhir/flask-mongo-app:latest
```

---

## 🐳 Kubernetes Deployment

### 🔹 Deploy Flask Application

```bash
kubectl apply -f k8s/flask-deployment.yaml
kubectl apply -f k8s/flask-service.yaml
```

### 🔹 Deploy MongoDB

```bash
kubectl apply -f k8s/mongo-secret.yaml
kubectl apply -f k8s/mongo-pvc.yaml
kubectl apply -f k8s/mongo-service.yaml
kubectl apply -f k8s/mongo-statefulset.yaml
```

---

## 🔐 MongoDB Authentication

MongoDB credentials are stored securely using **Kubernetes Secrets**:

* Username: `admin`
* Password: `password123`

Flask connects using:

```
mongodb://admin:password123@mongo-service:27017/flask_db
```

---

## 🌐 Access the Application

### Option 1: Using Minikube IP

```bash
minikube ip
```

Open in browser:

```
http://<minikube-ip>:30007
```

### Option 2: Port Forwarding

```bash
kubectl port-forward service/flask-service 5000:5000
```

Browser:

```
http://localhost:5000
```

---

## 🧪 API Testing

### Insert Data

```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"name":"Sudhir","stage":"Docker network working"}' \
http://localhost:5000/data
```

### Fetch Data

```bash
curl http://localhost:5000/data
```

### Sample Output

```json
[
  {
    "name": "Sudhir",
    "stage": "Docker network working"
  }
]
```

---

## 💡 Key Kubernetes Concepts Demonstrated

* **Deployment:** Flask runs with multiple replicas
* **Service (NodePort):** External access
* **StatefulSet:** MongoDB with stable identity
* **Persistent Volumes:** Data survives pod restarts
* **Secrets:** Secure credential management
* **Internal DNS:** Service-based communication

---

## 🎯 Why StatefulSet for MongoDB?

* MongoDB is **stateful**
* Needs stable network identity
* Requires persistent storage
* StatefulSet ensures ordered startup and stable volumes

---

## 📈 Learning Outcomes

* Real-world Kubernetes deployment workflow
* Debugging image pull issues in Minikube
* Understanding service discovery via Kubernetes DNS
* Secure application design using Secrets
* Production-style container orchestration

---

## 🏁 Conclusion

This project demonstrates a **complete, production-style backend system** deployed on Kubernetes.
It highlights containerization, orchestration, persistence, and secure communication between services.

Note: All Screenshots are attached in the screenshots/ folder.


---

## 👤 Author

**Sudhir**
 
