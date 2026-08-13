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
