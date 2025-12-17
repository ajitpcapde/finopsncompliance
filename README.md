# ☁️ Cloud Compliance Canvas

<div align="center">

![Python](https://img.shields.io/badge/Python-3.9+-3776ab?style=for-the-badge&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.28+-ff4b4b?style=for-the-badge&logo=streamlit&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-Security%20Hub%20%7C%20GuardDuty%20%7C%20Config-232f3e?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![Claude AI](https://img.shields.io/badge/Claude%20AI-Bedrock-d97706?style=for-the-badge&logo=anthropic&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge)

**Enterprise AWS Governance Platform**

AI-Powered Multi-Cloud Compliance, FinOps, and Security Orchestration

[Features](#-features) • [Installation](#-installation) • [Configuration](#-configuration) • [Modules](#-modules) • [Screenshots](#-screenshots) • [Architecture](#-architecture)

---

</div>

## 📋 Overview

**Cloud Compliance Canvas** is a comprehensive enterprise-grade platform for AWS governance, combining compliance management, FinOps intelligence, and AI-powered security orchestration in a single unified interface.

Built for cloud architects, security teams, and FinOps practitioners managing complex multi-account AWS environments, this platform provides real-time visibility, automated remediation, and intelligent cost optimization.

**Version 6.0 Enterprise Edition** — Production Ready — AWS re:Invent 2025 Ready

---

## ✨ Features

### 📊 Executive Dashboard
- **Real-Time KPIs** — Live compliance scores, security posture, and cost metrics
- **Multi-Account Overview** — Unified view across AWS Organizations
- **Trend Analysis** — Historical compliance and cost trend visualization
- **Risk Heatmaps** — Visual representation of security risks by account/region

### 🔐 Security & Compliance
- **AI-Powered Threat Detection** — Claude AI integration for intelligent threat analysis
- **Automated Remediation** — One-click and batch remediation capabilities
- **Compliance Framework Mapping** — SOC 2, PCI-DSS, HIPAA, GDPR, ISO 27001
- **Policy as Code Engine** — OPA, Sentinel, and SCP integration
- **Evidence Collection** — Automated audit trail and compliance documentation

### 💰 FinOps Intelligence
- **Predictive Analytics** — ML-powered cost forecasting
- **Chargeback & Showback** — Cost allocation by team, project, and environment
- **Optimization Recommendations** — AI-driven rightsizing and savings opportunities
- **Reserved Instance Analysis** — RI/Savings Plans coverage and recommendations
- **Tag Compliance** — Cost allocation tag enforcement and tracking

### 🔄 Account Lifecycle Management
- **Automated Onboarding** — Streamlined new account provisioning
- **Offboarding Workflows** — Secure account decommissioning
- **OU Management** — Organizational unit structure management
- **Baseline Deployment** — Automated security baseline application

### 🛡️ Vulnerability Management
- **EKS Container Scanning** — Base image and application vulnerability detection
- **OS-Specific Remediation** — Windows Server and Linux distribution-aware patching
- **NIST NVD Integration** — Real-time vulnerability database correlation
- **Bulk Remediation** — Enterprise-scale vulnerability resolution

### 🔌 Integration Hub
- **ITSM Integration** — Jira, ServiceNow, PagerDuty
- **Communication** — Slack, Microsoft Teams notifications
- **GitOps** — GitHub, GitLab, Bitbucket, ArgoCD
- **Data Platforms** — Snowflake, Apptio Cloudability, CloudHealth

---

## 🛠️ Installation

### Prerequisites

- Python 3.9 or higher
- AWS Account with appropriate IAM permissions
- Anthropic API key (for Claude AI features)

### Quick Start

```bash
# Clone the repository
git clone https://github.com/yourusername/cloud-compliance-canvas.git
cd cloud-compliance-canvas

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the application
streamlit run streamlit_app.py
```

### Streamlit Cloud Deployment

1. Fork this repository to your GitHub account
2. Go to [share.streamlit.io](https://share.streamlit.io)
3. Connect your GitHub repository
4. Configure secrets in the Streamlit Cloud dashboard

---

## ⚙️ Configuration

### Environment Variables

Create a `.streamlit/secrets.toml` file:

```toml
[aws]
access_key_id = "your_aws_access_key"
secret_access_key = "your_aws_secret_key"
region = "us-east-1"

[anthropic]
api_key = "your_anthropic_api_key"

[integrations]
jira_url = "https://your-org.atlassian.net"
jira_token = "your_jira_token"
slack_webhook = "https://hooks.slack.com/services/..."
```

### Required AWS IAM Permissions

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "securityhub:*",
        "guardduty:*",
        "config:*",
        "inspector2:*",
        "ce:*",
        "organizations:*",
        "cloudtrail:*",
        "iam:*"
      ],
      "Resource": "*"
    }
  ]
}
```

---

## 📦 Modules

### Core Modules

| Module | Description | File |
|--------|-------------|------|
| Main Application | Primary Streamlit interface | `streamlit_app.py` |
| Account Lifecycle | Onboarding/offboarding workflows | `account_lifecycle_enhanced.py` |
| SCP Policy Engine | Service Control Policy management | `scp_policy_engine.py` |
| FinOps Dashboard | Cost management and optimization | `finops_module_enhanced_complete.py` |
| AI Threat Analysis | Claude AI security analysis | `ai_threat_scene_6_PRODUCTION.py` |

### Security Modules

| Module | Description | File |
|--------|-------------|------|
| EKS Vulnerabilities | Container security scanning | `eks_container_vulnerability_module.py` |
| EKS Enterprise | Full enterprise vulnerability dashboard | `eks_vulnerability_enterprise_complete.py` |
| Batch Remediation | Bulk vulnerability remediation | `batch_remediation_production.py` |
| Code Generation | AI-powered remediation scripts | `code_generation_production.py` |

### OS Remediation Modules

| Module | Description | File |
|--------|-------------|------|
| Windows Remediation | Windows Server patching (2012-2025) | `windows_server_remediation_MERGED_ENHANCED.py` |
| Linux Remediation | Multi-distro patching (Ubuntu, RHEL, Amazon Linux) | `linux_distribution_remediation_MERGED_ENHANCED.py` |

### Integration Modules

| Module | Description | File |
|--------|-------------|------|
| Enterprise Integration | ITSM and notification integrations | `integration_scene_8_complete.py` |
| Pipeline Simulator | CI/CD security gate simulation | `pipeline_simulator.py` |
| AI Configuration | Natural language configuration | `ai_configuration_assistant_complete.py` |

---

## 📸 Screenshots

### Executive Dashboard
> Real-time compliance and security overview with key performance indicators

![Executive Dashboard](assets/screenshots/dashboard.svg)

### AI Threat Analysis
> Claude AI-powered threat detection and automated remediation recommendations

![AI Threat Analysis](assets/screenshots/ai-threat.svg)

### FinOps Intelligence
> Cost optimization, forecasting, and chargeback management

![FinOps Dashboard](assets/screenshots/finops.svg)

### Compliance Framework
> Multi-framework compliance mapping and evidence collection

![Compliance Framework](assets/screenshots/compliance.svg)

---

## 🏛️ Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         Cloud Compliance Canvas                              │
│                      Enterprise Governance Platform                          │
├─────────────────────────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │
│  │  Executive   │  │   Security   │  │    FinOps    │  │  Compliance  │    │
│  │  Dashboard   │  │   Center     │  │  Dashboard   │  │   Manager    │    │
│  └──────────────┘  └──────────────┘  └──────────────┘  └──────────────┘    │
├─────────────────────────────────────────────────────────────────────────────┤
│                          Core Services Layer                                 │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │  Account Lifecycle │ Policy Engine │ Remediation │ AI Analysis      │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
├─────────────────────────────────────────────────────────────────────────────┤
│                          AWS Integration Layer                               │
│  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐    │
│  │ Security  │ │ GuardDuty │ │   Config  │ │ Inspector │ │   Cost    │    │
│  │    Hub    │ │           │ │           │ │           │ │ Explorer  │    │
│  └───────────┘ └───────────┘ └───────────┘ └───────────┘ └───────────┘    │
├─────────────────────────────────────────────────────────────────────────────┤
│                          External Integrations                               │
│  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐    │
│  │   Jira    │ │ServiceNow │ │   Slack   │ │  GitHub   │ │ Snowflake │    │
│  └───────────┘ └───────────┘ └───────────┘ └───────────┘ └───────────┘    │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Technology Stack

| Layer | Technologies |
|-------|--------------|
| Frontend | Streamlit, Plotly, Pandas |
| AI/ML | AWS Bedrock (Claude 3.5), Anthropic API |
| AWS Security | Security Hub, GuardDuty, Config, Inspector, CloudTrail |
| AWS FinOps | Cost Explorer, Budgets, Trusted Advisor |
| Policy | OPA, Sentinel, Cloud Custodian, SCPs |
| Security Tools | Wiz.io, Snyk, KICS, Checkov, GitHub GHAS |
| Integration | Jira, ServiceNow, Slack, PagerDuty |
| Data | Snowflake, Apptio Cloudability |

---

## 🚀 Demo Mode

The application includes a **Demo Mode** that provides realistic simulated data for demonstrations and testing without requiring AWS credentials.

Toggle between Demo and Live modes in the sidebar:

```
🎮 Demo Mode: Simulated enterprise data
🔴 Live Mode: Real AWS account data
```

---

## 📚 Documentation

- [AWS Deployment Utility Guide](AWS_DEPLOYMENT_UTILITY_GUIDE.md)
- [Streamlit Cloud Quickstart](STREAMLIT_CLOUD_QUICKSTART.md)
- [Deployment Utility Reference](DEPLOYMENT_UTILITY_ANSWER.md)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

---

## 📝 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🔧 Integrated Technologies

<div align="center">

| AWS Services | Security Tools | FinOps | Integration |
|:------------:|:--------------:|:------:|:-----------:|
| Security Hub | Wiz.io | Cloudability | Jira |
| GuardDuty | Snyk | CloudHealth | ServiceNow |
| Config | KICS | Snowflake | Slack |
| Inspector | Checkov | — | PagerDuty |
| CloudTrail | GitHub GHAS | — | GitHub |
| Organizations | OPA | — | GitLab |

</div>

---

<div align="center">

**Built for Enterprise Cloud Governance Excellence**

☁️ Cloud Compliance Canvas v6.0 Enterprise Edition

⭐ Star this repository if you find it helpful!

</div>
