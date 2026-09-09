# 2026/08/12

## Microsoft Entra ID

Microsoft Entra ID was the focus of today's learning.

* Created and deleted users using an account with **Global Administrator** permissions.
* Created user groups and added users to the appropriate groups.
* Assigned **Administrative Units** to specific users.
* Learned that Administrative Units can be used to **restrict administrators to managing a specific subset of users**, rather than giving them access to manage all users in the directory.

### Key takeaway

Administrative Units provide a way to delegate administration within Microsoft Entra ID by limiting an administrator's management scope to a specific group of users.

# 2026/08/13

## Microsoft Entra ID & Azure Storage

Today's learning continued with **Microsoft Entra ID**, with a deeper focus on licensing, self-service password reset, and access control in Azure Storage.

* Learned more about **managing license usage and licensed features**, including how different Microsoft Entra licensing plans provide different capabilities and limitations, particularly **P1 vs P2**.
* Configured and explored **Self-Service Password Reset (SSPR)** and learned how password reset can be enabled for a specific group of users.
* Created an **Azure Storage Account** and worked with **Blob Storage**.
* Configured **Role-Based Access Control (RBAC)** to manage access to the storage resources.
* Learned that having **Global Administrator** permissions in Microsoft Entra ID does not automatically grant full access to every Azure resource. Certain resource-level permissions require an appropriate Azure RBAC role, such as **Owner**.
* Configured the storage account by:

  * Disabling **Allow Blob anonymous access**.
  * Enabling **Default to Microsoft Entra authorization in the Azure portal**.
* Gained a deeper understanding of how **RBAC inheritance** works when permissions are assigned at different scopes.
* Assigned myself an appropriate **Blob Storage data contributor role** to allow me to manage blob data.
* Assigned the users I created appropriate **Blob Storage reader roles**, allowing them to read blob data without giving them unnecessary write or administrative permissions.

### Key takeaway

Today's lab reinforced the distinction between **Microsoft Entra administrative roles and Azure RBAC roles**. Having a highly privileged identity role, such as Global Administrator, does not automatically provide access to Azure resource data. Access must be explicitly granted through the appropriate **RBAC role at the correct scope**, and permissions can be inherited from higher scopes such as the subscription or resource group.

# 2026/08/14

## Azure RBAC & Role Assignments

Today's learning focused heavily on **Azure Role-Based Access Control (RBAC)** and understanding how role assignments work across different scopes.

* Worked primarily with the **Owner** role to manage Azure resources and user access.
* Assigned users different **RBAC roles**, including **Contributor**, **Reader**, **Storage Blob Data Reader**, and **Storage Blob Data Contributor**.
* Assigned roles at different scopes, including the **subscription**, **resource group**, and individual resource levels.
* Created containers and uploaded files to **Blob Storage**, then tested user accounts to determine what actions their assigned permissions allowed them to perform.
* Tested whether users with different roles could **delete files** from Blob Storage. When a user was unable to delete a file, this confirmed that the assigned permissions were restricting the user as intended.
* Practiced how **role assignments at a higher scope can be inherited by resources and resource groups below that scope**.
* Compared permissions assigned at different levels to understand how **RBAC inheritance and effective permissions** work.
* Used these practical tests to reinforce the **principle of least privilege**, ensuring users were given only the level of access required for their tasks.

### Key takeaway

Today's lab helped me understand Azure RBAC more practically by testing permissions rather than only configuring them. I learned that role assignments can be applied at different scopes, with permissions inherited from higher scopes. I also saw how a broader role assignment, such as **Contributor at the subscription level**, can provide permissions across the resources within that scope. Testing user accounts by attempting actions such as deleting Blob Storage files helped me verify that my RBAC configurations were working as intended.

# 2026/08/16

## Azure ARM Templates & Template Parameters

Today's learning focused on **Azure Resource Manager (ARM) templates**, understanding how deployments behave when no resources are defined, and making templates more flexible and secure through the use of **parameters**.

* Deployed an ARM template with an empty `resources` array (`[]`). The deployment was successful and was recorded in the **Activity Log**, but no Azure resource was created because the template did not specify any resources to deploy.
* Updated the `azuredeploy.json` template to include a **Storage Account** resource using the resource type `Microsoft.Storage/storageAccounts`.
* Successfully deployed the updated ARM template and observed that the **Activity Log** reflected a different deployment status, showing **Accepted** during the deployment process.
* Learned that an ARM template can be used to define Azure resources declaratively, with the resources that are created determined by what is specified in the template.
* Updated the ARM template to make it more **flexible and reusable** rather than hardcoding configuration values directly into the template.
* Learned that **parameters** should be used for settings that may vary between environments, such as **SKU, size, capacity, and resource names**.
* Learned an important security practice: **never hardcode usernames or passwords** in ARM templates or provide default values for them.
* Learned that usernames, passwords, and other sensitive information should be supplied through **parameters** rather than being embedded directly in the template.
* Learned to use the **`secureString`** parameter type for passwords and other sensitive string values.
* Learned that when sensitive information needs to be passed as a JSON object, the **`secureObject`** parameter type should be used.
* Learned that template parameters using **`secureString`** or **`secureObject`** cannot be read or harvested after the deployment, helping to protect sensitive information.

### Key takeaway

Today's lab helped me understand that a successful ARM template deployment does not necessarily mean that a resource was created. When the `resources` array was empty, Azure successfully processed the deployment but had nothing to deploy. Adding a Storage Account resource to the template resulted in an actual resource deployment. I also learned the importance of using **parameters** to make ARM templates flexible and reusable across different environments, while sensitive information such as usernames and passwords should never be hardcoded. Using **`secureString`** and **`secureObject`** helps protect sensitive values during and after deployment.

## Azure Policies & Custom Policy Definitions

Today's learning focused on **Azure Policy**, understanding how policies are deployed, customized, assigned throughout the Azure hierarchy, and created from scratch using JSON.

* Learned how to **deploy Azure Policies** and configure policy assignments to enforce organizational rules and standards.
* Added and customized policies within Azure and observed how policies can be applied at different levels of the **Azure resource hierarchy**.
* Learned that policies can be assigned at different scopes, including the **management group, subscription, resource group, and individual resource levels**, depending on where governance is required.
* Learned how to monitor the **compliance status** of deployed policies from the Azure Policy dashboard.
* Observed that the compliance dashboard provides an overview of resources and their compliance with the policies that have been assigned.
* Learned that Azure Policies can be created from scratch using **JSON policy definitions**, providing greater control over the rules and conditions being enforced.
* Created **custom policies** and used Azure's generated policy template as a starting point before modifying the JSON definition.
* Modified the generated JSON template through the **Start with a blank/custom definition** approach to develop my own policy logic.
* Learned that Azure Policy provides a way to automate and enforce **governance, compliance, and configuration standards** across Azure environments.

### Key takeaway

Today's lab helped me understand how **Azure Policy** can be used to govern and monitor resources across an Azure environment. I learned that policies can be assigned at different levels of the Azure hierarchy, allowing governance rules to be applied at an appropriate scope. I also learned how to monitor policy compliance from the Azure dashboard and how to create **custom policy definitions using JSON**. Using Azure's generated templates as a starting point and modifying the JSON made it possible to develop my own custom policies rather than relying only on the built-in policies provided by Azure.

# 2026/08/18

## Azure PowerShell & Resource Deployment

Today's learning focused on going deeper into **Azure PowerShell**, including installing and configuring the required tools and using PowerShell to deploy Azure resources.

* Performed the required **PowerShell installations and configurations** for working with Azure.
* Started by deploying an **Azure Storage Account** using the Azure CLI and explored the different ways Azure resources can be deployed.
* Learned that Azure resources can be deployed using different approaches, including **JSON ARM templates, Bicep files, and scripts created from scratch**.
* Learned that instead of creating deployment templates from scratch, an existing Azure resource can be used as a starting point. From the resource's **Automation** menu, I could download the **ARM template, parameters file, and Bicep file**.
* Used these downloaded files as a **skeleton for the deployment configuration**, which made it easier to understand the required structure and configuration rather than starting with an empty file.
* Customized the downloaded templates in **Visual Studio Code** before deploying the resources.
* Used the **Deploy a custom template** feature to deploy the customized configurations and practiced carrying out the deployments using **PowerShell**.
* Repeated the exercise with different Azure resources, starting with a **Storage Account**, followed by a **Virtual Network**, and finally a **Virtual Machine**.
* Found that the **Virtual Machine deployment template** required significantly more attention than the Storage Account and Virtual Network templates because it contained more parameters and configuration settings that needed to be carefully reviewed and customized.
* Learned that while some resource templates can be relatively straightforward to modify, more complex resources require a better understanding of how the **template and parameter values work together** before deployment.

### Key takeaway

Today's lab gave me a better understanding of the different ways Azure resources can be deployed and how **PowerShell can be used as part of the deployment process**. I found that using an existing resource's exported ARM template, parameters, or Bicep file provides a useful starting point instead of building a deployment from scratch. I also learned that the complexity of a template depends heavily on the resource being deployed. Storage Accounts and Virtual Networks were relatively straightforward to customize, while the Virtual Machine template required much more careful attention to its parameters and configuration.

# 2026/08/19

## Microsoft Entra ID — Identity Management

Today's learning focused on **creating, configuring, and managing identities** in Microsoft Entra ID.

* Worked through exercises covering the **creation, configuration, and management of users**.
* Practiced creating and configuring user accounts in Microsoft Entra ID.
* Completed an exercise on **assigning licenses to users** and learned how licenses provide users with access to specific Microsoft services and features.
* Completed an exercise on **restoring and removing deleted users**.
* Learned how deleted user accounts can be managed and restored when necessary.

### Key takeaway

Today's exercises gave me more practical experience with **identity and user management in Microsoft Entra ID**. I learned how to create and configure users, assign the appropriate licenses, and manage deleted accounts by either restoring them or removing them when they are no longer required.

# 2026/08/20

## Microsoft Entra ID — Groups & Device Registration

Today's learning continued with **creating, configuring, and managing identities** in Microsoft Entra ID, with a focus on groups and device registration.

* Continued working through the identity management exercises in Microsoft Entra ID.
* Completed an exercise on **adding groups in Microsoft Entra ID**.
* Practiced creating and managing groups to organize users and manage access more effectively.
* Worked through an exercise on **configuring and managing device registration**.
* Learned how devices can be registered with Microsoft Entra ID and managed as part of an organization's identity environment.

### Key takeaway

Today's exercises expanded my understanding of **Microsoft Entra ID identity management** by showing how groups can be used to organize and manage users and how **device registration** connects devices to the organization's identity environment.

# 2026/08/27

## Azure Administrator, Network Administrator & Database Administrator Responsibilities

Today's learning focused on understanding the **core operational responsibilities of an Azure Administrator** and how these responsibilities differ from those of a **Network Administrator** and **Database Administrator** in an organization migrating from on-premises infrastructure to Azure.

* Identified five key responsibilities of an **Azure Administrator**:

  * Deploying and managing **virtual machines** and configuring the required compute resources.
  * Managing and configuring **Azure networking**.
  * Managing **Azure identities**, including creating, deleting, and merging users from directories outside of Microsoft Entra ID.
  * Deploying and managing **Azure Storage**, including storage accounts, blobs, containers, and files, while also managing storage security.
  * Monitoring the **usage, health, and performance of resources** deployed within the tenant.
* Learned that a **Network Administrator** remains responsible for the organization's physical and network infrastructure, including:

  * Configuring and installing network infrastructure and ensuring internet connectivity.
  * Implementing network security protocols, managing firewalls, and preventing unauthorized or unsecured access.
  * Managing network hardware such as **routers and switches** to ensure on-site computers can connect to the internet and cloud resources.
  * Troubleshooting network connectivity problems.
  * Monitoring network health and maintaining availability for critical operations while minimizing downtime.
* Considered how the responsibilities of a traditional Network Administrator may change as an organization moves more infrastructure to the cloud, with some day-to-day infrastructure responsibilities shifting toward cloud administration.
* Learned that a **Database Administrator (DBA)** is responsible for managing and maintaining the organization's databases and the data stored within them.
* Identified key DBA responsibilities, including:

  * Installing and configuring **database management systems** on deployed virtual machines.
  * Securing databases and managing permissions and access to data.
  * Ensuring databases are backed up and that **recovery and disaster-management plans** are in place.
  * Optimizing databases to maintain good performance when data is queried.
  * Keeping database systems **updated and maintained**.

### Key takeaway

Today's exercise helped me understand that although Azure, networking, and database administration can overlap, they have different areas of responsibility. The **Azure Administrator** focuses on managing cloud resources such as compute, networking, storage, identities, and monitoring. The **Network Administrator** focuses primarily on connectivity, network infrastructure, and network security, while the **Database Administrator** focuses on the databases themselves, including their security, backups, performance, and maintenance.

# 2026/08/28

## Remote Desktop, Windows Server & Virtual Machine Storage

Today's learning focused on completing my **formative assessment** and gaining practical experience with **Remote Desktop Protocol (RDP)**, Windows Server, and storage management within a virtual machine.

* Completed and submitted the remaining sections of my **formative assessment**.
* Practiced using **Remote Desktop Protocol (RDP)** to remotely connect to a virtual machine.
* Installed **Windows Server Datacenter** on a virtual machine.
* Learned that a **virtual machine requires an operating system** in order to function and provide a usable environment.
* Learned that although a virtual machine is provisioned with a virtual hard disk by default, additional virtual disks can be created and **attached to the virtual machine** when additional storage is required.
* Learned that separating the operating system disk from a data disk can help protect data from issues affecting the operating system disk and makes the data independent of the operating system.
* Practiced preparing a newly attached disk so that it could be used by the operating system.
* Learned that before a newly attached disk can be used normally, it needs to be **initialized and configured with a volume and drive letter**.
* Learned how to **partition and format the new drive** within the Windows Server virtual machine so that it can be used for storing data.

### Key takeaway

Today's practical work helped me understand how **operating systems and storage work within Azure virtual machines**. I learned that a VM needs an operating system to function and that additional virtual disks can be attached to separate data from the operating system. This provides greater flexibility when managing and protecting data because the data can remain separate from the disk containing the operating system.

# 2026/08/29

## Microsoft Cloud Adoption Framework for Azure – Cloud Governance

Today I worked through the Microsoft Learn chapter on the **Microsoft Cloud Adoption Framework for Azure** and focused on the **Govern** methodology. I learned that the Cloud Adoption Framework provides guidance, best practices, documentation, and tools to help organizations successfully plan, adopt, manage, and govern their Azure environments.

* Learned that the **Microsoft Cloud Adoption Framework for Azure** is an end-to-end framework designed to help organizations achieve their cloud adoption objectives.
* Learned that cloud governance is the process of **managing and controlling how cloud resources and services are used within an organization**.
* Learned that the **Govern methodology** provides a structured approach for establishing and improving cloud governance in Azure.
* Learned that cloud governance covers several important areas, including:

  * Regulatory compliance
  * Security
  * Operations
  * Cost management
  * Data management
  * Resource management
  * Artificial intelligence (AI)
* Learned that **Azure Policy** plays an important role in cloud governance by helping organizations enforce rules and maintain control over their Azure environments.
* Learned that effective governance helps reduce risks and ensures that cloud activities remain aligned with the organization's overall cloud strategy and business objectives.
* Learned that cloud governance is **not a once-off activity**. It is a continuous process that requires regular monitoring, evaluation, and adjustment as technology, risks, and compliance requirements change.
* Learned the five steps of the Cloud Adoption Framework's **Govern** methodology:

  1. **Build a governance team** – establish a team responsible for defining, maintaining, and reporting on governance policies.
  2. **Assess cloud risks** – identify and assess risks relating to areas such as security, compliance, costs, data, resources, operations, and AI.
  3. **Document cloud governance policies** – define clear rules and guidelines for acceptable cloud usage.
  4. **Enforce cloud governance policies** – use automated tools and manual oversight to ensure resources comply with the established policies.
  5. **Monitor cloud governance** – continuously monitor the environment and governance processes to maintain compliance.
* Learned that after establishing governance, organizations should regularly revisit **steps 2–5** to adapt their governance approach over time.

### Key takeaway

Today I learned that managing an Azure environment is not only about creating and configuring resources. Organizations also need governance to control how those resources are used, manage costs and risks, maintain security and compliance, and ensure that cloud usage supports business objectives. I also learned that Azure Policy can be used as an important tool for creating **guardrails** that help keep an Azure environment within the organization's defined rules and standards.

# 2026/08/31

## Virtual Machine Deployment and CyberPanel Installation

Today I continued my practical Azure training by creating and configuring a virtual machine and connecting to it remotely. I worked with both Windows Server and Linux, gaining practical experience with deploying a VM and accessing it using PowerShell.

### What I learned and did

* Created an Azure Virtual Machine and selected **Windows Server Datacenter** as the initial operating system option.
* Worked with **Ubuntu 22.04** on the virtual machine for the Linux environment.
* Installed **CyberPanel** on the Ubuntu virtual machine.
* Used **PowerShell on my local computer** to remotely connect and log in to the virtual machine.
* Practiced managing a cloud-based server remotely rather than working directly from the Azure portal.
* Learned that Azure VMs can be used to host different server environments and applications depending on the operating system and configuration.

### Next Exercise – Virtual Machine Scale Sets (VMSS)

The next part of the exercise introduces **Virtual Machine Scale Sets (VMSS)**. I will deploy a scale set and practice adjusting its flexibility by changing the number of virtual machines in the scale set. I will also continue practising remote access to the virtual machines.

## Key takeaway

Today I gained more practical experience with Azure virtual machines by deploying a server environment, installing CyberPanel on Ubuntu, and remotely accessing the VM using PowerShell. The next step is to build on this knowledge by learning how Virtual Machine Scale Sets allow multiple VMs to be managed together and scaled according to requirements.

## 2026/09/01

### Assignment Preparation and Azure Administration Review

Today I focused on working through questions for my Azure Administrator assignments and formative assessments. Rather than completing new practical Azure labs, I spent the day applying the knowledge I have gained from previous practical exercises to scenario-based questions.

* Worked through **Azure troubleshooting scenarios**, including investigating why a user might be unable to provision a Virtual Machine.
* Reviewed how to troubleshoot **RBAC assignments, Azure Policies, subscription limits, resource locks, and Resource Group constraints**.
* Worked through **Azure tagging standards**, including the use of `Environment`, `Owner`, `Department`, and `CostCentre` tags.
* Considered how Azure tags support **Cost Management, budgeting, cost allocation, accountability, and enterprise auditing**.
* Worked through a **Microsoft Entra ID user-provisioning scenario** involving creating new users, assigning temporary credentials, and requiring a password change during the first login.
* Worked through an **Azure Management Groups hierarchy** scenario involving a Holding Company and regional divisions in South Africa, Botswana, Namibia, and Zimbabwe.
* Applied the Azure hierarchy of **Management Groups → Subscriptions → Resource Groups → Resources** to a practical enterprise governance scenario.
* Focused on understanding **how Azure governance can be structured to provide regional control while maintaining central cost and policy governance**.

### Key takeaway

Today was mainly about **putting the practical knowledge I have gained into written, scenario-based answers**. I am starting to see how the individual Azure concepts I have been learning—such as RBAC, Policy, tagging, Management Groups, subscriptions, and Resource Groups—fit together as part of an overall **Azure administration and governance strategy**.

# 2026/09/03

## Virtual Machine Scale Sets, Networking & Azure Container Apps

Today's learning focused on **Virtual Machine Scale Sets (VMSS)**, Azure virtual networking, and the introduction of **Azure Container Apps** and the **Platform as a Service (PaaS)** model. I gained practical experience with how Azure can automatically scale compute resources based on workload demand, as well as how virtual machines communicate through subnets and how Azure container-based services can reduce the need to manage the underlying infrastructure.

* Learned about **Virtual Machine Scale Sets (VMSS)** and how they allow multiple virtual machines to be deployed and managed as a group.
* Learned that VM Scale Sets can automatically **scale out** by adding additional VM instances when demand increases and **scale in** when demand decreases.
* Practiced configuring scaling rules for a VM Scale Set based on **CPU utilization**.
* Used the Linux `stress` command to intentionally increase the CPU workload of a virtual machine. This allowed me to observe the VM reaching its CPU threshold and trigger the scaling rules that had been configured.
* After stopping the `stress` process, the CPU utilization decreased, allowing me to observe the VM Scale Set **scale down** as the workload returned to normal.
* Learned about **subnets** and how virtual machines that need to communicate with one another can be placed within the same subnet to allow communication over the virtual network.
* Learned that a **network interface card (NIC)** is an important component of an Azure virtual machine because it provides the network connection between the VM and the Azure virtual network and subnet.
* Learned that when creating an Azure virtual network, an **address space** must be defined and subnets are created within that address space. Virtual machines can then be connected to the appropriate subnet through their network interfaces.
* Learned how **jump servers** or proxy servers can be used to provide controlled access to virtual machines. Because access can be routed through the jump server, individual VMs do not necessarily need to have their own **public IP addresses**, which can reduce their direct exposure to the internet.
* Introduction to **Azure Container Apps**, learning how Azure can host containerized applications without requiring me to manage the underlying virtual machines directly.
* Learned the distinction between a **container** and a **container app**. A container itself does not provide the application-level scaling capability, while Azure Container Apps provides the platform for running containers and can automatically scale the application based on demand.
* Created a container application containing **two containers** using an **ARM template**, giving me practical experience with infrastructure-as-code for deploying container-based workloads.
* Learned how **Platform as a Service (PaaS)** abstracts much of the underlying infrastructure from the administrator, allowing the focus to shift from managing servers and hardware to managing the application and its configuration.
* Learned that **serverless services in Azure** further abstract the underlying infrastructure. Azure manages the underlying compute, CPU, memory, storage, and other infrastructure resources in the background, while I interact primarily with the service and application rather than managing the physical hardware.

### Key takeaway

Today's practical work helped me understand how Azure can provide **elasticity and infrastructure abstraction**. With Virtual Machine Scale Sets, I learned how Azure can automatically respond to changing workloads by scaling compute resources up or down. I also learned how networking components such as **virtual networks, subnets, and network interface cards** allow virtual machines to communicate securely. Finally, learning about Azure Container Apps and serverless services showed me how PaaS can reduce the amount of infrastructure that an administrator needs to manage, allowing more focus on the applications and workloads running in Azure.

# 2026/09/04

## Visual Studio, Docker, WSL2 & Azure Container Registry

Today I focused on learning about **containerized applications** and how an application developed locally can be packaged using Docker and published to an Azure container registry. I installed and configured **Visual Studio, Docker Desktop, and Windows Subsystem for Linux 2 (WSL2)** before creating a web application and publishing it from Visual Studio.

The practical exercise involved several troubleshooting steps because the local development environment was not initially configured correctly. This gave me additional experience in identifying and resolving infrastructure and configuration issues before successfully publishing the application to Azure.

### What I learned and did

* Installed **Visual Studio** as the development environment for creating the web application.
* Installed **Docker Desktop** to provide the containerization environment required to build and run containers locally.
* Installed and configured **Windows Subsystem for Linux 2 (WSL2)**, which can provide the Linux-based backend used by Docker Desktop on Windows.
* Learned about **containers** and how an application can be packaged together with its required dependencies into a portable container image.
* Troubleshot an issue where the **Docker Engine would not start** because hardware virtualization was disabled on the computer.
* Investigated the issue and determined that virtualization had to be enabled through the computer's **BIOS/UEFI firmware settings**.
* Enabled **hardware virtualization** in the BIOS/UEFI, after which the Docker Engine was able to start successfully.
* Created a web application named **WebApplication2** in Visual Studio using the **.NET 7 framework** to practise working with an older framework version and compatibility requirements.
* Encountered errors while working with the application template and determined that **Docker Desktop and the Docker Engine needed to be running in the background** before the container-related operations in Visual Studio could be performed successfully.
* Configured the **NuGet package source** as `nuget.org`, using the service endpoint `https://api.nuget.org/v3/index.json`, allowing the .NET application to retrieve the required packages during the build process.
* Successfully used Visual Studio's **Publish** functionality to build and package the application as a Docker container image.
* Published the container image to an **Azure Container Registry (ACR)** named **tlholocontainerregistry**.
* Verified the result in the Azure portal by navigating through **TlholoResources → tlholocontainerregistry → Services → Repositories** and confirming that the published application was present in the registry.
* Learned that **Azure Container Registry** provides a managed repository for storing and managing container images that can subsequently be used by Azure container hosting services.
* Gained an introduction to the **Platform as a Service (PaaS)** approach, where Azure can manage the underlying infrastructure required to run an application while the administrator focuses on the application and its configuration.

### Azure Resources Used

The Azure resources I worked with during the exercise were:

* **Resource Group – `TlholoResources`**: Provided the logical management boundary for the Azure resources used in the exercise.
* **Azure Container Registry – `tlholocontainerregistry`**: Provided the managed container registry where the Docker image produced from **WebApplication2** was published and stored.
* **Repositories**: Used within the Azure Container Registry to view the container images that had been pushed to the registry.

### Key takeaway

Today's practical exercise helped me understand the beginning of the **end-to-end container deployment workflow**. I developed an application in Visual Studio, used Docker to containerize it, and successfully published the resulting container image to **Azure Container Registry**. The troubleshooting was particularly valuable because I had to identify that hardware virtualization was disabled at the BIOS/UEFI level and that the Docker Engine needed to be running before Visual Studio could perform the container operations.

I also gained a clearer understanding of the role of **Azure Container Registry** within a containerized environment: the registry provides a managed location for storing container images, while a separate Azure container hosting service can subsequently retrieve and run those images. This introduced me to the broader **PaaS and managed-container model** in Azure.

# 2026/09/05

## Cloud Adoption Framework for Azure

Today I completed studying the **Cloud Adoption Framework for Azure (CAF)**, focusing on the governance aspects of adopting and managing cloud resources. The section introduced the importance of establishing governance policies that address business requirements, regulatory obligations, security, cost management, and operational consistency.

### What I learned and did

* Studied the **Cloud Adoption Framework for Azure** and its role in helping organizations plan, adopt, govern, and manage their Azure environment.
* Learned about the key considerations when defining a **cloud governance policy**, including:

  * **Business risk** – identifying and managing risks associated with cloud adoption.
  * **Policy and compliance** – ensuring that cloud resources and workloads comply with organizational policies, regulatory requirements, and industry standards.
  * **Process** – establishing consistent processes for managing and governing cloud resources.
* Studied the **five core disciplines of cloud governance**:

  * **Cost Management** – monitoring and controlling cloud expenditure, managing IT costs, and adjusting resources according to demand to ensure that cloud investments provide appropriate value.
  * **Security Baseline** – establishing and enforcing a minimum security standard across cloud adoption efforts to ensure that resources meet organizational security requirements.
  * **Resource Consistency** – maintaining consistent resource configurations and establishing standardized practices for resource onboarding, recovery, and discoverability.
  * **Identity Baseline** – establishing consistent identity and access-management standards, including the appropriate definition and assignment of roles and permissions.
  * **Deployment Acceleration** – improving the speed and consistency of deployments through centralized governance, standardized processes, and reusable deployment templates.
* Learned that **Azure Policy** is a primary Azure governance service used to enforce organizational standards and evaluate resource compliance at scale.
* Learned that Azure Policy can be applied to **existing resources as well as resources deployed in the future**, allowing organizations to establish governance guardrails across their Azure environment.
* Learned how Azure Policy can be used to assess whether resources comply with defined organizational requirements and identify non-compliant resources.
* Connected the concepts of **Azure Policy, governance, compliance, security, cost management, and resource consistency** to the practical Azure administration exercises I have completed previously.

### Key takeaway

Today's study helped me understand that **Azure administration is not only about deploying and maintaining resources**, but also about ensuring that those resources remain secure, compliant, consistent, and cost-effective. The **Cloud Adoption Framework for Azure** provides a broader governance framework, while services such as **Azure Policy** provide practical mechanisms for enforcing governance requirements within Azure. This builds on the practical policy and governance exercises I have already completed and gives me a better understanding of how those individual Azure administration tasks fit into an **enterprise cloud governance strategy**.

# 2026/09/06

## Azure Policy Design Principles, Governance & Azure Resource Manager

Today I completed studying the section **"Azure Policy Design Principles"**, focusing on how Azure governance is designed and implemented to maintain control over cloud resources and workloads. I also studied the **Azure resource hierarchy** and the distinction between **control plane and data plane operations** within Azure Resource Manager.

### What I learned and did

* Studied the role of **governance in Azure** and how governance mechanisms and processes help organizations maintain control over applications, resources, security, and cloud expenditure.
* Learned that effective Azure governance requires **planning policies and establishing strategic priorities** before implementing governance controls.
* Learned that cloud resources should be organized in a structured manner to support **security, resource management, cost tracking, and workload governance**.
* Studied the **Azure management hierarchy**, beginning with the **tenant root management group**, followed by management groups, subscriptions, resource groups, and individual resources.
* Learned that Azure management groups can be organized into a hierarchy extending to **six levels beneath the tenant root group**, allowing organizations to structure governance according to their organizational requirements.
* Reviewed the role of **Azure Resource Manager (ARM)** as the management layer responsible for handling Azure's **control plane operations**.
* Learned the distinction between the **control plane and data plane**:

  * **Control plane** – used to create, configure, manage, and control Azure resources within a subscription.
  * **Data plane** – used to access and interact with the actual capabilities and data provided by a specific Azure resource.
* Learned that **Azure Policy operates primarily through the control plane** and integrates with **Azure Resource Manager** to evaluate and enforce organizational rules and compliance requirements.
* Learned that Azure Resource Manager provides a consistent management layer across Azure services, centralizing common management capabilities such as **resource deployment, access control, policy, and resource organization**.
* Studied how the **data plane** relates to the actual operations performed against data or application functionality within an Azure resource.
* Learned that governance and policy controls can influence whether resources and their configurations comply with organizational requirements, while the actual workload or data operations occur through the resource's **data plane**.

### Key takeaway

Today's study helped me understand where **Azure Policy and Azure Resource Manager fit within the overall Azure architecture**. The distinction between the **control plane and data plane** is particularly important because it separates the management of Azure resources from the actual operations performed by those resources. I also gained a better understanding of how the Azure hierarchy—from the **tenant root management group through management groups, subscriptions, resource groups, and resources**—provides the structure on which governance policies can be applied. This builds directly on my previous study of the **Cloud Adoption Framework and Azure governance**, showing how governance principles can be translated into practical controls using Azure Policy and Azure Resource Manager.



# 2026/09/07

## Azure App Services & Azure Container Registry

Today I focused on learning about **Azure App Service** and **Azure Container Registry (ACR)**, with an emphasis on understanding how applications and container images can be deployed and managed using Azure services. I learned that when an **App Service** is created, Azure automatically provides a **default domain name**, which can be used to access the hosted web application.

I also worked with **Azure Container Registry** and practised the process of obtaining a container image locally, running the image using Docker, and then preparing the image to be stored in an Azure container registry. This exercise helped me understand the relationship between **Docker containers, container images, Azure Container Registry, and Azure App Service**.

### What I learned and did

* Learned about **Azure App Service** and its role as a managed **Platform as a Service (PaaS)** offering for hosting web applications.
* Learned that an App Service is assigned a **default domain** when it is created, providing a standard endpoint through which the hosted application can be accessed.
* Created an **Azure Container Registry** to provide a managed repository for storing container images.
* Connected to Azure using **Azure PowerShell** with `Connect-AzAccount`.
* Used `Get-AzSubscription` to retrieve and view the Azure subscriptions available to my account.
* Used `Set-AzContext` to select the required Azure subscription context before performing subsequent Azure administration operations.
* Connected to the Azure Container Registry using `Connect-AzContainerRegistry`.
* Used **Docker** to pull the `nginx` container image to my local computer.
* Ran the NGINX container locally and mapped the container port to port **8080** on the local machine to test the containerized application.
* Used Docker image tagging to associate the local NGINX image with the target Azure Container Registry repository.
* Practised the process of pushing the tagged container image to **Azure Container Registry**, allowing the image to be stored in Azure and made available for use by Azure container-hosting services.
* Gained practical experience with the workflow of moving a container image from a **local Docker environment into Azure Container Registry**.

### Commands Used

The main PowerShell and Docker commands used during the exercise were:

```powershell
Connect-AzAccount
Get-AzSubscription
Set-AzContext -Subscription "fef0ee0f0e0"
Connect-AzContainerRegistry -Name tlholocontainer

docker login
docker pull nginx
docker run -it --rm -p 8080:80 nginx
docker tag nginx tlhoregistry/test/nginx
docker push tlhoregistry/test/nginx
```

### Azure Resources Used

The Azure resources and services I worked with during the exercise were:

* **Azure App Service** – Used to learn how Azure provides a managed platform for hosting web applications and automatically assigns a default domain.
* **Azure Container Registry** – Used as a managed repository for storing container images.
* **Azure PowerShell** – Used to authenticate to Azure, select the appropriate subscription context, and interact with Azure resources.
* **Docker** – Used locally to pull, run, tag, and prepare the NGINX container image for storage in Azure Container Registry.

### Key takeaway

Today's practical exercise helped me understand the **container deployment workflow from a local environment into Azure**. I used Docker to obtain and run an NGINX container image locally, tagged the image for the Azure Container Registry, and practised pushing the image into the registry.

I also gained a better understanding of the relationship between **Azure App Service and Azure Container Registry**. App Service provides a managed platform for hosting applications, while Azure Container Registry provides a centralized and managed location for storing container images that can be used by Azure services. This strengthened my understanding of **PaaS, containerization, container registries, and Azure application deployment** from an Azure administration perspective.


# 2026/09/08

## Azure Compute Service Strategy – Architecture Case Study

Today I completed an **Azure Compute Service Strategy case study** for ZTQ Solutions. The exercise required me to evaluate three different workload scenarios and recommend the most appropriate Azure compute hosting model based on each workload's architecture, technology stack, traffic patterns, operational requirements, and deployment characteristics.

The assessment focused on selecting between **Azure Virtual Machines (IaaS), Azure App Service (PaaS), and Azure Container Apps (ACA)**. Rather than selecting a service based only on the application technology, I evaluated the operational requirements of each workload and considered factors such as scalability, infrastructure management, deployment strategies, cost optimization, and the level of operating-system control required.

### What I learned and did

* Analysed the requirements of **three different application workloads** and assessed which Azure compute service best aligned with each workload's characteristics.
* Evaluated **Azure Virtual Machines, Azure App Service, and Azure Container Apps** as potential compute hosting models.
* Considered the difference between **IaaS and PaaS** when determining how much infrastructure management responsibility would remain with the organization.
* Assessed **Workload 1 – Public-Facing Marketing Platform**, which uses a Node.js/React stack with dynamic APIs and mixed static content.
* Identified that the workload experiences **variable and unpredictable traffic spikes**, particularly during marketing campaigns.
* Recommended **Azure App Service (PaaS)** for Workload 1 because the requirements prioritize high availability, reduced operating-system management, and deployment capabilities such as **staging validation and blue-green deployment swaps**.
* Assessed **Workload 2 – Recruitment Portal Microservices**, which consists of containerized .NET Core and Go APIs operating within a decoupled microservices architecture.
* Identified that the workload is **event-driven and asynchronous**, with demand fluctuating according to applicant submission volumes.
* Recommended **Azure Container Apps (ACA)** for Workload 2 because the architecture requires independently scalable microservices, the ability to **scale to zero when idle**, and progressive traffic splitting without requiring the organization to manage an underlying Kubernetes cluster.
* Assessed **Workload 3 – Legacy Learning Management System (LMS)**, which is a monolithic application with custom IIS configurations, Windows Server dependencies, media transcoding components, and legacy C++/SQL Server Agent workloads.
* Identified that this workload requires **full operating-system-level administrative control**, including registry modifications, custom drivers, and system agent installations.
* Recommended **Azure Virtual Machines (IaaS)** for Workload 3 because the application has legacy Windows Server dependencies and requires administrative control over the operating system and its configuration.
* Considered the requirement for **automated rolling upgrades across VM instances** when evaluating the VM-based strategy for the legacy workload.
* Presented my **architectural recommendations** and explained the reasoning behind the selected compute service for each scenario.
* Practised approaching Azure architecture decisions from a **requirements-first perspective**, rather than selecting a service based solely on familiarity with the technology.

### Recommended Compute Strategy

| Workload                          | Recommended Service              | Primary Reason                                                                                                 |
| --------------------------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Public-Facing Marketing Platform  | **Azure App Service**      | Managed PaaS hosting, high availability, reduced OS management, and staging/blue-green deployment capabilities |
| Recruitment Portal Microservices  | **Azure Container Apps**   | Containerized microservices, event-driven scaling, scale-to-zero, and progressive traffic splitting            |
| Legacy Learning Management System | **Azure Virtual Machines** | Full OS-level control and support for legacy Windows Server and application dependencies                       |

### Key takeaway

Today's case study strengthened my ability to **select an Azure compute service based on workload requirements rather than simply choosing the most familiar hosting model**. I learned that the appropriate compute strategy depends on factors such as application architecture, traffic behaviour, scalability requirements, deployment methodology, infrastructure-management responsibility, and the degree of operating-system control required.

The exercise also reinforced the distinction between the three approaches. **Azure App Service** is well suited to managed application hosting where minimizing infrastructure administration is important, **Azure Container Apps** is appropriate for containerized and independently scalable microservices, while **Azure Virtual Machines** provide the greater level of operating-system control required by workloads with legacy or highly customized infrastructure dependencies.

Presenting my recommendations allowed me to practise communicating an **Azure architectural decision and the reasoning behind it**, which is an important part of working with cloud infrastructure beyond simply deploying individual Azure resources.
