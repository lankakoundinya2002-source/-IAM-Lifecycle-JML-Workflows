# 👤 IAM Lifecycle & JML Workflows

> **Portfolio Project** — Identity & Access Management Documentation
> Sai Koundinya Lanka | SC-300 Aspirant

[![Domain](https://img.shields.io/badge/Domain-Identity%20Lifecycle%20Management-blue)]()
[![Platform](https://img.shields.io/badge/Platform-Microsoft%20Entra%20ID%20%7C%20ServiceNow-0078D4)]()
[![Process](https://img.shields.io/badge/Process-Joiner%20%7C%20Mover%20%7C%20Leaver-green)]()
[![Status](https://img.shields.io/badge/Status-Active-brightgreen)]()

---

## 📌 Project Overview

The **IAM Lifecycle & JML Workflows** project is a comprehensive documentation and process design portfolio covering the complete **Identity Lifecycle Management** cycle — from the moment a user joins an organization to when they leave.

JML stands for **Joiner → Mover → Leaver** — the three critical phases every user identity passes through. This project documents the policies, workflows, ITSM ticketing procedures, and access governance controls that ensure the right people have the right access at the right time — and no longer.

This directly reflects day-to-day responsibilities in enterprise IAM teams, access management operations centers, and security support roles.

---

## 🎯 Why JML Matters

| Risk Without JML | Control With JML |
|-----------------|-----------------|
| Orphaned accounts with active access | Automated deprovisioning on exit |
| Over-privileged users after role change | Access review triggered on every move |
| Delayed onboarding, productivity loss | Standardized provisioning within SLA |
| Audit failures due to untracked access | Full audit trail for every lifecycle event |
| Compliance violations (DPDP, GDPR) | Policy-enforced lifecycle controls |

---

## 🏗️ JML Lifecycle Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    IDENTITY LIFECYCLE OVERVIEW                      │
└─────────────────────────────────────────────────────────────────────┘

        HR SYSTEM / BUSINESS TRIGGER
                    │
        ┌───────────┼────────────┐
        │           │            │
        ▼           ▼            ▼
  ┌──────────┐ ┌─────────┐ ┌──────────┐
  │  JOINER  │ │  MOVER  │ │  LEAVER  │
  │  (New    │ │ (Role / │ │  (Exit / │
  │   Hire)  │ │ Transfer│ │  Offboard│
  └────┬─────┘ └────┬────┘ └────┬─────┘
       │            │            │
       ▼            ▼            ▼
  Provision     Review &     Revoke &
  Identity      Update       Disable
  & Access      Access       Account
       │            │            │
       ▼            ▼            ▼
  Assign         Modify       Remove
  Licenses,      Group        Licenses,
  Groups,        Memberships  Sessions,
  Roles          & Roles      Access
       │            │            │
       ▼            ▼            ▼
  Notify         Notify       Archive
  User &         Manager      Account
  Manager        & User       (30 days)
       │            │            │
       └────────────┴────────────┘
                    │
                    ▼
           ServiceNow Ticket
           Closed & Audit Log
               Updated
```

---

## 📁 Repository Structure

```
iam-lifecycle-jml-workflows/
│
├── README.md                              # Project overview (this file)
│
├── docs/
│   ├── 01-jml-overview.md                # JML framework introduction
│   ├── 02-joiner-workflow.md             # Full Joiner (onboarding) process
│   ├── 03-mover-workflow.md              # Full Mover (role change) process
│   ├── 04-leaver-workflow.md             # Full Leaver (offboarding) process
│   ├── 05-access-request-management.md   # Access request & approval workflows
│   ├── 06-access-review-process.md       # Periodic access review procedures
│   ├── 07-servicenow-ticketing.md        # ITSM ticket templates & workflows
│   └── 08-compliance-and-audit.md        # Audit trail & compliance requirements
│
├── workflows/
│   ├── joiner/
│   │   ├── joiner-checklist.md           # Step-by-step onboarding checklist
│   │   ├── day-1-access-package.md       # Standard Day 1 access definitions
│   │   └── provisioning-sla.md           # SLA targets for provisioning
│   │
│   ├── mover/
│   │   ├── mover-checklist.md            # Role change access update checklist
│   │   ├── access-review-trigger.md      # When and how to trigger access review
│   │   └── role-change-matrix.md         # Access changes per role transition
│   │
│   └── leaver/
│       ├── leaver-checklist.md           # Offboarding checklist (Day 0 to Day 30)
│       ├── immediate-actions.md          # Actions on last working day
│       └── account-archival-policy.md    # Account retention & deletion policy
│
├── servicenow/
│   ├── ticket-templates/
│   │   ├── joiner-request-template.md    # ServiceNow Joiner ticket template
│   │   ├── mover-request-template.md     # ServiceNow Mover ticket template
│   │   ├── leaver-request-template.md    # ServiceNow Leaver ticket template
│   │   └── access-request-template.md    # General access request template
│   │
│   └── sla-definitions.md               # SLA tiers for IAM ticket categories
│
├── diagrams/
│   ├── jml-lifecycle-overview.png        # Full JML lifecycle diagram
│   ├── joiner-workflow-detail.png        # Detailed Joiner process flow
│   ├── mover-workflow-detail.png         # Detailed Mover process flow
│   ├── leaver-workflow-detail.png        # Detailed Leaver process flow
│   └── access-request-flow.png          # Access request approval workflow
│
├── policies/
│   ├── identity-lifecycle-policy.md     # Organizational IAM lifecycle policy
│   ├── access-review-policy.md          # Periodic access review policy
│   ├── privileged-access-policy.md      # Policy for privileged account lifecycle
│   └── orphaned-account-policy.md       # Detection & remediation of orphaned accounts
│
└── reports/
    ├── access-review-report-template.md  # Template for access review outcomes
    └── lifecycle-audit-log-sample.md     # Sample audit log for lifecycle events
```

---

## 🔄 Workflow Details

### 🟢 JOINER — New Employee Onboarding

**Trigger:** HR system generates new hire record (start date - 3 days)

```
Step 1: HR submits Joiner request via ServiceNow
Step 2: IAM team creates Entra ID user account
Step 3: Assign licenses (M365, security tools)
Step 4: Add to standard groups based on department/role
Step 5: Assign RBAC roles per job profile
Step 6: Set up MFA registration (mandatory Day 1)
Step 7: Provision mailbox, Teams, SharePoint access
Step 8: Send welcome email with login credentials
Step 9: Close ServiceNow ticket & update audit log
```

**SLA Target:** Account ready 24 hours before start date

---

### 🟡 MOVER — Role Change / Transfer

**Trigger:** Manager submits change request via ServiceNow

```
Step 1: Manager raises Mover request in ServiceNow
Step 2: IAM team reviews current vs. new role access
Step 3: Remove access no longer required (old role)
Step 4: Add access required for new role
Step 5: Update group memberships & RBAC roles
Step 6: Trigger access review for sensitive permissions
Step 7: Update user's manager/department attributes
Step 8: Notify user and new manager
Step 9: Close ticket & update audit log
```

**SLA Target:** Access updated within 4 business hours of approval

---

### 🔴 LEAVER — Employee Offboarding

**Trigger:** HR submits termination notice (last working day)

```
IMMEDIATE (Last Working Day):
Step 1: Disable Entra ID account
Step 2: Revoke all active sessions & tokens
Step 3: Remove MFA methods
Step 4: Transfer mailbox/OneDrive ownership to manager
Step 5: Remove from all distribution groups
Step 6: Revoke VPN and application access

WITHIN 24 HOURS:
Step 7: Remove all role assignments & licenses
Step 8: Audit and export access log for records

WITHIN 30 DAYS:
Step 9: Archive mailbox
Step 10: Permanently delete account after retention period
Step 11: Close ServiceNow ticket & final audit log entry
```

**SLA Target:** Account disabled within 1 hour of last working day end

---

## 🎫 ServiceNow ITSM Integration

| Ticket Type | Category | Priority | SLA |
|-------------|----------|----------|-----|
| New Joiner Provisioning | Access Management | P2 | 24 hrs |
| Role Change (Mover) | Access Management | P2 | 4 hrs |
| Urgent Leaver (Termination) | Security | P1 | 1 hr |
| Planned Leaver | Access Management | P2 | EOD |
| Access Request | Access Management | P3 | 8 hrs |
| Access Review | Governance | P3 | 5 days |
| Orphaned Account | Security | P2 | 4 hrs |

---

## 🔗 Microsoft Entra ID Implementation

| JML Step | Entra ID Feature Used |
|----------|----------------------|
| Create user account | Entra ID User Management |
| Assign licenses | Microsoft 365 License Management |
| Group-based access | Dynamic Groups / Security Groups |
| Role assignment | RBAC / Privileged Identity Management (PIM) |
| MFA enrollment | Authentication Methods Policy |
| Session revocation | Revoke Sign-in Sessions |
| Access review | Identity Governance — Access Reviews |
| Audit trail | Entra ID Audit Logs |

---

## 📚 Compliance Alignment

| Regulation | JML Control |
|------------|-------------|
| DPDP Act (India) | Data minimization — remove access to personal data on exit |
| ISO 27001 | Access control lifecycle policy (A.9.2) |
| SOC 2 | Logical access provisioning and deprovisioning evidence |
| NIST 800-53 | AC-2: Account Management controls |

---

## 👤 Author

**Sai Koundinya Lanka**
IAM & Cloud Security Engineer | SC-300 Aspirant
📧 lankakoundinya2002@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/sai-koundinya-iam-engineer/)
📍 Hyderabad, Telangana, India

---

> *"Access should be granted on need-to-know, need-to-use — and revoked the moment that need ends."*
