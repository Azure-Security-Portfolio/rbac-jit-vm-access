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
  - [1. Resource Group Creation]
  - [2. Virtual Machine Deployment]
  - [3. RBAC Role Assignment]
  - [4. RBAC Assignment Verification]
  - [5. Enable Defender for Servers]
  - [6. Cleanup]
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

1. Resource Group Creation
   - Created the resource group SecLab2-RG for isolation and simple cleanup (Screenshot: ResourceGroup-Create-SecLab2-RG.png)

2. Virtual Machine Deployment
   - Deployed Windows Server 2022 VM SecLab2-VM (B1s size) in the new resource group.
   - Verified VM status and public IP assignment (Screenshot: VM-Overview-SecLab2-VM.png)

3. RBAC Role Assignment
   - Opened Access control (IAM) and started a new role assignment.
   - Assigned the Virtual Machine Contributor role to test user at the resource group scope (Screenshot: RBAC-AddRoleAssignment-VirtualMachineContributor.png)

4. RBAC Assignment Verification
   - Confirmed via the Role Assignments tab that the test user had the correct least-privilege role (Screenshot: RBAC-RoleAssignments-VM-or-RG.png)
   - Additionally verified the test user was scoped correctly on the resource group (Screenshot: RBAC-LabTestUser-VirtualMachineContributor-SecLab2-RG.png)

5. Enable Defender for Servers
   - Enabled the Microsoft Defender for Servers plan in the subscription as a prerequisite for advanced controls (such as JIT. Screenshot: DefenderForServers-Enabled-AfterSave.png)

6. Cleanup
   - Deleted the resource group SecLab2-RG, removing all lab resources (VM, disks, NIC, public IP, NSG) to prevent ongoing costs.
   - Disabled Defender for Servers in the subscription after the lab.

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
