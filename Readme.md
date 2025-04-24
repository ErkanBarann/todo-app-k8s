## 📋 Project: To-Do Application – Kubernetes Deployment

### 📦 Goal:
This project aims to demonstrate how to deploy a simple **To-Do application** in a Kubernetes environment. The application consists of two main components:

- `web`: The frontend component that includes the user interface
- `db`: The backend component that stores the data (likely MySQL, PostgreSQL, etc.)

### 🧱 Architectural Components:

#### 1. **Database (db) Layer**
- `db-deployment.yaml` → Creates the database Pod.
- `db-service.yaml` → Makes the database accessible to the web application via a **ClusterIP service**.
- `db-pv.yaml` and `db-pvc.yaml` → Define persistent disk (PersistentVolume + PersistentVolumeClaim) for the database.
- `configmap.yaml` → Environment variables or configuration data (e.g. DB host, port) are defined here.

#### 2. **Application (web) Layer**
- `web-deployment.yaml` → Creates the Pod for the web application.
- `web-service.yaml` → Defines the service that exposes the web application (ClusterIP / NodePort).

#### 3. **Load Scaling**
- `hpa.yaml` → Horizontal Pod Autoscaler definition for the web application. The application becomes scalable under load (based on metrics such as CPU usage).

---

### 🌐 Service Types Used:
- **ClusterIP**: Communication between internal services (e.g. web ↔ db)
- (An Ingress could be added optionally.)

---

### ⚙️ Deployment Steps

```bash
# Create ConfigMap and PersistentVolumes
kubectl apply -f configmap.yaml
kubectl apply -f db-pv.yaml
kubectl apply -f db-pvc.yaml

# Start database components
kubectl apply -f db-deployment.yaml
kubectl apply -f db-service.yaml

# Deploy web application
kubectl apply -f web-deployment.yaml
kubectl apply -f web-service.yaml

# Horizontal Pod Autoscaler (HPA)
kubectl apply -f hpa.yaml
```


### 🗃️ File Structure Explanation

| File | Description |
|------|-------------|
| `configmap.yaml` | Contains environment variables |
| `db-deployment.yaml` | Database Pod |
| `db-service.yaml` | Database service |
| `db-pv.yaml` & `db-pvc.yaml` | Persistent data volumes |
| `web-deployment.yaml` | Web application Pod |
| `web-service.yaml` | Web application service |
| `hpa.yaml` | Automatic scaling under load |
| `Readme.md` | Project documentation (to be created) |

---

### ✅ Targeted Achievements:
- Multi-layer deployment with web + DB architecture
- Persistent storage of data
- Establishment of intra- and inter-cluster communication
- Ability to horizontally scale the application

