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
