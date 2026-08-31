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
