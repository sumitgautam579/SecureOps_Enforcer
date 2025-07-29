# SecureOps Enforcer: DevSecOps Compliance & Remediation

This repository demonstrates a fully automated, self‑healing DevSecOps pipeline that ensures continuous security and compliance across your infrastructure and applications—powered by Ansible, Jenkins, Docker, Helm, Kubernetes, and AWS.

- **Infrastructure as Code**: Ansible
- **Containerization & Orchestration**: Docker, Helm, Kubernetes (EKS)
- **CI/CD**: Jenkins Pipeline as Code
- **Security Scanning**: SonarQube, Fortify (AppScan)
- **Compliance & Remediation**: Chef, Ansible playbooks
- **Monitoring & SLAs**: Prometheus, Grafana, Nagios
- **Event Streaming**: Kafka, Zookeeper
- **Storage & Databases**: AWS S3, RDS (MySQL)
- **Application Server**: JBoss AS

---

## 🔧 Prerequisites

- **AWS Account** with permissions for EC2, VPC, RDS, S3, IAM, CloudWatch, Route 53
- **SSH Key Pair** tagged for EC2 instances (`ssh_key_name`)
- **Local Tools**: Docker, Ansible, AWS CLI, Git
- **CI Server**: Jenkins with Docker & Ansible plugins installed
- **Monitoring**: Access to Grafana & Prometheus

---

## 🏗️ Architecture

[SecureOps Enforcer Architecture Diagram](.doc/ARCH_SecureOps_enforcer.png)


## 📁 Repository Structure

```plaintext
secureops-enforcer/                 # Project root
├── ansible/                        # IaC: inventories, group_vars, roles, playbooks
├── docker/                         # Dockerfiles for JBoss & scanner containers
├── helm/                           # Helm chart for JBoss applications & sidecars
├── jenkins/                        # Jenkins pipeline definitions (Jenkinsfile)
├── grafana/                        # Provisioned datasources & dashboard JSONs
├── docs/                           # Architecture diagram & supporting docs
├── sla/                            # Service Level Objectives definitions
├── scripts/                        # Utility scripts (e.g. JBoss deploy)
└── README.md                       # ← You are here
```

---

## 🚀 Getting Started

1. **Fork this repository**
    - Click the Fork button [![Fork me on GitHub](https://img.shields.io/badge/Fork%20me-blue.svg)](https://github.com/sumitgautam579/SecureOps_Enforcer.git) 


2. **Clone the repository**

   ```bash
   git clone https://github.com/sumitgautam579/SecureOps_Enforcer.git
   cd secureops-enforcer
   ```

3. **Configure variables**

   - Edit `ansible/group_vars/all.yml` to set:
     - `aws_region`, `ssh_key_name`, `db_password`, `s3_bucket_logs`, `kafka_nodes`, `zookeeper_nodes`
   - Update notification email in `jenkins/Jenkinsfile`.
   - Add your architecture diagram at `docs/architecture.png`.

4. **Install dependencies**

   ```bash
   pip install ansible boto3 community.aws community.docker awscli
   ```

5. **Provision AWS infrastructure**

   ```bash
   ansible-playbook ansible/playbooks/provision.yml \
     -i ansible/inventory/aws_ec2.yml
   ```

6. **Run compliance scans and remediation**

   ```bash
   ansible-playbook ansible/playbooks/scan.yml \
     -i ansible/inventory/aws_ec2.yml
   ansible-playbook ansible/playbooks/remediate.yml \
     -i ansible/inventory/aws_ec2.yml
   ```

7. **Deploy monitoring stack**

   ```bash
   ansible-playbook ansible/playbooks/monitor.yml \
     -i ansible/inventory/aws_ec2.yml
   ```

8. **Execute CI/CD pipeline**

   - In Jenkins, create a Multibranch Pipeline pointing to this repo.
   - Configure AWS credentials and email notifications.
   - Run the pipeline to orchestrate all stages.

---

## 📊 Monitoring & SLAs

- **Grafana dashboards** auto‑loaded from `grafana/dashboards/`
- **Prometheus** datasource configured in `grafana/provisioning/datasources.yml`
- **Nagios** checks deployed via Ansible roles
- **Service Level Objectives** defined in `sla/SLOs.md`:
  - 99.9% compliance scan coverage
  - < 5 min auto‑remediation response
  - 99% monitoring uptime

---

## 🔐 Security & Scanning

- **SonarQube** and **Fortify/AppScan** scans invoked in Jenkins and Ansible playbooks
- **Chef** and **Ansible** auto‑remediate security drift immediately after detection

---

## 🤝 Contributing

Contributions and improvements are welcome! Please file an issue for suggestions or submit a pull request.

---

© 2025 **SecureOps-Enforcer** DEMO / **Sumit_Gautam_Devops_Engineer**

