Got it 👍 You want a `README.md` for your GitHub repo that contains Kubernetes manifests and Docker image build instructions for **Counter-Strike 1.6 (cs-1-6)** server. Here’s a clean and professional draft:

---

# Counter-Strike 1.6 – Kubernetes Deployment

This repository provides Kubernetes manifests and Docker build instructions for running a **Counter-Strike 1.6 dedicated server** inside a Kubernetes cluster.

## 🚀 Features

* Dockerfile for building a lightweight CS 1.6 dedicated server image
* Kubernetes manifests for deployment, service, and persistent storage
* Configurable environment variables for game settings
* Supports external access via NodePort / LoadBalancer

---

## 📂 Repository Structure

```
.
├── manifests/                # Kubernetes manifests
│   ├── deployment.yaml       # CS 1.6 server Deployment
│   ├── service.yaml          # Exposes server (NodePort/LoadBalancer)
│   └── pvc.yaml              # Persistent volume for configs/maps
├── Dockerfile                # Image build instructions
├── .dockerignore
├── README.md
```

---

## 🔨 Build Docker Image

You can build the Docker image locally or push it to your own registry:

```bash
# Clone repo
git clone https://github.com/your-org/cs-1-6-k8s.git
cd cs-1-6-k8s

# Build Docker image
docker build -t your-dockerhub-user/cs16-server:latest .

# Push to registry
docker push your-dockerhub-user/cs16-server:latest
```

---

## ☸️ Deploy on Kubernetes

Make sure your cluster is running and `kubectl` is configured.

```bash
# Apply manifests
kubectl apply -f manifests/
```

Check status:

```bash
kubectl get pods
kubectl get svc
```

---

## 🎮 Connect to Server

1. Get the external IP / NodePort:

   ```bash
   kubectl get svc cs16-service
   ```

2. Open **Counter-Strike 1.6 client**

3. Add server with:

   ```
   <EXTERNAL-IP>:<PORT>
   ```

---

## ⚙️ Configuration

You can customize server settings by editing environment variables inside `deployment.yaml`:

```yaml
env:
  - name: SERVER_NAME
    value: "CS 1.6 Kubernetes Server"
  - name: RCON_PASSWORD
    value: "changeme"
  - name: MAX_PLAYERS
    value: "16"
  - name: MAP
    value: "de_dust2"
```

---

## 📌 Notes

* Default port is `27015/UDP`.
* Persistent storage (`pvc.yaml`) is optional, but recommended for saving configs and maps.
* Tested on Kubernetes v1.27+.

---

## 📜 License

This project is licensed under the MIT License.

---

Do you also want me to include a **sample `deployment.yaml` and `service.yaml` snippet** directly inside the README for quick copy-paste, or should we keep it minimal and only reference the `manifests/` folder?

