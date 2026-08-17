# Microsoft Entra ID Deep Dive Homelab

![Microsoft Entra ID](https://img.shields.io/badge/Microsoft%20Entra%20ID-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Conditional Access](https://img.shields.io/badge/Conditional%20Access-0d47a1?style=for-the-badge&logo=microsoft&logoColor=white)
![PIM](https://img.shields.io/badge/PIM-4a148c?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Identity Protection](https://img.shields.io/badge/Identity%20Protection-b71c1c?style=for-the-badge&logo=microsoft&logoColor=white)
![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=for-the-badge&logo=powershell&logoColor=white)

A comprehensive Microsoft Entra ID deep dive homelab built hands-on on a live Microsoft 365 Business Premium tenant with Entra ID P2 trial. Every user, every policy, every security configuration done from scratch across 14 chapters covering Identity and Access Management, Privileged Identity Management, Identity Protection, Enterprise Applications, Hybrid Identity and Governance.

---

## Table of Contents

- [Tenant Details](#tenant-details)
- [What Was Built](#what-was-built)
- [Screenshots](#screenshots)
  - [B - Users](#b---users)
  - [C - Groups](#c---groups)
  - [D - Authentication Methods](#d---authentication-methods)
  - [E - Conditional Access](#e---conditional-access)
  - [F - SSPR](#f---sspr)
  - [G - PIM](#g---pim)
  - [H - Identity Protection](#h---identity-protection)
  - [I - Enterprise Applications](#i---enterprise-applications)
  - [J - App Registrations](#j---app-registrations)
  - [K - B2B External Collaboration](#k---b2b-external-collaboration)
  - [L - Entra Connect](#l---entra-connect)
  - [M - Access Reviews](#m---access-reviews)
  - [N - Monitoring](#n---monitoring)
- [Skills Demonstrated](#skills-demonstrated)
- [Tools and Technologies](#tools-and-technologies)
- [Repository Structure](#repository-structure)
- [About](#about)

---

## Tenant Details

| Component | Details |
|-----------|---------|
| Plan | Microsoft 365 Business Premium + Entra ID P2 Trial |
| Tenant | praveenlab2026.onmicrosoft.com |
| Users | 22 users across IT, Finance, HR, Sales, Marketing, Mumbai and Delhi sites |
| Admin Account | Praveenkumar.Saminathan@praveenlab2026.onmicrosoft.com |
| Entra ID P1 | Included in Business Premium - Conditional Access, Dynamic Groups, SSPR |
| Entra ID P2 | 30-day free trial - PIM, Identity Protection, Access Reviews |
| On-premises AD | labshandson.lan - Windows Server 2025 Domain Controller |
| Hardware | Dell Latitude i5, 16GB RAM, VMware Workstation |

---

## What Was Built

### Identity and Access Management
- Created and managed 22 users across multiple departments with full Joiner-Mover-Leaver lifecycle
- Blocked sign-in and revoked active sessions for leaver scenario
- Created Microsoft 365 Groups, Security Groups, Distribution Lists and Dynamic Groups with P1
- Dynamic Group with advanced membership rules using AND/OR conditions
- Group expiration policy configured with 365-day lifetime and email notifications to owners
- Group-based licensing - Business Premium assigned to security group for automatic license assignment
- Per-user MFA verified as Disabled - Conditional Access handles MFA enforcement

### Authentication Methods
- Microsoft Authenticator enabled for all users with number matching to prevent MFA fatigue attacks
- SMS disabled following security best practice
- Temporary Access Pass (TAP) configured and generated for Alice Johnson - one-time use, 60 minute lifetime
- Registration campaign enabled nudging users to register Authenticator app
- User registration details report showing MFA and SSPR capability per user

### Conditional Access - 9 Policies Configured
- CA001 - Require MFA for all users with Emergency Admin exclusion
- CA002 - Block access from outside Italy using Named Locations
- CA003 - Require MFA for all admin roles
- CA004 - Block legacy authentication (IMAP, POP3, SMTP Auth)
- CA005 - Require compliant device for Exchange Online (Report-only)
- CA006 - Admin sign-in frequency 1 hour with never persistent browser session (Report-only)
- CA007 - Sign-in risk Medium and above requires MFA (Report-only, P2)
- CA008 - User risk High requires password change (Report-only, P2)
- Microsoft-managed baseline policies also active

### Self-Service Password Reset (SSPR)
- SSPR enabled for all users with two methods required to reset
- Registration required on next sign-in, re-confirmation every 180 days
- Email notifications configured for users and admins
- Full SSPR flow tested via aka.ms/sspr

### Privileged Identity Management (PIM) - Entra ID P2
- Global Administrator active assignments discovered
- Alice Johnson made eligible for Exchange Administrator with time-bound assignment
- Global Administrator role settings hardened - 4 hour max, MFA required, justification required, approval required
- Full approval workflow tested - Alice requested Exchange Admin, admin approved
- PIM audit history showing all activations and assignments

### Identity Protection - Entra ID P2
- Real risk detection generated using Tor Browser - Anonymous IP address detected for Alice Johnson
- Alice Johnson flagged as High risk from Stockholm Tor exit node
- Risk-based Conditional Access policies CA007 and CA008 created
- Risk level chart showing High risk detection

### Enterprise Applications and SSO
- GitHub Enterprise Cloud added from gallery with SAML SSO configured
- SAML certificate generated, user and group assignment configured
- Usage and insights report showing 100% sign-in success rate

### App Registrations and Microsoft Graph API
- PraveenLab PowerShell App registered with client secret
- API permissions configured with admin consent - User.ReadWrite.All, Group.ReadWrite.All, Directory.ReadWrite.All
- Application authenticated to Microsoft Graph using OAuth 2.0 client credentials flow
- All 22 tenant users listed via PowerShell connected as application

### Hybrid Identity - Entra Connect
- UPN suffix praveenlab2026.onmicrosoft.com added to on-premises AD
- All 9 Delhi-HQ users updated via PowerShell - Ahmed Khan, Sofia Romano, James Smith, Priya Sharma, Raj Patel, Emma Wilson, Praveen Kumar, Maria Rossi, Luca Bianchi

### Access Reviews
- IT-Staff-Security access review created with monthly recurrence
- Full review workflow completed - approve and deny decisions for 5 members
- Access review notification email received by reviewer
- Quarterly Global Administrator Review created via PIM

### Monitoring
- Sign-in logs reviewed with full event detail showing MFA and CA evaluation
- Audit logs showing Access Reviews approve decisions
- Usage and insights workbook showing app activity
- Diagnostic settings configured for log export to Log Analytics

---

## Screenshots

### B - Users

| | |
|---|---|
| ![B01](screenshots/B-Users/B01-all-users-list.png) | ![B02](screenshots/B-Users/B02-user-properties.png) |
| B01 - All users list showing 22 users with source and type columns | B02 - Chris Green user properties showing Object ID and UPN |
| ![B03](screenshots/B-Users/B03-user-account-tab.png) | ![B04](screenshots/B-Users/B04-bulk-operations.png) |
| B03 - User properties tab showing department, job title and contact info | B04 - Bulk operations menu showing bulk create, invite and delete options |
| ![B05](screenshots/B-Users/B05-per-user-mfa.png) | ![B06](screenshots/B-Users/B06-user-blocked.png) |
| B05 - Per-user MFA showing all users Disabled - Conditional Access handles MFA | B06 - Bob Smith with sign-in blocked demonstrating leaver process |
| ![B07](screenshots/B-Users/B07-deleted-users.png) | ![B08](screenshots/B-Users/B08-revoke-sessions.png) |
| B07 - Deleted users page showing accounts pending 30-day deletion | B08 - Successfully revoked sign-in sessions for Francis Robinson |

---

### C - Groups

| | |
|---|---|
| ![C01](screenshots/C-Groups/C01-all-groups-list.png) | ![C02](screenshots/C-Groups/C02-dynamic-group-rule.png) |
| C01 - All groups showing 9 groups including M365, Security and Distribution types | C02 - Dynamic-IT-Department group with membership rule |
| ![C03](screenshots/C-Groups/C03-group-expiration-policy.png) | ![C04](screenshots/C-Groups/C04-group-based-licensing.png) |
| C03 - Group expiration policy set to 365 days | C04 - Group properties showing M365 group type |
| ![C05](screenshots/C-Groups/C05-group-owners.png) | |
| C05 - Finance Team owners tab showing Alice Johnson as group owner | |

---

### D - Authentication Methods

| | |
|---|---|
| ![D01](screenshots/D-Auth-Methods/D01-auth-methods-list.png) | ![D02](screenshots/D-Auth-Methods/D02-authenticator-enabled.png) |
| D01 - Authentication methods showing Authenticator and TAP enabled, SMS disabled | D02 - Microsoft Authenticator settings Enabled for all users |
| ![D03](screenshots/D-Auth-Methods/D03-sms-disabled.png) | ![D04](screenshots/D-Auth-Methods/D04-tap-enabled.png) |
| D03 - SMS method disabled - phishing-resistant methods prioritised | D04 - Temporary Access Pass settings Enabled for all users |
| ![D05](screenshots/D-Auth-Methods/D05-tap-generated.png) | ![D06](screenshots/D-Auth-Methods/D06-registration-campaign.png) |
| D05 - TAP generated for Alice Johnson - one-time use, 60 minute validity | D06 - Registration campaign Enabled nudging users to register Authenticator |
| ![D07](screenshots/D-Auth-Methods/D07-user-registration-details.png) | |
| D07 - User registration details report showing MFA and SSPR capability per user | |

---

### E - Conditional Access

| | |
|---|---|
| ![E01](screenshots/E-Conditional-Access/E01-ca-policies-list.png) | ![E02](screenshots/E-Conditional-Access/E02-ca005-compliant-device.png) |
| E01 - All 10 CA policies showing CA001-CA006 and Microsoft-managed policies | E02 - CA005 Require Compliant Device for Exchange Online Report-only |
| ![E03](screenshots/E-Conditional-Access/E03-ca006-signin-frequency.png) | ![E04](screenshots/E-Conditional-Access/E04-signin-log-ca-evaluation.png) |
| E03 - CA006 Admin Sign-in Frequency 1 Hour Report-only | E04 - Sign-in log showing all 9 CA policies evaluated |

---

### F - SSPR

| | |
|---|---|
| ![F01](screenshots/F-SSPR/F01-sspr-properties.png) | ![F02](screenshots/F-SSPR/F02-sspr-auth-methods.png) |
| F01 - SSPR Properties enabled for all users | F02 - SSPR Authentication methods with 2 methods required |
| ![F03](screenshots/F-SSPR/F03-sspr-registration.png) | ![F04](screenshots/F-SSPR/F04-sspr-notifications.png) |
| F03 - SSPR Registration required on sign-in, re-confirm every 180 days | F04 - SSPR Notifications enabled for users and admins |
| ![F05](screenshots/F-SSPR/F05-sspr-user-experience.png) | |
| F05 - SSPR user experience at aka.ms/sspr showing verification method selection | |

---

### G - PIM

| | |
|---|---|
| ![G01](screenshots/G-PIM/G01-pim-ga-active-assignments.png) | ![G02](screenshots/G-PIM/G02-approve-requests.png) |
| G01 - Global Administrator active assignments showing main admin and Emergency Admin | G02 - PIM Approve requests showing Alice Johnson Exchange Admin activation pending |
| ![G03](screenshots/G-PIM/G03-Approving-request.png) | ![G04](screenshots/G-PIM/G04-Approved-assignment-request.png) |
| G03 - Approving Alice Johnson Exchange Admin request with business justification | G04 - Alice Johnson My roles showing Exchange Administrator Activated |
| ![G05](screenshots/G-PIM/G05-pim-eligible-assignment-bob.png) | ![G06](screenshots/G-PIM/G06-pim-role-settings-ga.png) |
| G05 - Exchange Administrator eligible assignments showing Alice Johnson | G06 - Global Administrator settings - 4 hour max, MFA required, approval required |
| ![G07](screenshots/G-PIM/G07-pim-my-roles.png) | ![G08](screenshots/G-PIM/G08-pim-audit-history.png) |
| G07 - My roles showing Security Administrator eligible assignment | G08 - PIM audit history showing all activations and assignments |

---

### H - Identity Protection

| | |
|---|---|
| ![H01](screenshots/H-Identity-Protection/H01-ID-Protection-Dashboard.png) | ![H02](screenshots/H-Identity-Protection/H02-risky-signin-alice.png) |
| H01 - Identity Protection dashboard with P2 activated | H02 - Alice Johnson blocked sign-in from Tor browser via CA002 |
| ![H03](screenshots/H-Identity-Protection/H03-risk-detection-anonymous-ip.png) | ![H04](screenshots/H-Identity-Protection/H04-risk-detection-signin-events-alice.png) |
| H03 - Anonymous IP address High risk detection - Stockholm Tor exit node | H04 - Alice Johnson sign-in events showing Tor failures and normal sign-ins |
| ![H05](screenshots/H-Identity-Protection/H05-risky-signin.png) | ![H06](screenshots/H-Identity-Protection/H06-risky-user.png) |
| H05 - Risky sign-in detail showing IP address and risk detections | H06 - Alice Johnson High risk user with Anonymous IP risk event |
| ![H07](screenshots/H-Identity-Protection/H07-signin-risk-level-medium-high.png) | ![H08](screenshots/H-Identity-Protection/H08-user-risk-password-change.png) |
| H07 - CA007 Sign-in Risk Medium and High requires MFA | H08 - CA008 User Risk High requires password change Report-only |
| ![H09](screenshots/H-Identity-Protection/H09-risk-level-chart.png) | |
| H09 - Risk level chart showing 1 High risk user at 4.55% | |

---

### I - Enterprise Applications

| | |
|---|---|
| ![I01](screenshots/I-Enterprise-Apps/I01-saml-configuration.png) | ![I02](screenshots/I-Enterprise-Apps/I02-permissions-user-read.png) |
| I01 - GitHub Enterprise Cloud SAML configuration with Identifier and Reply URL | I02 - Enterprise app permissions showing User.Read delegated permission |
| ![I03](screenshots/I-Enterprise-Apps/I03-usage-insights-enterprise-applications.png) | ![I04](screenshots/I-Enterprise-Apps/I04-enterprise-apps-list.png) |
| I03 - Usage and insights showing 100% sign-in success rate | I04 - Enterprise applications list showing GitHub apps and Microsoft Graph |
| ![I05](screenshots/I-Enterprise-Apps/I05-user-assignment.png) | ![I06](screenshots/I-Enterprise-Apps/I06-singlesignon-SAML-certificates.png) |
| I05 - Users and groups showing IT-Staff-Security and admin assigned to GitHub | I06 - SAML certificate with Active status and 2029 expiry |

---

### J - App Registrations

| | |
|---|---|
| ![J01](screenshots/J-App-Registrations/J01-app-registrations-list.png) | ![J02](screenshots/J-App-Registrations/J02-app-overview.png) |
| J01 - App registrations list showing PraveenLab PowerShell App | J02 - App overview showing Client ID, Tenant ID and Object ID |
| ![J03](screenshots/J-App-Registrations/J03-certificates-secrets.png) | ![J04](screenshots/J-App-Registrations/J04-api-permissions.png) |
| J03 - Certificates and secrets showing client secret with expiry | J04 - API permissions with admin consent granted for all permissions |
| ![J05](screenshots/J-App-Registrations/J05-app-registration-powershell.png) | |
| J05 - PowerShell connected as application via OAuth 2.0 listing all 22 users | |

---

### K - B2B External Collaboration

| | |
|---|---|
| ![K01](screenshots/K-B2B/K01-guest-user-invited.png) | ![K02](screenshots/K-B2B/K02-external-collaboration-settings.png) |
| K01 - All users showing External Test User with Guest type | K02 - External collaboration settings showing member users can invite guests |
| ![K03](screenshots/K-B2B/K03-collaboration-restrictions.png) | ![K04](screenshots/K-B2B/K04-access-review-created.png) |
| K03 - Collaboration restrictions set to allow invitations to any domain | K04 - Quarterly Global Administrator Review created via access reviews |

---

### L - Entra Connect

| | |
|---|---|
| ![L01](screenshots/L-Entra-Connect/L01-upn-suffix-added.png) | ![L02](screenshots/L-Entra-Connect/L02-upn-updated-powershell.png) |
| L01 - UPN suffix praveenlab2026.onmicrosoft.com added in AD Domains and Trusts | L02 - PowerShell updating all 9 Delhi-HQ users to new UPN suffix |

---

### M - Access Reviews

| | |
|---|---|
| ![M01](screenshots/M-Access-Reviews/M01-ITSecurity-access-review-overview.png) | ![M02](screenshots/M-Access-Reviews/M02-Identity-governance-access-review-dashboard.png) |
| M01 - IT Security access reviews overview showing 5 members under review | M02 - Identity Governance dashboard showing access reviews configured |
| ![M03](screenshots/M-Access-Reviews/M03-access-review-approval-status.png) | ![M04](screenshots/M-Access-Reviews/M04-access-review-members-approve-deny.png) |
| M03 - Access review approval status showing IT-Staff-Security review in progress | M04 - Access review members showing approve and deny decisions |
| ![M05](screenshots/M-Access-Reviews/M05-access-review-reviewed-approved.png) | ![M06](screenshots/M-Access-Reviews/M06-access-review-notification-mail.png) |
| M05 - Completed access review showing approved and denied decisions per member | M06 - Access review notification email received in Outlook |

---

### N - Monitoring

| | |
|---|---|
| ![N01](screenshots/N-Monitoring/N01-Monitoring%20and%20health-sign%20in%20logs.png) | ![N02](screenshots/N-Monitoring/N02-sign%20in%20logs-details.png) |
| N01 - Sign-in logs showing interactive sign-in events with IP and status | N02 - Sign-in log detail showing MFA requirement satisfied by claim |
| ![N03](screenshots/N-Monitoring/N03-monitoring%20and%20health-audit%20logs.png) | ![N04](screenshots/N-Monitoring/N04-audit%20logs-details.png) |
| N03 - Audit logs showing Access Reviews approve decisions with success status | N04 - Audit log detail showing approve decision with correlation ID |
| ![N05](screenshots/N-Monitoring/N05-workbook-usage%20and%20insights.png) | ![N06](screenshots/N-Monitoring/N06-diagonistic%20setting-dashboard.png) |
| N05 - Usage and insights showing app sign-in activity and success rates | N06 - Diagnostic settings configured for export to Log Analytics |

---

## Skills Demonstrated

| Role | Skills Covered in This Lab |
|------|---------------------------|
| IAM Engineer | Conditional Access 9 policies, MFA methods, SSPR, Dynamic Groups, PIM, Identity Protection |
| Identity Administrator | User lifecycle, group governance, access reviews, hybrid identity, B2B collaboration |
| Security Engineer | Risk-based CA, Identity Protection, Tor-based risk detection, PIM just-in-time access |
| Cloud Administrator | App registrations, enterprise apps, SAML SSO, Microsoft Graph API client credentials |
| IT Support Engineer | TAP generation, SSPR config, sign-in log investigation, audit log review |

---

## Tools and Technologies

| Category | Tools |
|----------|-------|
| Identity | Microsoft Entra ID P1 and P2, Conditional Access, MFA, SSPR, TAP, PIM, Identity Protection |
| Governance | Access Reviews, Group Expiration, Group-based Licensing |
| Applications | Enterprise Applications, SAML SSO, App Registrations, Microsoft Graph API |
| Hybrid Identity | Entra Connect, UPN Suffix, On-premises AD preparation |
| External Collaboration | B2B Guest Users, External Identities, Guest Access Reviews |
| Automation | PowerShell, Microsoft Graph SDK, OAuth 2.0 client credentials flow |
| Monitoring | Sign-in Logs, Audit Logs, Workbooks, Diagnostic Settings |
| Admin Portals | entra.microsoft.com, admin.microsoft.com, security.microsoft.com |

---

## Repository Structure

```
Microsoft-Entra-ID-Homelab/
├── README.md
├── LICENSE
├── requirements.txt
└── screenshots/
    ├── B-Users/
    ├── C-Groups/
    ├── D-Auth-Methods/
    ├── E-Conditional-Access/
    ├── F-SSPR/
    ├── G-PIM/
    ├── H-Identity-Protection/
    ├── I-Enterprise-Apps/
    ├── J-App-Registrations/
    ├── K-B2B/
    ├── L-Entra-Connect/
    ├── M-Access-Reviews/
    └── N-Monitoring/
```

---

## About

Built by **Praveenkumar Saminathan**

MSc Geoinformatics Engineering - Politecnico di Milano, Milan, Italy (Graduated July 2026)

Almost 4 years IT support experience including Tata Consultancy Services and freelance IT support in Milan.

**Certifications:** AWS Cloud Practitioner | AZ-900 (Microsoft Azure Fundamentals) | SC-900 (Microsoft Security, Compliance and Identity Fundamentals)

**Target Roles:** IAM Engineer | Identity Administrator | Cloud Security Engineer | IT Support | IT Infrastructure

- Portfolio: [praveenkumar-saminathan](https://orange3456.github.io/praveenkumar-saminathan.github.io/)
- LinkedIn: [praveenkumar-saminathan-993902228](https://www.linkedin.com/in/praveenkumar-saminathan-993902228)
- GitHub: [Orange3456](https://github.com/Orange3456)

---

> This lab was built entirely hands-on on a live Microsoft 365 Business Premium tenant with Entra ID P2 trial. Every policy configured from scratch, every command typed, every error troubleshot. The Tor Browser was used to generate a real Anonymous IP risk detection in Identity Protection demonstrating actual security event handling.
