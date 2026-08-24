# Microsoft Entra ID IAM & Access Governance Lab

## Overview

This project demonstrates the redesign of a fictional organization's payroll access model using Microsoft Entra ID and Microsoft Entra Privileged Identity Management (PIM).

The original payroll process relied on a single employee to review and approve payroll. The employee's extended absence exposed a single point of failure and highlighted weaknesses in privileged access management, business continuity and access governance.

The redesigned model provides two authorized payroll approvers while reducing standing privilege and introducing independent governance controls. Privileged payroll access is managed through eligible group membership, time-limited activation, business justification and recurring access certification.

## Security Objectives

The solution was designed to:

- Eliminate the single point of failure in payroll approval
- Implement role-based access control (RBAC)
- Apply least privilege to payroll access
- Reduce standing privileged access through PIM
- Establish primary and backup payroll approvers
- Require justification for privileged access activation
- Introduce separation of duties between access users and reviewers
- Support business continuity during employee absence
- Periodically recertify privileged access through access reviews
- Maintain auditable evidence of access governance decisions

## Environment

- Microsoft Entra ID
- Microsoft Entra Privileged Identity Management (PIM)
- Microsoft Entra ID Governance
- Enterprise Applications
- Security Groups
- Access Reviews

## Architecture & Identity Design

The payroll access model separates standard application access, privileged payroll approval and governance responsibilities.

### Identity Roles

| Identity | Business Role | Access Responsibility |
|---|---|---|
| Bob Barker | Primary Payroll Approver | Eligible for privileged payroll approver access through PIM |
| Anita Adams | Backup Payroll Approver | Eligible for privileged payroll approver access through PIM |
| Casey Castigan | Payroll Manager | Reviews and certifies payroll approver access |
| Edna Edwards | Payroll User | Standard payroll application access |
| Duane Dumphrey | Standard User | No privileged payroll approval responsibility |

### Access Model

Two security groups were used to separate ordinary payroll access from privileged approval responsibilities:

- **SG-Payroll-Users** provides access to the TNWGroup Payroll System enterprise application.
- **SG-Payroll-Approvers** represents the privileged payroll approval function and is governed through Privileged Identity Management.

Bob Barker and Anita Adams are configured as **eligible**, rather than permanently active, members of SG-Payroll-Approvers. When payroll approval access is required, an eligible approver activates membership through PIM for a limited period and provides a business justification.

Casey Castigan serves as the independent reviewer for recurring access certification, separating the governance function from the employees receiving privileged access.

### Governance Flow

`Eligible Approver → PIM Activation → Time-Limited Group Membership → Payroll Approval Access → Expiration`

Recurring governance is applied separately:

`SG-Payroll-Approvers → Semi-Annual Access Review → Independent Reviewer → Approve or Deny Continued Eligibility`

## Implementation

### 1. Tenant Identity and Group Configuration

Five fictional user identities were created to represent the payroll and governance roles used throughout the lab.

Two security groups were then created to separate standard payroll application access from privileged payroll approval responsibilities:

- `SG-Payroll-Users` for standard payroll application access
- `SG-Payroll-Approvers` for privileged payroll approval access

This group-based design allows permissions to be assigned according to business function rather than directly to individual users, supporting RBAC and simplifying access administration.

### 2. Enterprise Application Access

The `TNWGroup Payroll System` enterprise application was configured to represent the organization's payroll application.

Standard payroll application access was assigned through `SG-Payroll-Users`, establishing a group-based access model rather than assigning the application directly to individual employees.

### 3. Privileged Payroll Access with PIM

`SG-Payroll-Approvers` was configured for Microsoft Entra Privileged Identity Management (PIM).

Bob Barker and Anita Adams were assigned as eligible members rather than maintaining permanent active membership. This reduces standing privileged access while preserving two authorized payroll approvers for business continuity.

PIM activation was configured to require business justification and provide access for a limited duration. An eligible approver can therefore obtain privileged payroll access when required without retaining that access continuously.

### 4. Privileged Access Activation

The PIM workflow was tested by activating eligible membership in `SG-Payroll-Approvers`.

The activation demonstrated the just-in-time access lifecycle:

`Eligible → Activation Request → Business Justification → Active Membership → Expiration`

This provides an auditable mechanism for granting privileged access only when there is a legitimate business need.

### 5. Recurring Access Certification

A semi-annual access review was created for `SG-Payroll-Approvers` to periodically verify that privileged payroll eligibility remains appropriate.

Casey Castigan, acting as Payroll Manager, was assigned as the independent reviewer. This separates privileged access usage from access certification responsibilities.

The review requires justification for access decisions and provides Microsoft Entra recommendations based on available identity activity. During testing, the reviewer evaluated both eligible payroll approvers and documented decisions regarding continued access.

This creates a recurring governance control around privileged access rather than relying solely on the original assignment decision.
