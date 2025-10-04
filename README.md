# Python + Backend + DevOps + AI — 20-Day Learning Plan

This repository contains a **20-day structured learning plan** to master Python fundamentals, backend development with FastAPI, DevOps automation, and AI agent integration.  
The plan is designed for **1 hour per day**. Each day includes:  
- **Concepts** → Fundamental explanations  
- **Analogy** → Relating it to DevOps/backend scenarios  
- **Example** → Practical Python code  
- **Exercise** → Hands-on tasks to practice  

---

## **Week 1: Python Core Foundations**
**Goal:** Learn Python basics — variables, data types, control flow, functions, and file handling.  

### **Day 1 – Variables & Print**
**Concepts:**  
- Variables are like labeled boxes storing data.  
- Python infers the type automatically.  
- Data types: `str`, `int`, `float`, `bool`.  

**Analogy:** Like Terraform/Helm variables in YAML.  

**Example:**
```python
app_name = "phoenix-api"
replicas = 3
tls_enabled = True

print("==== Deployment Summary ====")
print(f"App: {app_name}, Replicas: {replicas}, TLS: {tls_enabled}")
```

**Exercise:** Create 3 variables (`app_name`, `replicas`, `monitoring_enabled`) and print them in a formatted summary.  

---

### **Day 2 – Lists & Dictionaries**
**Concepts:**  
- Lists store ordered collections.  
- Dictionaries store key-value pairs (like JSON/YAML).  

**Analogy:**  
- Lists = pod lists (`kubectl get pods`).  
- Dicts = JSON API response from Kubernetes.  

**Example:**
```python
pods = ["pod-1", "pod-2", "pod-3"]
print(pods[1])  # pod-2

deployment = {"app": "phoenix", "replicas": 3, "status": "Running"}
print(deployment["status"])  # Running
```

**Exercise:** Create a list of environments (`dev`, `stage`, `prod`) and a dict representing a deployment with keys: `app_name`, `image_tag`, `status`.  

---

### **Day 3 – Loops & Conditions**
**Concepts:**  
- Loops repeat actions (`for pod in pods:`).  
- Conditions branch logic (`if status == "Running":`).  

**Analogy:**  
- Loop = iterating pods to check health.  
- Condition = trigger alerts if unhealthy.  

**Example:**
```python
pods = [
    {"name": "pod-1", "status": "Running"},
    {"name": "pod-2", "status": "CrashLoopBackOff"}
]

for pod in pods:
    if pod["status"] != "Running":
        print(f"⚠️ {pod['name']} unhealthy: {pod['status']}")
```

**Exercise:** Count how many pods are unhealthy and print total.  

---

### **Day 4 – Functions**
**Concepts:**  
- Functions = reusable code blocks (`def`).  
- Accept parameters, return values.  

**Analogy:** Bash functions in shell scripts.  

**Example:**
```python
def restart_service(name):
    print(f"Restarting {name}...")

restart_service("nginx")
```

**Exercise:** Write a function `scale_app(app, replicas)` that prints a scaling message.  

---

### **Day 5 – File I/O**
**Concepts:**  
- `open()` for reading/writing files.  
- Loop through lines.  

**Analogy:** Reading `app.log` for errors.  

**Example:**
```python
with open("sample.log") as f:
    for line in f:
        if "ERROR" in line:
            print("❗", line.strip())
```

**Exercise:** Count ERROR lines in a file and print summary.  

---

### **Day 6 – JSON & YAML**
**Concepts:**  
- JSON = standard API format.  
- YAML = configs like Helm values.  

**Analogy:** Parsing `kubectl get pod -o json` or `values.yaml`.  

**Example:**
```python
import json, yaml

data = '{"app":"phoenix","replicas":3}'
config = json.loads(data)
print(config["app"])

yaml_data = """
app: phoenix
replicas: 3
"""
parsed = yaml.safe_load(yaml_data)
print(parsed["replicas"])
```

**Exercise:** Load a real Helm values.yaml and print one field.  

---

### **Day 7 – Mini Project**
Build a **Log Analyzer**:  
- Input: log file  
- Output: list of errors, count of total errors  

---

## **Week 2: DevOps-Friendly Python**
**Goal:** Organize code, handle errors, logging, CLI, subprocess.  

### **Day 8 – Modules & Imports**
**Concepts:** Split code into files and reuse with imports.  
**Analogy:** Like reusing Terraform modules.  
**Example:**
```python
# utils.py
def greet(name): return f"Hello {name}"

# main.py
from utils import greet
print(greet("DevOps"))
```

---

### **Day 9 – Virtualenv & Dependencies**
**Concepts:** venv isolates Python environments.  
**Example:**
```bash
python3 -m venv venv
source venv/bin/activate
pip install requests
pip freeze > requirements.txt
```

---

### **Day 10 – Exception Handling**
**Concepts:** Use try/except for error handling.  
**Example:**
```python
try:
    val = int("oops")
except ValueError as e:
    print("❌ Error:", e)
```

---

### **Day 11 – Logging**
**Concepts:** Structured logging with levels.  
**Example:**
```python
import logging
logging.basicConfig(level=logging.INFO)
logging.info("Deployment started")
logging.error("Deployment failed")
```

---

### **Day 12 – CLI (Argparse)**
**Example:**
```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--app", required=True)
args = parser.parse_args()
print(f"Deploying {args.app}")
```

---

### **Day 13 – Subprocess**
**Concepts:** Run shell commands.  
**Example:**
```python
import subprocess
result = subprocess.run(["echo", "hello"], capture_output=True, text=True)
print(result.stdout)
```

➡️ Replace with `kubectl get pods`  

---

### **Day 14 – Mini Project**
Build **Pod Checker CLI**:  
- Input: namespace  
- Output: count running pods vs crashloop  

---

## **Week 3: FastAPI Backend**
**Goal:** Build APIs and simulate frontend calls.  

### **Day 15 – FastAPI Setup**
```bash
pip install fastapi uvicorn
```
```python
from fastapi import FastAPI
app = FastAPI()

@app.get("/")
def root():
    return {"msg": "Hello DevOps"}
```

Run: `uvicorn main:app --reload`  

---

### **Day 16 – Pydantic Models**
```python
from pydantic import BaseModel
class Deployment(BaseModel):
    app: str
    replicas: int
```

---

### **Day 17 – CRUD & Frontend Demo**
- Build GET `/pods`, POST `/deploy`  
- Call with Postman or fetch() from Node.js  

---

### **Day 18 – Database Integration**
- Add PostgreSQL with SQLAlchemy  

---

### **Day 19 – Auth & Middleware**
- JWT Auth  
- Logging middleware  

---

### **Day 20 – Mini Project**
Full FastAPI service with:  
- DB integration  
- Auth  
- API consumed by frontend fetch()  

---

## 🚀 Beyond 20 Days
- **LangChain/LangGraph agents** (AI integration)  
- **End-to-end project**: FastAPI + LangChain, Dockerized, deployed to AKS  
- **Frontend basics**: Node.js/TypeScript  
