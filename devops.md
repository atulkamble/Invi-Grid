# 🚀 1. DevOps Core – Interview Q&A (with Answers)

### ❓ Q1: What is CI/CD?

**Answer:**
CI/CD is a practice to automate code integration, testing, and deployment.

* CI → Continuous Integration (build + test)
* CD → Continuous Delivery/Deployment (release automation)

---

### ❓ Q2: Difference between Docker and Kubernetes?

| Feature | Docker           | Kubernetes     |
| ------- | ---------------- | -------------- |
| Purpose | Containerization | Orchestration  |
| Scope   | Single container | Manage cluster |
| Scaling | Manual           | Auto-scaling   |

---

### ❓ Q3: What is Infrastructure as Code (IaC)?

**Answer:**
Managing infrastructure using code instead of manual setup.

Example tools:

* Terraform
* AWS CloudFormation

---

### ❓ Q4: What is a Jenkins pipeline?

**Answer:**
Automation pipeline for build, test, deploy.

### ✅ Sample Jenkinsfile

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
```

---

# 💻 2. Coding Questions (DevOps + QA)

---

### ❓ Q5: Write Python script to call API

### ✅ Answer + Code

```python
import requests

url = "https://api.github.com"
response = requests.get(url)

print("Status Code:", response.status_code)
print("Response:", response.json())
```

---

### ❓ Q6: Parse JSON response

### ✅ Answer + Code

```python
import json

data = '{"name": "Atul", "role": "DevOps"}'
parsed = json.loads(data)

print(parsed["name"])
```

---

### ❓ Q7: Error handling in Python

### ✅ Answer + Code

```python
try:
    x = int("abc")
except ValueError:
    print("Conversion failed")
finally:
    print("Execution completed")
```

---

### ❓ Q8: Bash script to check server status

### ✅ Answer + Code

```bash
#!/bin/bash

if ping -c 1 google.com > /dev/null
then
  echo "Server is reachable"
else
  echo "Server is down"
fi
```

---

# 🧪 3. QA (Manual + Automation) Q&A

---

### ❓ Q9: What is Regression Testing?

**Answer:**
Testing existing functionality after code changes to ensure nothing is broken.

---

### ❓ Q10: What is Bug Lifecycle?

**Answer:**

```
New → Assigned → Open → Fixed → Retest → Closed
```

---

### ❓ Q11: Selenium vs Postman?

| Tool     | Use           |
| -------- | ------------- |
| Selenium | UI Automation |
| Postman  | API Testing   |

---

# 🔄 4. QA Automation Coding

---

### ❓ Q12: Selenium login automation (Python)

### ✅ Answer + Code

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

driver.get("https://example.com/login")

driver.find_element(By.ID, "username").send_keys("admin")
driver.find_element(By.ID, "password").send_keys("123")
driver.find_element(By.ID, "login").click()

print("Login Test Executed")
driver.quit()
```

---

### ❓ Q13: API Test using Python

### ✅ Answer + Code

```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/posts/1")

assert response.status_code == 200
assert "userId" in response.json()

print("API Test Passed")
```

---

# 🔧 5. DevOps + QA Pipeline Example

---

### ❓ Q14: Explain pipeline flow

**Answer:**

```
Code → Build → Unit Test → UI Test → API Test → Deploy
```

---

### ❓ Q15: GitHub Actions pipeline example

### ✅ Answer + Code

```yaml
name: CI Pipeline

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v3

    - name: Run Tests
      run: echo "Running tests..."

    - name: Build
      run: echo "Building app..."
```

---

# 🔥 6. Real Interview Coding Questions

---

### ❓ Q16: Write script to check log errors

### ✅ Answer + Code

```python
with open("app.log") as file:
    for line in file:
        if "ERROR" in line:
            print(line)
```

---

### ❓ Q17: Retry logic script

### ✅ Answer + Code

```python
import time

for i in range(3):
    print("Trying...")
    success = False
    
    if success:
        break
    time.sleep(2)
else:
    print("Failed after retries")
```

---

# 🎯 7. Advanced DevOps QA Question

---

### ❓ Q18: How do you integrate testing in CI/CD?

**Answer:**

* Unit tests → during build
* UI tests → after build
* API tests → before deployment
* Security scans → before production

---

# 📌 8. Quick Revision (Important 🔥)

### DevOps

* CI/CD pipeline
* Docker vs Kubernetes
* Terraform basics

### QA

* Regression testing
* Selenium + API testing

### Coding

* API calls
* JSON parsing
* Error handling

---
