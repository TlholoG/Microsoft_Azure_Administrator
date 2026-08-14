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
