# 🔷 Terraform Scenario-Based Questions & Answers

## ✅ 1. Multi-Environment Deployment (Dev / Prod)

**Scenario:**
You need to deploy the same infrastructure in **dev and prod** with different configurations.

**Answer:**
Use **Terraform Workspaces + variables**

```bash
terraform workspace new dev
terraform workspace new prod
terraform workspace select dev
```

```hcl
variable "instance_type" {}

resource "aws_instance" "web" {
  instance_type = var.instance_type
}
```

```bash
terraform apply -var="instance_type=t2.micro"   # dev
terraform apply -var="instance_type=t3.large"   # prod
```

👉 **Best Practice:**

* Use **separate backend state** for production

---

## ✅ 2. State File Corruption / Team Collaboration

**Scenario:**
Multiple engineers are working, and state file conflicts occur.

**Answer:**
Use **Remote Backend with Locking**

```hcl
terraform {
  backend "s3" {
    bucket         = "my-tf-state"
    key            = "env/dev/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-lock"
  }
}
```

👉 Prevents:

* State corruption
* Concurrent writes

---

## ✅ 3. Resource Drift

**Scenario:**
Someone manually changed an EC2 instance outside Terraform.

**Answer:**

```bash
terraform plan
```

👉 Terraform detects drift

To fix:

```bash
terraform apply
```

OR import resource:

```bash
terraform import aws_instance.web i-123456
```

---

## ✅ 4. Reusable Infrastructure

**Scenario:**
You want reusable code for VPC, EC2, RDS.

**Answer: Use Modules**

```hcl
module "vpc" {
  source = "./modules/vpc"
}
```

👉 Benefits:

* Reusability
* Clean architecture
* Enterprise standard

---

## ✅ 5. Zero Downtime Deployment

**Scenario:**
Update infrastructure without downtime.

**Answer:**

```hcl
lifecycle {
  create_before_destroy = true
}
```

👉 Used in:

* Load balancers
* Auto Scaling

---

## ✅ 6. Secret Management

**Scenario:**
Avoid hardcoding DB passwords.

**Answer:**

* Use **AWS Secrets Manager / Azure Key Vault**

```hcl
data "aws_secretsmanager_secret_version" "db" {
  secret_id = "db-password"
}
```

---

## ✅ 7. Dependency Management

**Scenario:**
Ensure DB is created before App server.

**Answer:**

```hcl
depends_on = [aws_db_instance.db]
```

---

## ✅ 8. Large Scale Infra Deployment

**Scenario:**
Deploy 100 EC2 instances.

**Answer:**

```hcl
resource "aws_instance" "web" {
  count = 100
}
```

OR better:

```hcl
for_each = toset(["app1", "app2"])
```

---

## ✅ 9. CI/CD Integration

**Scenario:**
Run Terraform in pipeline.

**Answer:**

```yaml
steps:
  - terraform init
  - terraform plan
  - terraform apply -auto-approve
```

👉 Use:

* GitHub Actions / Jenkins / Azure DevOps

---

## ✅ 10. Multi-Cloud Deployment

**Scenario:**
Deploy infra on AWS + Azure.

**Answer:**

```hcl
provider "aws" {}
provider "azurerm" {}
```

👉 Terraform supports **multi-cloud architecture**

---

# 🔷 Ansible Scenario-Based Questions & Answers

---

## ✅ 1. Configuration Drift

**Scenario:**
Servers are not consistent.

**Answer:**
Use **Idempotent Playbooks**

```yaml
- name: Install nginx
  apt:
    name: nginx
    state: present
```

👉 Runs multiple times without breaking

---

## ✅ 2. Deploy App to Multiple Servers

**Scenario:**
Deploy app to 50 servers.

**Answer:**

```ini
[web]
server1
server2
```

```yaml
- hosts: web
  tasks:
    - name: Copy app
      copy:
        src: app/
        dest: /var/www/html/
```

---

## ✅ 3. Dynamic Inventory (Cloud)

**Scenario:**
Servers are dynamic (AWS EC2).

**Answer:**
Use **Dynamic Inventory Plugin**

```bash
ansible-inventory -i aws_ec2.yaml --list
```

---

## ✅ 4. Secrets Handling

**Scenario:**
Secure passwords.

**Answer: Use Ansible Vault**

```bash
ansible-vault encrypt secrets.yml
```

---

## ✅ 5. Conditional Execution

**Scenario:**
Run tasks only on Ubuntu.

**Answer:**

```yaml
when: ansible_os_family == "Debian"
```

---

## ✅ 6. Rolling Deployment (Zero Downtime)

**Scenario:**
Update servers one by one.

**Answer:**

```yaml
- hosts: web
  serial: 1
```

---

## ✅ 7. Reusability

**Scenario:**
Reuse configurations.

**Answer: Use Roles**

```bash
ansible-galaxy init web-role
```

```yaml
- hosts: web
  roles:
    - web-role
```

---

## ✅ 8. Service Management

**Scenario:**
Ensure service always running.

**Answer:**

```yaml
- name: Start nginx
  service:
    name: nginx
    state: started
    enabled: yes
```

---

## ✅ 9. Handling Failures

**Scenario:**
Ignore failure for non-critical task.

**Answer:**

```yaml
ignore_errors: yes
```

---

## ✅ 10. Integrating with Terraform

**Scenario:**
Provision infra + configure servers.

**Answer:**

1. Terraform → create EC2
2. Ansible → configure

```bash
terraform apply
ansible-playbook -i inventory playbook.yml
```

---

# 🔷 Combined Terraform + Ansible Scenario (VERY IMPORTANT)

## ✅ End-to-End DevOps Scenario

**Scenario:**
You need to:

* Provision EC2 instances
* Install Nginx
* Deploy application

**Solution Flow:**

1. **Terraform**

```bash
terraform apply
```

2. Generate inventory:

```bash
terraform output public_ip
```

3. **Ansible**

```yaml
- hosts: web
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

---

# 🔥 Interview Tips (High Impact)

* Terraform = **Provisioning (Infra as Code)**
* Ansible = **Configuration Management**
* Together = **Complete DevOps Automation**

---
