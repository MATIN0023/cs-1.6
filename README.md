Got it 👍 I’ll remove the `image-cs-1-6/` part since you don’t want to keep Docker image build instructions in the README. Here’s the **cleaned-up README.md** with **Helm chart** instructions only:

```md
# cs-1.6 · Kubernetes / Helm Counter-Strike 1.6 Server

This repository contains **Kubernetes manifests** and a **Helm chart** to deploy a **Counter-Strike 1.6** dedicated server on Kubernetes.

---

## 📂 Repository Structure

```

.
├── deployment-ingress-cluster-cs-1.6.yaml    # Kubernetes manifest for deployment + ingress setup
├── configmap.yaml                             # ConfigMap with server.cfg + users.ini
├── helm-chart/                                # Helm chart for CS 1.6 deployment
└── README.md

````

---

## ☸️ Kubernetes Deployment (manifests)

You can deploy using the plain Kubernetes manifests:

```bash
kubectl apply -f configmap.yaml
kubectl apply -f deployment-ingress-cluster-cs-1.6.yaml
````

Then verify:

```bash
kubectl get pods
kubectl get svc
kubectl get ingress
```

---

## 📦 Helm Chart

This repo includes a Helm chart under `helm-chart/` to simplify installation, upgrades, and customization via values. Use it to deploy (or upgrade) your server setup more cleanly.

### Install with Helm

```bash
helm install cs16 ./helm-chart -n matin --create-namespace
```

### Upgrade / Change Config

```bash
helm upgrade cs16 ./helm-chart -n matin
```

### Example `values.yaml`

```yaml
replicaCount: 1

image:
  repository: yourdockeruser/cs16-server
  tag: latest

service:
  type: LoadBalancer
  gamePort: 27015
  httpPort: 80

config:
  serverCfg: |
    hostname "intellare"
    sv_name "intellare"
    rcon_password "intellare"
    maxplayers "32"
    mp_roundtime "4"
    mp_startmoney "800"
    # … rest of server.cfg …
  usersIni: |
    "damesstos" "" "abcdefghijklmnopqrstu" ""
    "behnam" "" "abcdefghijklmnopqrstu" ""
    "mehrdad" "" "abcdefghijklmnopqrstu" ""
```

You can override these in your own `my-values.yaml`:

```bash
helm install cs16 ./helm-chart -f my-values.yaml -n matin
```

---

## 🎮 Connect to the Server

1. Get the external IP (or hostname) from your Service or Ingress:

   ```bash
   kubectl get svc -n matin
   ```

2. In **Counter-Strike 1.6 client**, join with:

   ```
   <EXTERNAL-IP>:27015
   ```

---

## ⚙️ Notes

* All server settings (`server.cfg` and `users.ini`) are controlled via Helm `values.yaml`.
* Default port: **27015/UDP**
* Make sure your cloud firewall or cluster allows UDP traffic on this port.
* Works with Kubernetes v1.27+

---

## 📝 License

This project is licensed under the **MIT License**.
(Include `LICENSE` file in repo.)

---

👉 Do you also want me to **generate the full `helm-chart/` folder structure** (with `Chart.yaml`, `values.yaml`, and templates) so you can just drop it into your repo?

