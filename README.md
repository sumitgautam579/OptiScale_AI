# OptiScale_AI: AI/ML-Powered Cloud Cost Optimization Engine 


A turnkey FinOps solution that ingests AWS billing data, applies ML-driven rightsizing, and auto-applies cost-saving changes with Ansible, Helm, and Jenkins—monitored in Grafana.

## 🛠️ Real-World Use Case

A mid-sized SaaS company struggling with unpredictable AWS bills integrates OptiScale_AI to automatically ingest daily billing data, generate ML-driven rightsizing recommendations for EC2 and RDS, and apply approved Terraform changes via Ansible. Within the first month, they may reduce their cloud spend upto by 25% and gain continuous visibility into cost anomalies through Grafana dashboards.

## 🏗️ Architecture

[OptiScale_AI Architecture Diagram](doc/OptiScale_AI_ARCH.png)
---

## ✨ Highlights
- **Predictive Rightsizing:** Python ML model in Docker forecasts optimal EC2/RDS instance sizes.
- **Automated Provisioning:** Ansible roles automate AWS infrastructure (S3, RDS) and EKS cluster setup.
- **Container Orchestration:** Helm chart deploys CronJob on EKS for scheduled cost analysis.
- **CI/CD Pipeline:** Jenkins pipelines for linting, provisioning, deployment, and dashboard provisioning.
- **Observability:** Prometheus scraping and Grafana dashboards for real-time cost insights.
- **Cloud Native:** AWS (EC2, S3, IAM, RDS, CloudWatch, Route 53, VPC, CloudFront) plus Kubernetes.

---

## 🔧 Prerequisites
- **AWS Account** with access keys for EC2, S3, ECR, RDS, EKS, IAM, CloudWatch.
- **SSH Key Pair** in AWS for EC2/EKS node authentication.
- **Local Tools:** Docker, kubectl, eksctl (optional), Ansible, AWS CLI, Helm, Git.
- **CI Server:** Jenkins with Docker & Kubernetes plugins.
- **Monitoring:** Access to Grafana & Prometheus.

---

## 📂 Repository Structure
```plaintext
optiscale-ai/                    # Project root
├── README.md                    # ← This file
├── docs/
│   └── architecture.png         # Architecture diagram
├── ansible/
│   ├── inventory/
│   ├── group_vars/
│   ├── roles/
│   │   ├── aws_provision/
│   │   ├── eks_provision/
│   │   ├── cost_analyzer/
│   │   └── grafana_provision/
│   └── playbooks/
├── docker/
│   ├── Dockerfile
│   ├── requirements.txt
│   └── analyze.py
├── helm/optiscale-chart/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
├── jenkins/
│   └── Jenkinsfile
├── grafana/
│   ├── provisioning/
│   └── dashboards/
└── sla/
    └── SLOs.md
```

---

## 🚀 Quick Start

1. **Fork this repository**
    - Click the Fork button [![Fork me on GitHub](https://img.shields.io/badge/Fork%20me-blue.svg)](https://github.com/sumitgautam579/OptiScale_AI.git) 


2. **Clone the repository**
```
    git clone https://github.com/sumitgautam579/OptiScale_AI.git

    cd optiscale-ai
```
```bash


# 1. Configure AWS credentials
export AWS_ACCESS_KEY_ID=...
export AWS_SECRET_ACCESS_KEY=...

# 2. Install Ansible collections
ansible-galaxy collection install community.aws community.docker

# 3. Provision infra & EKS
ansible-playbook ansible/playbooks/provision.yml -i ansible/inventory/aws_ec2.yml

# 4. Build & deploy analyzer
ansible-playbook ansible/playbooks/deploy.yml -i ansible/inventory/aws_ec2.yml

# 5. Helm deploy CronJob
helm upgrade --install optiscale helm/optiscale-chart --namespace optiscale --create-namespace

# 6. Provision Grafana dashboards
ansible-playbook ansible/playbooks/grafana.yml  -i ansible/inventory/aws_ec2.yml
```

---

## 📊 Monitoring & SLAs
- **Grafana dashboards:** `grafana/dashboards/`
- **Prometheus datasource:** `grafana/provisioning/datasources.yml`
- **Service Level Objectives:** see `sla/SLOs.md`:
  - 99.9% CronJob success rate
  - Analysis latency < 15 minutes
  - Monthly cost drift < 10%

---

## 🤝 Contributing
Contributions welcome! Open issues or PRs to add new features, improve docs, or suggest enhancements.

---

## 📄 License

© 2025 **OptiScale_AI** DEMO / **Sumit_Gautam_Devops_Engineer**

Licensed under the MIT License. See `LICENSE` for details.
