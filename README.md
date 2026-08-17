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
  - [Chapter 2 - Users](#chapter-2---users)
  - [Chapter 3 - Groups](#chapter-3---groups)
  - [Chapter 4 - Authentication Methods](#chapter-4---authentication-methods)
  - [Chapter 5 - Conditional Access](#chapter-5---conditional-access)
  - [Chapter 6 - SSPR](#chapter-6---sspr)
  - [Chapter 7 - PIM](#chapter-7---pim)
  - [Chapter 8 - Identity Protection](#chapter-8---identity-protection)
  - [Chapter 9 - Enterprise Applications](#chapter-9---enterprise-applications)
  - [Chapter 10 - App Registrations](#chapter-10---app-registrations)
  - [Chapter 11 - B2B External Collaboration](#chapter-11---b2b-external-collaboration)
  - [Chapter 12 - Entra Connect](#chapter-12---entra-connect)
  - [Chapter 13 - Access Reviews](#chapter-13---access-reviews)
  - [Chapter 14 - Monitoring](#chapter-14---monitoring)
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
| Admin Account | PRAVEENKUMARSAMINATHAN@praveenlab2026.onmicrosoft.com |
| Entra ID P1 | Included in Business Premium - Conditional Access, Dynamic Groups, SSPR |
| Entra ID P2 | 30-day trial - PIM, Identity Protection, Access Reviews |
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
- Group-based licensing - Business Premium assigned to IT-Staff-Security group for automatic license assignment
- Per-user MFA verified as Disabled across all users - Conditional Access handles MFA enforcement

### Authentication Methods
- Microsoft Authenticator enabled for all users with number matching to prevent MFA fatigue attacks
- SMS disabled following security best practice - phishing-resistant methods prioritised
- Temporary Access Pass (TAP) configured and generated for Alice Johnson - one-time use, 60 minute lifetime
- Registration campaign enabled nudging users to register Authenticator app
- User registration details report reviewed showing MFA and SSPR capability per user

### Conditional Access - 9 Policies Configured
- CA001 - Require MFA for all users with Emergency Admin exclusion
- CA002 - Block access from outside Italy using Named Locations
- CA003 - Require MFA for all admin roles
- CA004 - Block legacy authentication (IMAP, POP3, SMTP Auth)
- CA005 - Require compliant device for Exchange Online (Report-only)
- CA006 - Admin sign-in frequency 1 hour with never persistent browser session (Report-only)
- CA007 - Sign-in risk Medium and above requires MFA (Report-only, P2)
- CA008 - User risk High requires password change (Report-only, P2)
- Microsoft-managed policies: Block legacy auth, MFA for Azure management, MFA for admins, MFA for all users

### Self-Service Password Reset (SSPR)
- SSPR enabled for all users
- Two methods required to reset for security
- Registration required on next sign-in, re-confirmation every 180 days
- Email notifications configured - users notified on reset, admins notified on admin resets
- Full SSPR flow tested via aka.ms/sspr showing verification method selection

### Privileged Identity Management (PIM) - Entra ID P2
- Global Administrator active assignments discovered - main admin and Emergency Admin identified as permanent
- Alice Johnson made eligible for Exchange Administrator with 30-day time-bound assignment
- Security Administrator eligible assignment configured for lab admin account
- Global Administrator role settings hardened: 4-hour max activation, Azure MFA required, justification required, approval required
- Full approval workflow tested - Alice requested Exchange Admin activation with business justification, admin approved
- PIM audit history showing all activations, role setting updates and eligible assignments

### Identity Protection - Entra ID P2
- Identity Protection dashboard configured with P2 trial
- Real risk detection generated using Tor Browser - Anonymous IP address detected for Alice Johnson
- Alice Johnson flagged as High risk user from Stockholm Tor exit node sign-in attempt
- Risky sign-in detail showing attack type: Access using proxy, detected offline
- Sign-in events for Alice showing CA002 block from outside Italy applied simultaneously
- CA007 and CA008 risk-based Conditional Access policies created replacing deprecated built-in risk policies
- Risk level chart showing High risk detection across tenant

### Enterprise Applications and SSO
- GitHub Enterprise Cloud added from Entra Gallery
- SAML-based SSO configured with Identifier, Reply URL and Sign on URL
- SAML certificate generated with 3-year expiry and federation metadata URL
- IT-Staff-Security group and admin account assigned to app with Assignment required enabled
- Usage and insights report showing app sign-in activity and success rates

### App Registrations and Microsoft Graph API
- PraveenLab PowerShell App registered in Entra ID
- Client secret created with 6-month expiry
- API permissions configured: User.ReadWrite.All, Group.ReadWrite.All, Directory.ReadWrite.All with admin consent granted
- Application authenticated to Microsoft Graph using client credentials (OAuth 2.0 app-only flow)
- All 22 tenant users listed via PowerShell connected as application without user sign-in

### B2B External Collaboration
- Guest user invited to tenant using personal Gmail account
- External collaboration settings configured: member users and specific admins can invite guests
- Collaboration restrictions: allow invitations to any domain
- Quarterly Guest User Review created for Finance Team targeting guest users only

### Hybrid Identity - Entra Connect
- Alternative UPN suffix praveenlab2026.onmicrosoft.com added to on-premises AD via Active Directory Domains and Trusts
- All 9 Delhi-HQ AD users updated to use @praveenlab2026.onmicrosoft.com UPN via PowerShell
- Users updated: Ahmed Khan, Sofia Romano, James Smith, Priya Sharma, Raj Patel, Emma Wilson, Praveen Kumar, Maria Rossi, Luca Bianchi

### Access Reviews
- IT-Staff-Security access review created via Identity Governance
- Access review dashboard showing review status and governance overview
- Multi-stage review configured with approval workflow
- Email notification received confirming review assignment to reviewer
- Review decisions completed showing approve/deny workflow

### Monitoring
- Sign-in logs reviewed with detailed entry showing Conditional Access evaluation results for all 9 policies
- Audit logs reviewed showing admin activities with full details
- Usage and insights workbook accessed
- Diagnostic settings dashboard reviewed for log export configuration

---

## Screenshots

### Chapter 2 - Users

| | |
|---|---|
| ![B01](screenshots/chapter%202/B01-all-users-list.png) | ![B02](screenshots/chapter%202/B02-user-properties.png) |
| B01 - All users list showing 22 users with source and type columns | B02 - Chris Green user properties showing Object ID, UPN, group memberships |
| ![B03](screenshots/chapter%202/B03-user-account-tab.png) | ![B04](screenshots/chapter%202/B04-bulk-operations.png) |
| B03 - User properties tab showing department, job title, contact information | B04 - Bulk operations menu showing bulk create, invite and delete options |
| ![B05](screenshots/chapter%202/B05-per-user-mfa.png) | ![B06](screenshots/chapter%202/B06-user-blocked.png) |
| B05 - Per-user MFA showing all users as Disabled - Conditional Access handles MFA | B06 - Bob Smith with sign-in blocked demonstrating leaver process |
| ![B07](screenshots/chapter%202/B07-deleted-users.png) | ![B08](screenshots/chapter%202/B08-revoke-sessions.png) |
| B07 - Deleted users page showing IT Help Desk and Praveenkumar Admin pending 30-day deletion | B08 - Successfully revoked sign-in sessions for Francis Robinson |

---

### Chapter 3 - Groups

| | |
|---|---|
| ![C01](screenshots/chapter%203/C01-all-groups-list.png) | ![C02](screenshots/chapter%203/C02-dynamic-group-rule.png) |
| C01 - All groups showing 9 groups including M365, Security and Distribution types | C02 - Dynamic-IT-Department group with membership rule (user.userType -eq Member) |
| ![C03](screenshots/chapter%203/C03-group-expiration-policy.png) | ![C04](screenshots/chapter%203/C04-group-based-licensing.png) |
| C03 - Group expiration policy set to 365 days with admin email for groups without owners | C04 - IT Department Hub group properties showing M365 group type and assigned membership |
| ![C05](screenshots/chapter%203/C05-group-owners.png) | |
| C05 - Finance Team owners tab showing Alice Johnson as group owner | |

---

### Chapter 4 - Authentication Methods

| | |
|---|---|
| ![D01](screenshots/chapter%204/D01-auth-methods-list.png) | ![D02](screenshots/chapter%204/D02-authenticator-enabled.png) |
| D01 - Authentication methods policies showing Authenticator and TAP enabled, SMS disabled | D02 - Microsoft Authenticator settings showing Enabled for all users with Any authentication mode |
| ![D03](screenshots/chapter%204/D03-sms-disabled.png) | ![D04](screenshots/chapter%204/D04-tap-enabled.png) |
| D03 - SMS method showing disabled - phishing-resistant methods prioritised | D04 - Temporary Access Pass settings showing Enabled for all users |
| ![D05](screenshots/chapter%204/D05-tap-generated.png) | ![D06](screenshots/chapter%204/D06-registration-campaign.png) |
| D05 - TAP generated for Alice Johnson showing one-time use, 60 minute validity | D06 - Registration campaign Enabled nudging users to register Microsoft Authenticator |
| ![D07](screenshots/chapter%204/D07-user-registration-details.png) | |
| D07 - User registration details report showing MFA and SSPR capability per user | |

---

### Chapter 5 - Conditional Access

| | |
|---|---|
| ![E01](screenshots/chapter%205/E01-ca-policies-list.png) | ![E02](screenshots/chapter%205/E02-ca005-compliant-device.png) |
| E01 - All 10 CA policies showing CA001-CA006 user policies plus Microsoft-managed policies | E02 - CA005 Require Compliant Device for Exchange Online in Report-only mode |
| ![E03](screenshots/chapter%205/E03-ca006-signin-frequency.png) | ![E04](screenshots/chapter%205/E04-signin-log-ca-evaluation.png) |
| E03 - CA006 Admin Sign-in Frequency 1 Hour with persistent browser session disabled | E04 - Sign-in log showing all 9 CA policies evaluated with Success and Not applied results |

---

### Chapter 6 - SSPR

| | |
|---|---|
| ![F01](screenshots/chapter%206/F01-sspr-properties.png) | ![F02](screenshots/chapter%206/F02-sspr-auth-methods.png) |
| F01 - SSPR Properties showing Selected - enabled for all users | F02 - SSPR Authentication methods showing security questions with 2 methods required to reset |
| ![F03](screenshots/chapter%206/F03-sspr-registration.png) | ![F04](screenshots/chapter%206/F04-sspr-notifications.png) |
| F03 - SSPR Registration requiring users to register on sign-in, re-confirm every 180 days | F04 - SSPR Notifications showing Yes for both user and admin notification settings |
| ![F05](screenshots/chapter%206/F05-sspr-user-experience.png) | |
| F05 - SSPR user experience at aka.ms/sspr showing verification method selection for Alice | |

---

### Chapter 7 - PIM

| | |
|---|---|
| ![G01](screenshots/chapter%207/G01-pim-ga-active-assignments.png) | ![G02](screenshots/chapter%207/G02-approve-requests.png) |
| G01 - Global Administrator active assignments showing main admin and Emergency Admin as permanent | G02 - PIM Approve requests page showing Alice Johnson Exchange Admin activation request pending |
| ![G03](screenshots/chapter%207/G03-Approving-request.png) | ![G04](screenshots/chapter%207/G04-Approved-assignment-request.png) |
| G03 - Approving Alice Johnson Exchange Admin request with business justification visible | G04 - Alice Johnson My roles showing Exchange Administrator Activated with 2-hour window |
| ![G05](screenshots/chapter%207/G05-pim-eligible-assignment-bob.png) | ![G06](screenshots/chapter%207/G06-pim-role-settings-ga.png) |
| G05 - Exchange Administrator eligible assignments showing Alice Johnson with direct membership | G06 - Global Administrator role settings showing 4 hour max, Azure MFA required, approval required |
| ![G07](screenshots/chapter%207/G07-pim-my-roles.png) | ![G08](screenshots/chapter%207/G08-pim-audit-history.png) |
| G07 - My roles showing Security Administrator eligible assignment expiring September 15 2026 | G08 - PIM audit history showing all activations, role setting updates and eligible assignments |

---

### Chapter 8 - Identity Protection

| | |
|---|---|
| ![H01](screenshots/chapter%208/H01-ID-Protection-Dashboard.png) | ![H02](screenshots/chapter%208/H02-risky-signin-alice.png) |
| H01 - Identity Protection dashboard with P2 activated showing risk policy sections | H02 - Alice Johnson blocked sign-in from Tor browser - CA002 block outside Italy applied |
| ![H03](screenshots/chapter%208/H03-risk-detection-anonymous-ip.png) | ![H04](screenshots/chapter%208/H04-risk-detection-signin-events-alice.png) |
| H03 - Anonymous IP address risk detection for Alice - High risk, real-time, Stockholm Tor exit node | H04 - Alice Johnson sign-in events showing Tor sign-in failures and normal sign-ins from Caronno |
| ![H05](screenshots/chapter%208/H05-risky-signin.png) | ![H06](screenshots/chapter%208/H06-risky-user.png) |
| H05 - Risky sign-in detail showing request ID, IP address from Stockholm and risk detections | H06 - Alice Johnson Risky User Details showing High risk level with Anonymous IP risk event |
| ![H07](screenshots/chapter%208/H07-signin-risk-level-medium-high.png) | ![H08](screenshots/chapter%208/H08-user-risk-password-change.png) |
| H07 - CA007 Sign-in Risk Medium and High requires MFA - risk-based Conditional Access | H08 - CA008 User Risk High requires password change - Report-only mode |
| ![H09](screenshots/chapter%208/H09-risk-level-chart.png) | |
| H09 - Risk level chart showing 1 High risk user at 4.55% with new risky users per day trend | |

---

### Chapter 9 - Enterprise Applications

| | |
|---|---|
| ![I01](screenshots/chapter%209/I01-saml-configuration.png) | ![I02](screenshots/chapter%209/I02-permissions-user-read.png) |
| I01 - GitHub Enterprise Cloud SAML configuration with Identifier, Reply URL and Sign on URL | I02 - Enterprise app permissions showing User.Read delegated permission |
| ![I03](screenshots/chapter%209/I03-usage-insights-enterprise-applications.png) | ![I04](screenshots/chapter%209/I04-enterprise-apps-list.png) |
| I03 - Usage and insights showing app sign-in activity with 100% success rate | I04 - Enterprise applications list showing GitHub apps and Microsoft Graph |
| ![I05](screenshots/chapter%209/I05-user-assignment.png) | ![I06](screenshots/chapter%209/I06-singlesignon-SAML-certificates.png) |
| I05 - Users and groups showing IT-Staff-Security and admin account assigned to GitHub app | I06 - SAML certificate with Active status, thumbprint and 2029 expiry date |

---

### Chapter 10 - App Registrations

| | |
|---|---|
| ![J01](screenshots/chapter%2010/J01-app-registrations-list.png) | ![J02](screenshots/chapter%2010/J02-app-overview.png) |
| J01 - App registrations list showing PraveenLab PowerShell App | J02 - App registration overview showing Client ID, Tenant ID and Object ID |
| ![J03](screenshots/chapter%2010/J03-certificates-secrets.png) | ![J04](screenshots/chapter%2010/J04-api-permissions.png) |
| J03 - Certificates and secrets showing client secret with 6-month expiry | J04 - API permissions showing User.ReadWrite.All, Group.ReadWrite.All, Directory.ReadWrite.All with admin consent |
| ![J05](screenshots/chapter%2010/J05-app-registration-powershell.png) | |
| J05 - PowerShell connected as application via OAuth 2.0 client credentials listing all 22 users | |

---

### Chapter 11 - B2B External Collaboration

| | |
|---|---|
| ![K01](screenshots/chapter%2011/K01-guest-user-invited.png) | ![K02](screenshots/chapter%2011/K02-external-collaboration-settings.png) |
| K01 - Guest user created in tenant with User type Guest and #EXT# UPN | K02 - External collaboration settings showing member users can invite guests |
| ![K03](screenshots/chapter%2011/K03-collaboration-restrictions.png) | ![K04](screenshots/chapter%2011/K04-access-review-created.png) |
| K03 - Collaboration restrictions set to allow invitations to any domain | K04 - Quarterly Guest User Review created for Finance Team targeting guests only |

---

### Chapter 12 - Entra Connect

| | |
|---|---|
| ![L01](screenshots/chapter%2012/L01-upn-suffix-added.png) | ![L02](screenshots/chapter%2012/L02-upn-updated-powershell.png) |
| L01 - UPN suffix praveenlab2026.onmicrosoft.com added in Active Directory Domains and Trusts | L02 - PowerShell updating all 9 Delhi-HQ users to new UPN suffix showing green confirmation |

---

### Chapter 13 - Access Reviews

| | |
|---|---|
| ![M01](screenshots/chapter%2013/M01-ITSecurity-access-review-overview.png) | ![M02](screenshots/chapter%2013/M02-Identity-governance-access-review-dashboard.png) |
| M01 - IT-Staff-Security access review overview showing review configuration | M02 - Identity Governance access review dashboard |
| ![M03](screenshots/chapter%2013/M03-access-review-approval-status.png) | ![M04](screenshots/chapter%2013/M04-access-review-members-approve-deny.png) |
| M03 - Access review showing approval status and review progress | M04 - Access review members page showing approve and deny decision workflow |
| ![M05](screenshots/chapter%2013/M05-access-review-reviewed-approved.png) | ![M06](screenshots/chapter%2013/M06-access-review-notification-mail.png) |
| M05 - Access review completed showing approved decisions | M06 - Access review notification email received by reviewer |

---

### Chapter 14 - Monitoring

| | |
|---|---|
| ![N01](screenshots/chapter%2014/N01-Monitoring%20and%20health-sign%20in%20logs.png) | ![N02](screenshots/chapter%2014/N02-sign%20in%20logs-details.png) |
| N01 - Monitoring and health sign-in logs overview | N02 - Sign-in log detail showing full event information |
| ![N03](screenshots/chapter%2014/N03-monitoring%20and%20health-audit%20logs.png) | ![N04](screenshots/chapter%2014/N04-audit%20logs-details.png) |
| N03 - Monitoring and health audit logs overview | N04 - Audit log detail showing admin activity with full context |
| ![N05](screenshots/chapter%2014/N05-workbook-usage%20and%20insights.png) | ![N06](screenshots/chapter%2014/N06-diagonistic%20setting-dashboard.png) |
| N05 - Workbooks usage and insights dashboard | N06 - Diagnostic settings dashboard for log export configuration |

---

## Skills Demonstrated

| Role | Skills Covered in This Lab |
|------|---------------------------|
| IAM Engineer | Conditional Access 9 policies, MFA methods, SSPR, Dynamic Groups, Entra ID P1 and P2, PIM, Identity Protection |
| Identity Administrator | User lifecycle management, group governance, access reviews, hybrid identity, B2B collaboration |
| Security Engineer | Risk-based CA policies, Identity Protection risk detection, Tor-based anonymous IP detection, PIM just-in-time access |
| Cloud Administrator | App registrations, enterprise applications, SAML SSO configuration, Microsoft Graph API via client credentials |
| IT Support Engineer | Per-user MFA management, TAP generation, SSPR configuration, sign-in log investigation, audit log review |

---

## Tools and Technologies

| Category | Tools |
|----------|-------|
| Identity | Microsoft Entra ID P1 and P2, Conditional Access, MFA, SSPR, TAP, PIM, Identity Protection |
| Governance | Access Reviews, Entitlement Management, Group Expiration, Group-based Licensing |
| Applications | Enterprise Applications, SAML SSO, App Registrations, Microsoft Graph API |
| Hybrid Identity | Entra Connect, UPN Suffix, On-premises AD, Password Hash Sync preparation |
| External Collaboration | B2B Guest Users, External Identities, Guest Access Reviews |
| Automation | PowerShell, Microsoft Graph SDK, Client Credentials OAuth 2.0 flow |
| Monitoring | Sign-in Logs, Audit Logs, Workbooks, Diagnostic Settings, Identity Protection reports |
| Admin Portals | entra.microsoft.com, admin.microsoft.com, security.microsoft.com |

---

## Repository Structure

```
microsoft-entra-id-homelab/
├── README.md
├── LICENSE
├── requirements.txt
└── screenshots/
    ├── chapter 2/
    │   ├── B01-all-users-list.png
    │   ├── B02-user-properties.png
    │   ├── B03-user-account-tab.png
    │   ├── B04-bulk-operations.png
    │   ├── B05-per-user-mfa.png
    │   ├── B06-user-blocked.png
    │   ├── B07-deleted-users.png
    │   └── B08-revoke-sessions.png
    ├── chapter 3/
    │   ├── C01-all-groups-list.png
    │   ├── C02-dynamic-group-rule.png
    │   ├── C03-group-expiration-policy.png
    │   ├── C04-group-based-licensing.png
    │   └── C05-group-owners.png
    ├── chapter 4/
    │   ├── D01-auth-methods-list.png
    │   ├── D02-authenticator-enabled.png
    │   ├── D03-sms-disabled.png
    │   ├── D04-tap-enabled.png
    │   ├── D05-tap-generated.png
    │   ├── D06-registration-campaign.png
    │   └── D07-user-registration-details.png
    ├── chapter 5/
    │   ├── E01-ca-policies-list.png
    │   ├── E02-ca005-compliant-device.png
    │   ├── E03-ca006-signin-frequency.png
    │   └── E04-signin-log-ca-evaluation.png
    ├── chapter 6/
    │   ├── F01-sspr-properties.png
    │   ├── F02-sspr-auth-methods.png
    │   ├── F03-sspr-registration.png
    │   ├── F04-sspr-notifications.png
    │   └── F05-sspr-user-experience.png
    ├── chapter 7/
    │   ├── G01-pim-ga-active-assignments.png
    │   ├── G02-approve-requests.png
    │   ├── G03-Approving-request.png
    │   ├── G04-Approved-assignment-request.png
    │   ├── G05-pim-eligible-assignment-bob.png
    │   ├── G06-pim-role-settings-ga.png
    │   ├── G07-pim-my-roles.png
    │   └── G08-pim-audit-history.png
    ├── chapter 8/
    │   ├── H01-ID-Protection-Dashboard.png
    │   ├── H02-risky-signin-alice.png
    │   ├── H03-risk-detection-anonymous-ip.png
    │   ├── H04-risk-detection-signin-events-alice.png
    │   ├── H05-risky-signin.png
    │   ├── H06-risky-user.png
    │   ├── H07-signin-risk-level-medium-high.png
    │   ├── H08-user-risk-password-change.png
    │   └── H09-risk-level-chart.png
    ├── chapter 9/
    │   ├── I01-saml-configuration.png
    │   ├── I02-permissions-user-read.png
    │   ├── I03-usage-insights-enterprise-applications.png
    │   ├── I04-enterprise-apps-list.png
    │   ├── I05-user-assignment.png
    │   └── I06-singlesignon-SAML-certificates.png
    ├── chapter 10/
    │   ├── J01-app-registrations-list.png
    │   ├── J02-app-overview.png
    │   ├── J03-certificates-secrets.png
    │   ├── J04-api-permissions.png
    │   └── J05-app-registration-powershell.png
    ├── chapter 11/
    │   ├── K01-guest-user-invited.png
    │   ├── K02-external-collaboration-settings.png
    │   ├── K03-collaboration-restrictions.png
    │   └── K04-access-review-created.png
    ├── chapter 12/
    │   ├── L01-upn-suffix-added.png
    │   └── L02-upn-updated-powershell.png
    ├── chapter 13/
    │   ├── M01-ITSecurity-access-review-overview.png
    │   ├── M02-Identity-governance-access-review-dashboard.png
    │   ├── M03-access-review-approval-status.png
    │   ├── M04-access-review-members-approve-deny.png
    │   ├── M05-access-review-reviewed-approved.png
    │   └── M06-access-review-notification-mail.png
    └── chapter 14/
        ├── N01-Monitoring and health-sign in logs.png
        ├── N02-sign in logs-details.png
        ├── N03-monitoring and health-audit logs.png
        ├── N04-audit logs-details.png
        ├── N05-workbook-usage and insights.png
        └── N06-diagonistic setting-dashboard.png
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
