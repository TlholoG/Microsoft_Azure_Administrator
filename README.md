# ☁️ Microsoft Azure Administrator — AZ-104 Labs

A hands-on Azure administration learning repository documenting my practical work while completing **Microsoft Azure Administrator (AZ-104) training**.

This repository contains daily learning notes, Azure deployment files, PowerShell and Azure CLI commands, configuration exercises, troubleshooting experiences, and practical labs completed throughout my training.

The repository is intended to document my progression from learning individual Azure concepts to applying them through practical administration and deployment tasks.

---

## 🎯 Objectives

The main objectives of this repository are to:

* Develop practical Azure administration skills.
* Prepare for the Microsoft AZ-104 certification.
* Practice deploying and managing Azure resources.
* Learn Azure administration through both the Azure Portal and command-line tools.
* Develop proficiency with Azure PowerShell and Azure CLI.
* Practice infrastructure deployment using ARM templates.
* Understand Microsoft Entra ID and Azure role-based access control.
* Apply Azure governance and policy concepts.
* Document troubleshooting experiences and solutions.
* Maintain a record of my daily technical learning and progress.

---

## 🧪 Practical Labs

The repository contains hands-on exercises covering areas such as:

### Azure Resource Management

* Resource groups
* Resource deployment
* Resource management
* Resource locks
* Azure Resource Manager
* ARM templates

### Identity & Access Management

* Microsoft Entra ID
* Users and groups
* Administrative Units
* Role-Based Access Control (RBAC)
* Azure role assignments
* Microsoft Entra licensing
* Self-Service Password Reset (SSPR)

### Azure Storage

* Storage accounts
* Blob storage
* Containers
* Storage permissions
* Azure Storage RBAC
* Microsoft Entra authorization
* Storage security configuration

### Governance

* Azure Policy
* Policy assignments
* Custom policies
* Compliance monitoring
* Resource governance

### Networking

* Azure networking concepts
* Network configuration
* Connectivity
* Network security concepts

### Monitoring & Management

* Azure Monitor
* Activity logs
* Resource monitoring
* Troubleshooting deployments

---

## ⚙️ Infrastructure as Code & Automation

A significant part of the training involves learning how Azure resources can be deployed and managed programmatically.

Technologies and approaches explored include:

* Azure PowerShell
* Azure CLI
* ARM templates
* JSON
* Bash
* PowerShell scripting

For example, ARM templates are used to define Azure resources declaratively rather than creating every resource manually through the Azure Portal.

Example deployment structure:

```text
Parameters
     ↓
ARM Template
     ↓
Resource Deployment
     ↓
Azure Resource Group
     ↓
Azure Resource
     ↓
Outputs
```

The repository contains deployment files used during the practical labs.

---

## 📝 Daily Learning Log

The `az104-daily-learning-log.md` file documents my learning progression throughout the training.

Each entry records the concepts covered and practical work completed during the day.

Topics documented include:

* Azure administration
* Microsoft Entra ID
* RBAC
* Azure Storage
* Azure Policy
* ARM templates
* Azure CLI
* Azure PowerShell
* Resource deployment
* Troubleshooting
* Governance

The learning log is intended to capture not only what I learned, but also the practical problems encountered and how they were resolved.

---

## 📁 Repository Structure

```text
Microsoft_Azure_Administrator/
│
├── README.md
├── az104-daily-learning-log.md
├── az104-daily-learning-log.txt
├── az_notes.txt
└── azuredeploy.json
```

Additional lab files and deployment templates will be added as the training progresses.

---

## 🛠️ Technologies & Tools

* **Microsoft Azure**
* **Azure Portal**
* **Azure PowerShell**
* **Azure CLI**
* **PowerShell**
* **Bash**
* **ARM Templates**
* **JSON**
* **Microsoft Entra ID**
* **Azure RBAC**
* **Azure Policy**
* **Azure Storage**
* **Azure Monitor**
* **Git & GitHub**

---

## 🧠 Skills Being Developed

### Azure Administration

* Resource deployment and management
* Resource groups
* Azure Storage
* Azure networking
* Azure monitoring
* Azure governance

### Identity & Security

* Microsoft Entra ID
* RBAC
* Role assignments
* Access control
* Storage authorization
* Security configuration

### Automation

* Azure CLI
* Azure PowerShell
* PowerShell scripting
* ARM templates
* Infrastructure deployment

### Troubleshooting

* Deployment troubleshooting
* Azure activity logs
* Template validation
* Resource configuration issues
* Command-line troubleshooting

---

## 📈 Learning Progression

This repository is a living record of my development as an Azure Administrator.

The progression is moving from:

```text
Azure Fundamentals
       ↓
Azure Resource Management
       ↓
Identity & Access
       ↓
Storage
       ↓
Governance & Policy
       ↓
Networking
       ↓
Infrastructure Deployment
       ↓
Automation & Administration
```

The goal is to develop the ability to not only understand Azure services, but also **deploy, configure, manage, secure and troubleshoot them in practice**.

---

## 🚧 Current Status

**Active development**

This repository will continue to be updated throughout my AZ-104 training with:

* New daily learning entries
* Additional Azure labs
* PowerShell commands
* Azure CLI commands
* ARM templates
* Deployment configurations
* Troubleshooting notes
* Lessons learned

---

## ⚠️ Security Note

Deployment files in this repository are intended for educational purposes.

No passwords, access keys, connection strings, secrets, tokens, or other sensitive credentials should be committed to the repository.

Where sensitive values are required during deployment, they should be supplied through appropriate parameters, secure mechanisms, or environment-specific configuration rather than stored directly in source control.

---

## 🎓 Certification

This repository supports my preparation for the:

**Microsoft Certified: Azure Administrator Associate — AZ-104**

The practical work documented here complements the theoretical concepts covered through Microsoft Learn and instructor-led training.
