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
