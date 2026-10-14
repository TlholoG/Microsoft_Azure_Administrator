**Question 380**


OverviewGeneral OverviewContoso, Ltd. is a consulting company that has a main office in Montreal and branch offices in Seattle and New York.EnvironmentExisting EnvironmentContoso has an Azure subscription named Sub1 that is linked to an Microsoft Entra ID (Microsoft Entra ID) tenant. The network contains an on-premises Active Directory domain that syncs to the Microsoft Entra ID tenant.The Microsoft Entra ID tenant contains the users shown in the following table.

Name    Type     Role
User1   Member   None
User2   Guest    None
User3   Member   None
User4   Member   None

Sub1 contains two resource groups named RG1 and RG2 and the virtual networks shown in the following table.

Name    Subnet             Peered with
VNET1   Subnet1, Subnet2   VNET2
VNET2   Subnet1            VNET1, VNET3
VNET3   Subnet1            VNET2
VNET4   Subnet1            None

User1 manages the resources in RG1. User4 manages the resources in RG2.

Sub1 contains virtual machines that run Windows Server 2019 as shown in the following table

Name   IP address    Location     Connected to
VM1    10.0.1.4      West US      VNET1/Subnet1
VM2    10.0.2.4      West US      VNET1/Subnet2
VM3    172.16.1.4    Central US   VNET2/Subnet1
VM4    192.168.1.4   West US      VNET3/Subnet1
VM5    10.0.22.4     East US      VNET4/Subnet1

No network security groups (NSGs) are associated to the network interfaces or the subnets.

Sub1 contains the storage accounts shown in the following table.

| Name     | Kind                           | Location   | File share               | Identity-based access for file share                 |
| -------- | ------------------------------ | ---------- | ------------------------ | ---------------------------------------------------- |
| storage1 | Storage (general purpose v1)   | West US    | sharea                   | Azure Active Directory Domain Services (Azure AD DS) |
| storage2 | StorageV2 (general purpose v2) | East US    | shareb, sharec           | Disabled                                             |
| storage3 | BlobStorage                    | East US 2  | **Not applicable** | **Not applicable**                             |
| storage4 | FileStorage                    | Central US | shared                   | Azure Active Directory Domain Services (Azure AD DS) |

Requirements

Planned Changes

Contoso plans to implement the following changes:

-Create a blob container named container1 and a file share named share1 that will use the Cool storage tier.

-Create a storage account named storage5 and configure storage replication for the Blob service.

-Create an NSG named NSG1 that will have the custom inbound security rules shown in the following table.

| Priority | Port | Protocol | Source      | Destination    | Action |
| -------- | ---- | -------- | ----------- | -------------- | ------ |
| 500      | 3389 | TCP      | 10.0.2.0/24 | Any            | Deny   |
| 1000     | Any  | ICMP     | Any         | VirtualNetwork | Allow  |

-Associate NSG1 to the network interface of VM1.

-Create an NSG named NSG2 that will have the custom outbound security rules shown in the following table.

| Priority | Port | Protocol | Source      | Destination    | Action |
| -------- | ---- | -------- | ----------- | -------------- | ------ |
| 200      | 3389 | TCP      | 10.0.0.0/16 | VirtualNetwork | Deny   |
| 400      | Any  | ICMP     | 10.0.2.0/24 | 10.0.1.0/24    | Allow  |

-Associate NSG2 to VNET1/Subnet2.

Technical RequirementsContoso must meet the following technical requirements:

-Create container1 and share1.-Use the principle of least privilege.

-Create an Microsoft Entra ID security group named Group4.

-Back up the Azure file shares and virtual machines by using Azure Backup.

-Trigger an alert if VM1 or VM2 has less than 20 GB of free space on volume C.

-Enable User1 to create Azure policy definitions and User2 to assign Azure policies to RG1.

-Create an internal Basic Azure Load Balancer named LB1 and connect the load balancer to VNET1/Subnet1

-Enable flow logging for IP traffic from VM5 and retain the flow logs for a period of eight months.

-Whenever possible, grant Group4 Azure role-based access control (Azure RBAC) read-only permissions to the Azure file shares.

You need to identify which storage account to use for the flow logging of IP traffic from VM5. The solution must meet the retention requirements.

Which storage account should you identify?

A. storage1
B. storage2
C. storage3
D. storage4


*Correct answer: B. storage2*

### *Step-by-step explanation*

*The requirement is to enable flow logging for IP traffic from VM5, which is connected to VNET4 in East US, and retain the logs for eight months.*

*Azure Network Watcher flow logs require a storage account to store the logged traffic data. The storage account must support the required configuration.*

| *Option*      | *Storage account type*           | *Suitable?*                                |
| -------------- | --------------------------------- | ------------------------------------------- |
| *A. storage1* | *General-purpose v1*             | *Not the best choice for this scenario*    |
| *B. storage2* | *General-purpose v2 (StorageV2)* | *Correct*                                  |
| *C. storage3* | *BlobStorage*                    | *Not the intended choice in this question* |
| *D. storage4* | *FileStorage*                    | *No — designed for premium Azure Files*   |

### *Why storage2?*

- *StorageV2 supports Azure Blob Storage, which is used to store Network Watcher flow logs.*
- *It supports lifecycle management and access tiers for managing stored data.*
- *The logs can be retained for eight months by configuring the appropriate retention and lifecycle settings.*

*Exam takeaway: When a question asks which storage account to use for Azure Network Watcher flow logs, look for a supported general-purpose storage account, typically StorageV2.*
