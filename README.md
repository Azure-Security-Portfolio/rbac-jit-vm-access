## Azure RBAC & Just-In-Time (JIT) VM Access Lab

Implementation of least-privilege access and privilege management in Microsoft Azure by enforcing Role-Based Access Control (RBAC) for Virtual Machines and enabling Just-In-Time (JIT) access with Microsoft Defender for Servers. Demonstrates real-world privilege reduction, RBAC best practices, and modern attack surface minimization in cloud environments.

---

## Table of Contents

- [Overview]
- [Real-World Risk]
- [What I Built]
- [Diagram]
- [Objectives]
- [Steps Performed]
  - [1. User and Group Creation]
  - [2. RBAC Role Assignment]
  - [3. Permission Verification]
  - [4. Defender for Servers / JIT Access]
  - [5. Cleanup]
- [Screenshots]
- [Lessons Learned]
- [References]

---

## Overview

This lab demonstrates how to apply least-privilege principles to Azure infrastructure using RBAC and (if available) Just-In-Time (JIT) VM access. RBAC is used to assign minimal, task-specific permissions to users. JIT, part of Defender for Servers, restricts VM management port exposure to narrow time windows, minimizing the attack surface. These controls align with Zero Trust, real-world privilege management, and compliance standards.

---

## Real-World Risk
Standing, excessive, or overly broad permissions are a leading cause of cloud breaches. Attackers often target accounts with unnecessary admin rights or always-open management ports. Without least-privilege RBAC and time-based access controls, a single compromised credential or unpatched management port can give attackers persistent access to critical resources. By enforcing granular RBAC and implementing Just-In-Time (JIT) VM access, organizations reduce both the attack surface and the opportunity for privilege escalation, aligning with Zero Trust and modern compliance requirements.

---

## What I Built

- Provisioned an isolated resource group and a secure Azure virtual machine.
- Created an Azure AD test user and applied the Virtual Machine Contributor role using RBAC, enforcing least-privilege access.
- Enabled Microsoft Defender for Servers, preparing the environment for advanced security controls like Just-In-Time (JIT) VM access.
- Documented (and, if available, demonstrated) the process of restricting VM management port access to time-limited, on-demand windows via JIT, drastically reducing potential exposure to attacks.
- Captured every technical step with screenshots and a clear architecture diagram to provide technical and non-technical audiences full visibility into the security controls applied.

---

## Diagram

![Architecture Diagram](diagram.png)

---

## Objectives

- Deploy and organize Azure resources securely within a resource group.
- Assign RBAC roles for granular, least-privilege VM access.
- Verify that limited permissions are enforced in practice.
- Clean up all lab resources to avoid charges and demonstrate responsible lifecycle management.

---

## Steps Performed

1. Resource and VM Creation
   - Created resource group: SecLab2-RG in East US.
   - Deployed a Windows Server 2022 VM: SecLab2-VM (size: B1s).
   - Verified creation and resource organization.

2. RBAC Role Assignment
   - Created Azure AD test user: labtestuser@azurelabstest.onmicrosoft.com.
   - Assigned the “Virtual Machine Contributor” role to the test user at the resource group scope using Access Control (IAM).
   - Confirmed the user’s role assignment via the portal.

3. Permission Verification
   - Confirmed the test user could only start/stop/restart the VM and could not delete the resource group or manage roles.
   -Verified effective permissions using the Access Control (IAM) “Role assignments” and “Check access” features.
   - (Direct login as test user not possible due to Azure subscription limits; permissions documented via admin screenshots.)

4. Defender for Servers / JIT Access
   - Enabled Microsoft Defender for Servers on the subscription to allow JIT features (*Note: Just-In-Time VM Access could not be enabled in this environment due to Azure portal limitations for this subscription. In a standard enterprise subscription, the process would continue by enabling JIT on the VM via Defender for Cloud, as documented here.)
   - Demonstrated understanding and documented steps for JIT access control, including screenshot of Defender for Servers activation.
  
5. Cleanup
   - Deleted the resource group (SecLab2-RG), ensuring all associated resources (VM, disks, NIC, NSG, public IP) were also removed to prevent ongoing charges.
   - Disabled Defender for Servers in the subscription after the lab to avoid future costs from advanced security features.
   - Verified removal in the Azure Portal to confirm there are no remaining active resources or security plans from the lab.

---

## Screenshots

*All screenshots are included in the screenshots/ folder.

| Step | Filename                                                  | Description                                                    |
| ---- | --------------------------------------------------------- | -------------------------------------------------------------- |
| 1    | ResourceGroup-Create-SecLab2-RG.png                       | Resource group `SecLab2-RG` creation/overview                  |
| 2    | VM-Overview-SecLab2-VM.png                                | Virtual machine `SecLab2-VM` overview (name, state, public IP) |
| 3    | RBAC-AddRoleAssignment-VirtualMachineContributor.png      | “Add role assignment” form for Virtual Machine Contributor     |
| 4    | RBAC-RoleAssignments-VM-or-RG.png                         | Role assignments tab showing assigned users/roles              |
| 5    | RBAC-LabTestUser-VirtualMachineContributor-SecLab2-RG.png | Specific RBAC assignment for Lab Test User on RG               |
| 6    | DefenderForServers-Enabled-AfterSave.png                  | Defender for Servers plan enabled in subscription              |

## Screenshot Explanations

1. ResourceGroup-Create-SecLab2-RG.png: Shows the Azure resource group created for the lab and its contents.

2. VM-Overview-SecLab2-VM.png: Displays the details and status of the virtual machine, confirming deployment.

3. RBAC-AddRoleAssignment-VirtualMachineContributor.png: Captures the process of assigning the Virtual Machine Contributor role via IAM.

4. RBAC-RoleAssignments-VM-or-RG.png: Proves which users/roles are assigned at the VM or resource group scope.

5. RBAC-LabTestUser-VirtualMachineContributor-SecLab2-RG.png: Confirms the test user is assigned least-privilege access (VM Contributor role) at the resource group level.

6. DefenderForServers-Enabled-AfterSave.png: Documents that Defender for Servers was enabled to support advanced security controls (like JIT).

---

## Lessons Learned

- RBAC in Azure allows precise, least-privilege access assignment—essential for security and compliance.
- Real-world cloud security involves not only granting but also proving permissions are minimal.
- JIT access further limits the attack surface by reducing standing administrative privilege, though not always available in every subscription.
- Responsible lifecycle management (including cleanup and cost control) is crucial for effective cloud security operations.
- Documenting limitations and linking to official guidance is a valuable, professional practice.

---

## References

- Azure role-based access control (RBAC)
(https://learn.microsoft.com/en-us/azure/role-based-access-control/overview)

- Just-In-Time VM Access in Defender for Cloud
(https://learn.microsoft.com/en-us/azure/defender-for-cloud/just-in-time-access-usage)

- Microsoft Defender for Servers
(https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-defender-for-servers)

- Resource groups in Azure
(https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)

- Zero Trust Guidance: Zero Trust Security Principles
(https://www.microsoft.com/en-us/security/business/zero-trust)

---

Sebastian Silva C. – July, 2025 – Berlin, Germany.
