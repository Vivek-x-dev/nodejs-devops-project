#  Enterprise CI/CD Pipeline: Jenkins, Docker & AWS

A production-grade Continuous Integration and Deployment pipeline automating the lifecycle of a containerized application from **Local Development** to **AWS EC2** environments.

---

##  System Architecture

The workflow follows a "Build once, run anywhere" philosophy using Docker and Jenkins orchestrating the movement across environments.



### 🔄 The Workflow
1.  **Code Commit:** Developer pushes changes to a specific branch on **GitHub**.
2.  **Trigger:** **GitHub Webhooks** notify Jenkins of the push event.
3.  **CI Phase:** **Jenkins** pulls the code, builds the **Docker Image**, and tags it.
4.  **Artifact Storage:** The image is pushed to **Docker Hub** (Private/Public registry).
5.  **CD Phase:** Jenkins executes a remote deployment script on the **AWS EC2** instance.
6.  **Orchestration:** **Docker Compose** pulls the latest image and restarts services.
7.  **Ingress:** **Nginx** acts as a Reverse Proxy to route external traffic to the app.

---

##  Core Concepts

### Continuous Integration (CI)
Automates the process of merging code changes. By using **Jenkins**, we ensure that every commit is automatically built into a container, catching integration errors early.

### Containerization (Docker)
By packaging the application and its dependencies into a **Docker Image**, we eliminate the "it works on my machine" problem. The environment in Staging is identical to Production.

### Reverse Proxy & Gateway (Nginx)
**Nginx** serves as the entry point for all web traffic. It provides:
* **Abstraction:** Users connect to Nginx, which talks to the internal Docker network.
* **Efficiency:** Handles SSL termination and static file caching.
* **Security:** Prevents direct exposure of the application ports to the public internet.

---

## 🛠️ Tech Stack & Components

| Component | Technology | Role |
| :--- | :--- | :--- |
| **VCS** | GitHub | Source code management & triggers |
| **CI/CD Tool** | Jenkins | Pipeline orchestration & automation |
| **Container** | Docker | Application packaging |
| **Registry** | Docker Hub | Image versioning and storage |
| **Cloud** | AWS EC2 | Hosting infrastructure |
| **Runtime** | Docker Compose | Multi-container management |
| **Web Server** | Nginx | Reverse Proxy & Load Balancing |

---


## Connect With Me

<p align="center">
  <a href="https://www.linkedin.com/in/Yvivek-x-dev/">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
</p>

<p align="center">
  Let's connect and talk about DevOps, CI/CD, and Cloud Infrastructure!
</p>



## 📂 Project Structure

```text
.
nodejs-devops-project/
│
├── app/                     # Node.js app
│   ├── server.js
│   ├── package.json
│
├── Dockerfile
├── docker-compose.yml
├── docker-compose.staging.yml
├── docker-compose.prod.yml
│
├── nginx/
│   ├── default.conf
│
├── Jenkinsfile
│
└── README.md

---
'''
