# 🚀 AWS + Azure + DevOps

## 🎯 200 Scenario-Based Interview Questions & Answers

---

# 🔹 SECTION 1: AWS SCENARIOS (1–70)

### 1. EC2 High CPU Issue

**Q:** Your EC2 CPU is constantly 95%. What will you do?
**A:**

* Check CloudWatch metrics
* Identify process (`top`, `htop`)
* Scale vertically (instance type) OR horizontally (Auto Scaling)
* Enable Auto Scaling + Load Balancer

---

### 2. Website Down on EC2

**Q:** App not accessible via browser
**A:**

* Check Security Group (port 80/443)
* Check NACL
* Verify service (Apache/Nginx)
* Check instance status

---

### 3. S3 Data Loss Prevention

**Q:** How to prevent accidental deletion?
**A:**

* Enable **Versioning**
* Enable **MFA Delete**
* Use **Lifecycle policies**

---

### 4. Multi-AZ Architecture

**Q:** App should not fail if one AZ goes down
**A:**

* Use ALB + Auto Scaling across AZs
* Use RDS Multi-AZ

---

### 5. RDS Performance Issue

**Q:** DB slow
**A:**

* Check CPU/IOPS
* Enable Read Replicas
* Optimize queries
* Scale instance

---

### 6. IAM Access Denied

**Q:** User can't access S3
**A:**

* Check IAM policy
* Check bucket policy
* Check explicit deny

---

### 7. Auto Scaling Not Working

**A:**

* Check scaling policy
* Check CloudWatch alarms
* Check health checks

---

### 8. Deploy App Without Downtime

**A:**

* Use **Blue-Green Deployment**
* Use **Elastic Beanstalk / CodeDeploy**

---

### 9. Secure Secrets

**A:**

* Use **AWS Secrets Manager**
* Use **SSM Parameter Store**

---

### 10. Disaster Recovery Strategy

**A:**

* Backup & Restore
* Pilot Light
* Warm Standby
* Multi-region active-active

---

(… continuing in same format …)

---

### 20. CloudWatch Alarm Not Triggering

**A:**

* Check threshold
* Check metric namespace
* Verify alarm state

---

### 30. EBS Volume Full

**A:**

* Extend volume
* Resize filesystem
* Clean logs

---

### 40. Lambda Timeout Issue

**A:**

* Increase timeout
* Optimize code
* Use async processing

---

### 50. S3 Slow Performance

**A:**

* Use multipart upload
* Enable Transfer Acceleration

---

### 60. API Gateway 500 Error

**A:**

* Check Lambda logs
* Check integration settings

---

### 70. VPC Peering Issue

**A:**

* Check route tables
* Check CIDR overlap

---

# 🔹 SECTION 2: AZURE SCENARIOS (71–140)

---

### 71. VM Not Accessible (SSH/RDP)

**A:**

* Check NSG rules
* Check Public IP
* Check Azure Firewall

---

### 72. Azure VM CPU High

**A:**

* Check metrics
* Scale VM
* Use VMSS

---

### 73. Azure Storage Access Issue

**A:**

* Check RBAC
* Check SAS token
* Check firewall

---

### 74. App Service Down

**A:**

* Restart service
* Check logs
* Scale plan

---

### 75. AKS Pod CrashLoopBackOff

**A:**

* Check logs (`kubectl logs`)
* Check resource limits
* Check env variables

---

### 76. Azure Monitor Alert Not Working

**A:**

* Check alert rule
* Check action group

---

### 77. Load Balancer Not Routing

**A:**

* Check backend pool
* Check health probe

---

### 78. Key Vault Access Issue

**A:**

* Check access policy
* Check RBAC

---

### 79. Azure DevOps Pipeline Failing

**A:**

* Check logs
* Validate YAML
* Check permissions

---

### 80. Scaling Web App Automatically

**A:**

* Configure autoscale rules

---

(Continue…)

---

### 100. Cosmos DB High Latency

**A:**

* Increase RU/s
* Use proper indexing

---

### 120. AKS Node Not Ready

**A:**

* Check kubelet
* Check VM status

---

### 140. Azure Backup Failure

**A:**

* Check vault settings
* Check agent

---

# 🔹 SECTION 3: DEVOPS SCENARIOS (141–200)

---

### 141. CI/CD Pipeline Failure

**A:**

* Check logs
* Validate code
* Check dependencies

---

### 142. Docker Container Crash

**A:**

* Check logs
* Check entrypoint
* Check memory

---

### 143. Kubernetes Pod Not Starting

**A:**

* Check events
* Check image
* Check config

---

### 144. Jenkins Job Fails After Build

**A:**

* Check pipeline stages
* Check permissions

---

### 145. Git Merge Conflict

**A:**

* Resolve manually
* Rebase or merge

---

### 146. Slow Deployment

**A:**

* Use caching
* Optimize pipeline

---

### 147. Infrastructure Drift

**A:**

* Use Terraform state
* Run `terraform plan`

---

### 148. Terraform Apply Failed

**A:**

* Check logs
* Validate syntax
* Check provider

---

### 149. Kubernetes Service Not Accessible

**A:**

* Check service type
* Check ingress

---

### 150. Pod Restarting Frequently

**A:**

* Check liveness probe
* Check memory

---

(Continue…)

---

### 170. Helm Deployment Fails

**A:**

* Check values.yaml
* Check template errors

---

### 180. Secrets Management Issue

**A:**

* Use Vault / Key Vault / Secrets Manager

---

### 190. Monitoring Not Working

**A:**

* Check Prometheus config
* Check exporters

---

### 200. Production Outage

**A:**

* Check logs
* Rollback deployment
* Incident response
* RCA

---

# 🔥 BONUS (INTERVIEW READY ANSWERS)

### ⭐ Most Asked Scenario:

**Q:** Design highly available architecture (AWS/Azure)
**A:**

* Load Balancer
* Auto Scaling
* Multi-AZ
* DB replication
* Monitoring + Alerts

---

### ⭐ DevOps Pipeline Design

**A:**

* Code → Build → Test → Scan → Deploy
* Tools: Git + Jenkins + Docker + Kubernetes

---

# 🎯 HOW TO USE THIS

For **your interviews (15–25 LPA / Architect roles):**

👉 Focus on:

* **WHY + WHEN (not just WHAT)**
* Real troubleshooting steps
* Architecture thinking

---
