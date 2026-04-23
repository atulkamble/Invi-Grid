# 🐳 Docker Scenario-Based Interview Q&A

---

## 🔹 1. Container Keeps Restarting (CrashLoop-like behavior)

**Scenario:**
Your Docker container keeps restarting continuously.

**Answer:**

```bash
docker ps -a
docker logs <container_id>
docker inspect <container_id>
```

**Root Causes:**

* Application crash
* Wrong CMD/ENTRYPOINT
* Missing env variables
* Port conflicts

**Fix Example:**

```bash
docker run -d -e DB_HOST=mysql myapp
```

---

## 🔹 2. Image Size Too Large

**Scenario:**
Your Docker image is 2GB → slow CI/CD pipeline.

**Solution:**

* Use multi-stage builds
* Use alpine base image
* Remove unnecessary packages

```dockerfile
FROM node:18 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
```

---

## 🔹 3. Container Cannot Connect to Another Container

**Scenario:**
App container cannot connect to DB container.

**Fix:**

```bash
docker network create mynet

docker run -d --name db --network mynet mysql
docker run -d --name app --network mynet myapp
```

Use container name as hostname:

```bash
DB_HOST=db
```

---

## 🔹 4. Data Lost After Container Restart

**Scenario:**
Database data disappears after restart.

**Solution: Use Volumes**

```bash
docker volume create db_data

docker run -d -v db_data:/var/lib/mysql mysql
```

---

## 🔹 5. Container Works Locally but Fails in Server

**Scenario:**
Runs fine on laptop, fails in EC2.

**Possible Issues:**

* Architecture mismatch (ARM vs x86)
* Missing env variables
* Network/security group issue

**Fix:**

```bash
docker buildx build --platform linux/amd64 -t myapp .
```

---

## 🔹 6. Port Not Accessible

**Scenario:**
App runs but not accessible via browser.

**Fix:**

```bash
docker run -p 8080:80 nginx
```

Check:

```bash
netstat -tulnp
```

---

## 🔹 7. Too Many Containers Running → High CPU

**Scenario:**
System overloaded due to many containers.

**Solution:**

```bash
docker stats
docker stop $(docker ps -q)
```

Limit resources:

```bash
docker run -d --cpus="1" --memory="512m" nginx
```

---

## 🔹 8. Secrets Exposed in Dockerfile

**Scenario:**
Credentials hardcoded.

❌ Bad:

```dockerfile
ENV DB_PASSWORD=admin123
```

✅ Fix:

```bash
docker run -e DB_PASSWORD=secure myapp
```

---

# ☸️ Kubernetes Scenario-Based Interview Q&A

---

## 🔹 1. Pod in CrashLoopBackOff

**Scenario:**
Pod keeps restarting.

**Debug Steps:**

```bash
kubectl get pods
kubectl describe pod <pod>
kubectl logs <pod>
```

**Common Issues:**

* App crash
* ConfigMap missing
* DB not reachable

---

## 🔹 2. Pod Running but Not Accessible

**Scenario:**
Pod is running but no access.

**Check Service:**

```bash
kubectl get svc
```

Fix:

```yaml
type: NodePort
```

Or:

```yaml
type: LoadBalancer
```

---

## 🔹 3. Application Cannot Reach Database

**Scenario:**
Microservice cannot connect to DB.

**Check:**

```bash
kubectl get svc
kubectl exec -it <pod> -- ping mysql
```

Fix:

* Use correct service name
* Check DNS:

```bash
mysql.default.svc.cluster.local
```

---

## 🔹 4. Deployment Not Updating

**Scenario:**
New image not deployed.

**Fix:**

```bash
kubectl set image deployment/app app=nginx:latest
```

Or:

```bash
kubectl rollout restart deployment app
```

---

## 🔹 5. Pod Stuck in Pending

**Scenario:**
Pod not scheduled.

**Check:**

```bash
kubectl describe pod <pod>
```

**Reasons:**

* No resources
* NodeSelector issue
* Taints/Tolerations

---

## 🔹 6. High CPU Usage in Cluster

**Scenario:**
Cluster under heavy load.

**Check:**

```bash
kubectl top nodes
kubectl top pods
```

**Fix:**

* Enable HPA

```bash
kubectl autoscale deployment app --cpu-percent=50 --min=1 --max=5
```

---

## 🔹 7. Config Changes Not Reflecting

**Scenario:**
Updated ConfigMap but app still using old config.

**Fix:**

```bash
kubectl rollout restart deployment app
```

---

## 🔹 8. Secret Management Issue

**Scenario:**
App cannot read secret.

**Fix:**

```bash
kubectl create secret generic db-secret \
  --from-literal=password=admin123
```

Mount:

```yaml
env:
- name: DB_PASSWORD
  valueFrom:
    secretKeyRef:
      name: db-secret
      key: password
```

---

## 🔹 9. Pod Deleted Automatically

**Scenario:**
Pod disappears after deletion.

👉 Controlled by Deployment/ReplicaSet

Check:

```bash
kubectl get deployment
```

---

## 🔹 10. Rolling Update Failed

**Scenario:**
Deployment update breaks app.

**Rollback:**

```bash
kubectl rollout undo deployment app
```

---

## 🔹 11. Logs Not Available

**Scenario:**
Logs missing after restart.

**Fix:**

```bash
kubectl logs <pod> --previous
```

---

## 🔹 12. External Traffic Not Reaching Cluster

**Scenario:**
App exposed but not reachable.

**Check:**

* LoadBalancer IP
* Security group / firewall
* Ingress config

---

## 🔹 13. Persistent Storage Not Working

**Scenario:**
Data not saved.

Check:

```bash
kubectl get pvc
kubectl get pv
```

---

## 🔹 14. Multi-Container Pod Issue

**Scenario:**
Sidecar container fails.

Debug:

```bash
kubectl logs <pod> -c <container>
```

---

## 🔹 15. Node Not Ready

**Scenario:**
Worker node down.

Check:

```bash
kubectl get nodes
```

Fix:

* Restart kubelet
* Check cloud instance

---

# 🚀 Bonus: Real Interview Level Scenario

---

## 🔥 Scenario: Production Outage

**Problem:**

* App down
* Pods restarting
* CPU spike

**Approach (SRE Mindset):**

1. Check cluster:

```bash
kubectl get pods -A
```

2. Identify failing pods:

```bash
kubectl describe pod
kubectl logs
```

3. Check resources:

```bash
kubectl top pods
```

4. Rollback:

```bash
kubectl rollout undo deployment app
```

5. Scale:

```bash
kubectl scale deployment app --replicas=5
```

---

# 📌 Interview Tip (Important)

Always answer in this format:

👉 **Problem → Debug Steps → Root Cause → Fix**

---
