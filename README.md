<!--# practice of Devops Experiment

# Practical 1 — Git Basics

```bash id="p1"
mkdir gitdemo
cd gitdemo
git init
echo "Hello World" > hello.txt
git status
git add .
git commit -m "Initial commit"
git log --oneline
echo "Second line" >> hello.txt
git diff
git add .
git commit -m "Update file"
git log --oneline
```

---

# Practical 2 — GitHub Repository

```bash id="p2"
mkdir githubdemo
cd githubdemo
git init
echo "My GitHub project" > readme.txt
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/githubdemo.git
git branch -M main
git push -u origin main
```

---

# Practical 3 — Branching and Merging

```bash id="p3"
mkdir branchdemo
cd branchdemo
git init
echo "Main content" > main.txt
git add .
git commit -m "Initial commit"

git branch feature
git checkout feature

echo "Feature work" >> main.txt
git add .
git commit -m "Feature commit"

git checkout master
git merge feature

git log --oneline
git branch
```

---

# Practical 4 — GitHub Pull Request & Merge Conflict

```bash id="p4"
git clone https://github.com/yourusername/repo.git
cd repo

git checkout -b feature-branch

echo "Feature line" >> README.md
git add .
git commit -m "Feature edit"
git push origin feature-branch

git checkout main
echo "Main line" >> README.md
git add .
git commit -m "Main edit"

git merge feature-branch
```

---

# Practical 5 — GitHub Actions Workflow

```bash id="p5"
mkdir practice5
cd practice5
git init

echo "Hello" > hello.txt

mkdir -p .github/workflows

cat > .github/workflows/main.yml << 'EOF'
name: Hello Workflow

on:
  push:
    branches:
      - main

jobs:
  hello:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello GitHub Actions"
EOF

git add .
git commit -m "Add workflow"

git remote add origin https://github.com/yourusername/practice5.git
git branch -M main
git push -u origin main
```

---

# Practical 6 — CI/CD Workflow

```bash id="p6"
mkdir cicdemo
cd cicdemo
git init

cat > index.html << 'EOF'
<h1>CI/CD Demo</h1>
EOF

mkdir -p .github/workflows

cat > .github/workflows/deploy.yml << 'EOF'
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: echo "Building..."
      - run: echo "Testing..."
      - run: echo "Deploying..."
EOF

git add .
git commit -m "CI/CD setup"

git remote add origin https://github.com/yourusername/cicdemo.git
git branch -M main
git push -u origin main
```

---

# Practical 7 — Automated Testing

```bash id="p7"
mkdir testdemo
cd testdemo
git init

cat > test_sample.py << 'EOF'
def add(a,b):
    return a+b

def test_add():
    assert add(2,3)==5
EOF

mkdir -p .github/workflows

cat > .github/workflows/test.yml << 'EOF'
name: Testing

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.x'
      - run: pip install pytest
      - run: pytest test_sample.py
EOF

git add .
git commit -m "Testing workflow"

git remote add origin https://github.com/yourusername/testdemo.git
git branch -M main
git push -u origin main
```

---

# Practical 8 — Docker Basics

```bash id="p8"
mkdir dockerdemo
cd dockerdemo

cat > app.py << 'EOF'
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello Docker"

app.run(host='0.0.0.0',port=5000)
EOF

echo "flask" > requirements.txt

cat > Dockerfile << 'EOF'
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python","app.py"]
EOF

docker build -t myflaskapp .

docker run -d -p 5000:5000 myflaskapp

docker ps
```

---

# Practical 9 — Docker Compose

```bash id="p9"
mkdir composedemo
cd composedemo

cat > docker-compose.yml << 'EOF'
services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mydb
    ports:
      - "3307:3306"
EOF

docker compose up -d

docker compose ps

docker compose logs web

docker compose logs db

docker compose down
```

---

# Practical 10 — Ansible Playbook

```bash id="p10"
mkdir ansibledemo
cd ansibledemo

ansible --version

cat > inventory.ini << 'EOF'
[webservers]
localhost ansible_connection=local
EOF

cat > install_nginx.yml << 'EOF'
---
- name: Install and start Nginx
  hosts: webservers

  tasks:
    - name: Install Nginx
      command: brew install nginx

    - name: Start Nginx
      command: brew services start nginx
EOF

ansible-playbook -i inventory.ini install_nginx.yml
```
