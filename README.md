# Containerized microservice using nginx reverseproxy.

This project demonstrates a microservices-based architecture using Docker, Docker Compose, Nginx as a reverse proxy, and two lightweight services written in Go and Python (Flask). It's designed to reflect real-world DevOps practices such as service containerization, health checks, logging, and reverse proxy routing.

---

## 🚀 Project Structure

```
.
├── docker-compose.yml
├── nginx
│   ├── nginx.conf
│   └── Dockerfile
├── service_1
│   ├── main.go
│   └── Dockerfile
├── service_2
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
└── README.md
```

---

## 📆 Summary of Services

### Service 1: Go API

* Written in Go
* Provides `/ping` and `/hello` endpoints
* Uses native `net/http` package
* Dockerized and listens on port `8001`

### Service 2: Python Flask API

* Written in Python using Flask
* Also provides `/ping` and `/hello` endpoints
* Dockerized and listens on port `8002`

---

## Security Groups

Make sure your EC2 instance has inbound rules for ports:

22 (SSH)

80 (HTTP)

443 (HTTPS) [Optional]

8080 (Nginx Access)

## ⚙️ Docker Compose

`docker-compose.yml` orchestrates all 3 services:

* `service_1`: Builds Go code and exposes `8001`
* `service_2`: Builds Flask app and exposes `8002`
* `nginx`: Acts as reverse proxy, listens on `8080`, routes to other services

Both services include health checks using `curl` to `/ping`. Nginx only starts after both services are healthy.

---

## 📊 Nginx Configuration Highlights

* Routes:

  * `/service1/` → Service 1 (Go)
  * `/service2/` → Service 2 (Flask)

* Logs:

  * Custom log format added for access logging
  * Includes timestamp, HTTP path, status, bytes sent

* Example log entry:

  ```
  172.18.0.1 - [24/Jun/2025:12:35:42 +0000] "GET /service1/ping HTTP/1.1" status=200 bytes_sent=18
  ```

---

## 🌐 Endpoints

| Method | Path            | Description         |
| ------ | --------------- | ------------------- |
| GET    | /service1/ping  | Health check        |
| GET    | /service1/hello | Greeting from Go    |
| GET    | /service2/ping  | Health check        |
| GET    | /service2/hello | Greeting from Flask |

---

## ✨ Bonus Implementations

| Feature                     | Purpose                                                   |
| --------------------------- | --------------------------------------------------------- |
| Healthchecks via Docker     | Ensures containers are up and working before Nginx starts |
| Custom Nginx Access Logging | Helps debug and monitor traffic to each service           |
| Port Mapping                | Services exposed at host:8001, 8002, and Nginx on 8080    |
| Clean Code Structure        | Easily navigable and deployable microservice project      |

---



## 💡 Tips for Live Demo or Curl Testing

```bash
curl http://<your-ec2-ip>:8080/service1/ping
curl http://<your-ec2-ip>:8080/service2/hello
```









































