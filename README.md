
# 🎵 MP3 Converter Microservices Platform

A **production-style microservices project** that converts uploaded video files into MP3 audio using an **asynchronous event-driven pipeline**. The system is secured with **JWT authentication**, deployed on **Kubernetes (Minikube)**, and exposed via **NGINX Ingress**, supporting an end-to-end **upload → convert → store → notify → download** flow.

---

## 🚀 Features

* 🔐 **JWT-based Authentication & Authorization**
* 🌐 **API Gateway** for centralized routing
* ⚙️ **Asynchronous Conversion Pipeline** using RabbitMQ
* 🎧 **Video → MP3 conversion workers**
* 🗄️ **MongoDB GridFS** for large file storage
* 📩 **Notification service** after successful conversion
* ☸️ **Kubernetes deployment** (Minikube)
* 🔁 **NGINX Ingress** for domain-based routing
* 📦 Fully **Dockerized microservices**

---

## 🧱 Microservices Architecture

```
Client
  ↓
NGINX Ingress
  ↓
API Gateway
  ↓
Auth Service ── JWT
  ↓
Upload Service
  ↓
RabbitMQ Queue
  ↓
Converter Workers
  ↓
MongoDB GridFS
  ↓
Notification Service
```

---

## 🛠️ Tech Stack

* **Backend:** Python (FastAPI / Flask)
* **Auth:** JWT
* **Messaging:** RabbitMQ
* **Database:** MongoDB + GridFS
* **Containers:** Docker
* **Orchestration:** Kubernetes (Minikube)
* **Ingress:** NGINX Ingress Controller
* **Storage:** Persistent Volumes
* **CLI Testing:** cURL

---

## 📂 Services Overview

| Service              | Responsibility                    |
| -------------------- | --------------------------------- |
| Auth Service         | User login & JWT token generation |
| Gateway              | Central API routing               |
| Upload Service       | Accepts video uploads             |
| Converter Worker     | Converts video → MP3              |
| Notification Service | Sends conversion status           |
| RabbitMQ             | Async task queue                  |
| MongoDB GridFS       | Stores videos & MP3 files         |

---

## 🔐 Authentication Flow

1. User logs in using **Basic Auth**
2. Auth service issues a **JWT token**
3. JWT is passed in `Authorization: Bearer <token>` header
4. Protected routes validate JWT at the Gateway

---

## ⚙️ Local Setup (Minikube)

### 1️⃣ Start Minikube

```bash
minikube start
```

### 2️⃣ Enable Ingress

```bash
minikube addons enable ingress
```

### 3️⃣ Apply Kubernetes Manifests

```bash
kubectl apply -f ./manifests
```

### 4️⃣ Map Domain (Windows)

```txt
127.0.0.1 mp3converter.com
```

---

## 🐳 Docker Build & Deployment

```bash
docker build .
docker tag c7d84984726612 kushagra/notification:latest
docker push kushagra0717/notification:latest

kubectl delete -f ./manifests
kubectl apply -f ./manifests
```

---

## 🧪 API Testing (cURL)

### 🔑 Login

```bash
curl -X POST http://mp3converter.com/login \
-u videompconvertermessage@gmail.com
```

### 📤 Upload Video (with JWT)

```bash
curl -X POST http://mp3converter.com/upload \
-H "Authorization: Bearer <JWT_TOKEN>" \
-F "file=@testvideo.mp4"
```

### 🧪 Localhost Testing (Ingress)

```bash
curl --resolve "mp3converter.com:80:127.0.0.1" -X POST \
http://mp3converter.com/login \
-u videompconvertermessage@gmail.com:Admin123
```

```bash
curl --resolve "mp3converter.com:80:127.0.0.1" -X POST \
http://mp3converter.com/upload \
-H "Authorization: Bearer <JWT_TOKEN>" \
-F "file=@testvideo.mp4"
```

---

## 🔄 End-to-End Flow

1. User logs in → receives JWT
2. Video uploaded via Gateway
3. Upload service publishes job to RabbitMQ
4. Converter worker consumes job
5. MP3 generated and stored in GridFS
6. Notification service sends completion update
7. User downloads MP3

---

## 📌 Highlights

* Event-driven, **loosely coupled microservices**
* Handles **large files efficiently** with GridFS
* Designed for **scalability & fault tolerance**
* Real-world **DevOps + Backend system design**

---

## 📈 Future Improvements

* ✅ Download endpoint with signed URLs
* 📊 Prometheus + Grafana monitoring
* 📬 Email/Webhook notifications
* 🔐 OAuth2 support
* ☁️ Cloud deployment (EKS/GKE)

---

## 👤 Author

**Kushagra Agrawal**
Backend | DevOps | Distributed Systems
Docker • Kubernetes • RabbitMQ • MongoDB • JWT

---

