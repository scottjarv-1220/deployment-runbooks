# Project: Enterprise Webex SSO Implementation & SAML Integration
**Target Go-Live:** Date / Year 
**Role:** Project Lead / Systems Analyst

# Executive Summary
This runbook outlines the migration of a 2000 user enterprise environmentfrom Basic Authentication to Entra ID SAML Single Sign-On (SSO). The primary objective was to enhance corporate security while maintaining zero to minimal downtime for mission critical collaboration tools, including high profile external Board of Directors access. This rundown is for an evnironment using Control Hub Pro Pack and a hybrid Exchange Calendar Connector. On prem Exchange, on prem Active Directory with EntraID.

This runbook is gaming the following scenario. With above Executive Summary, implementation is occuring on a Thursday evening to assure minimal downtime.

# Authentication Tiering & Account Logic
A critical component of this deployment was the classification of accounts into specific authentication tiers to ensure zero to minimal downtime for departmental operations.

| Account Category | Auth Method | Use Case |
| :--- | :--- | :--- |
| **Standard User** | Entra ID (SSO) | Primary workforce (2,000+ users). |
| **Functional/Service** | Basic Auth (Non-SSO) | Shared accounts for Group1, Group2, Group3 to prevent "Individual-Linked" failures. |
| **Break-Glass Admin** | Basic Auth (Bypass) | Emergency access (`generic-account`) to revert IDP settings if SSO handshake fails. |
| **External/Board** | Basic Auth (Manual) | Non-domain accounts (e.g., Gmail) providing high-level governance access without requiring internal AD credentials. |

### Justification Strategy
- **Security Compliance:** Provided formal justification to the Cyber Security team for all accounts remaining on Basic Authentication. Group accounts functioning as announcement spaces for high turnover business areas where individual paid accounts is impractical moved to Basic Free Tier licensing. Group accounts serving a single functional purpose (ie- Workspaces) with free Basic Teir messaging and paid Meetings are backed by the users who use these accounts to have individual paid licenses. 
- **B2B Guest Exploration:** Initiate a long term roadmap to migrate Board members to Entra ID B2B Guest accounts to eventually eliminate Basic Authentication of this group.

## Pre Deployment Validation (T-Minus 7 Days)
- [ ] **Stakeholder Approval:** Final verification of SSO Justification via Cyber Security.
- [ ] **Impact Assessment:** Identified potential "Orphaned" accounts (Conference Rooms, External Board of Directors).
- [ ] **Testing Strategy:** Create am external sandbox account to simulate any external (eg- Board of Directors) login flows.
- [ ] **Communication:** Draft transparent user notices with public internal Confluence Q&A documentation. Test links in a private window session to verify their functionality.

## Risk Mitigation & "Break-Glass" Strategy
To prevent administrative lockout during the IDP switchover:
- [ ] **Break-Glass Group:** Verify a dedicated Control Hub group with SSO bypass permissions. Verify correct group accounts are placed in here.
- [ ] **Functional Account Tiering:** Audit service accounts (Group1, Group2, Group3, etc.) to ensure tiering remains intact post enforcement.
- [ ] **Emergency Credentials:** Secure offline access to `generic-account` administrative credentials.

## Execution Phase (Go-Live Window)
### Phase 1: Communication
- [ ] **Public Notice** Within five days of go-live, send out internal public notice communication of upcoming Webex SSO change and link public internal Conflunce Q&A documentation.
### Phase 1: Authentication Switch
* **Primary IDP:** Enable Entra ID SAML.
* **Secondary IDP:** Enable Webex Basic Auth specifically for the "Break-Glass" and Group accounts.
* **Enforcement:** Activate SSO enforcement across the organization.

### Phase 2: Functional Validation (UAT)
- [ ] **Admin Bypass:** Confirm `generic-account` bypasses SSO successfully.
- [ ] **Internal SSO:** Verify Entra ID handshake for internal staff.
- [ ] **External/Guest Access:** Validate the external accounts are unaffected by internal IDP changes.
- [ ] **Hybrid Services:** Confirm Calendar Service functionality by generating test meetings in integrated conference rooms.

## Emergency Rollback Plan
In the event of a critical authentication failure:
1. Authenticate via **Break-Glass** bypass account.
2. Navigate to `Control Hub -> Authentication`.
3. Revert Primary IDP to **Webex Basic Auth**.
4. Trigger Cisco TAC P1 Incident protocol.

## 📈 Post-Migration Roadmap
* **Short-Term:** 24-hour hyper-care monitoring for login failures.
* **Long-Term:** Evaluate Entra ID B2B Guest accounts for Board members to further unify the security perimeter.
