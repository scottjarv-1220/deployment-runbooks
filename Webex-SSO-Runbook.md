# Project: Enterprise Webex SSO Implementation & SAML Integration
**Target Go-Live:** Date / Year 
**Role:** Project Lead / Systems Analyst

## Executive Summary
This runbook outlines the migration of a 2000 user enterprise environmentfrom Basic Authentication to Entra ID SAML Single Sign-On (SSO). The primary objective is to enhance corporate security while maintaining minimal downtime for mission critical collaboration tools, including high profile external users. 

This runbook is gaming the following scenario. With above Executive Summary, implementation is occuring on a Thursday evening to assure minimal downtime.

## Authentication Tiering & Account Logic
A critical component of this deployment was the classification of accounts into specific authentication tiers to ensure minimal downtime for departmental operations.

| Account Category | Auth Method | Use Case |
| :--- | :--- | :--- |
| **Standard User** | Entra ID (SSO) | Primary workforce (2000+ users). |
| **Functional/Service** | Basic Auth (Non SSO) | Shared accounts for Group1, Group2, Group3 to prevent "Individual Linked" failures. |
| **Break-Glass Admin** | Basic Auth (Bypass) | Emergency access (`generic-account`) to revert IDP settings if SSO handshake fails. This account aslo serves as the system architect service account. Its use case is required to successfully run the AD Sync server and the Csico Webex Expressway Calendar Connector. |
| **External** | Basic Auth (Manual) | Non domain accounts (e.g., Gmail) providing high level governance access without requiring internal AD credentials. |

### Justification Strategy
- **Security Compliance:** Provided formal justification to the Cyber Security team for all accounts remaining on Basic Authentication. This evnironment is using Control Hub Pro Pack and a hybrid Exchange Calendar Connector: on prem Exchange, on prem Active Directory with EntraID. Pro Pack allows you to have multiple IDPs: one for SSO and and one for Webex Basic Authentication. Webex Terms of Service requires NamedUsers be paired with existing users, ie- a single person. Envronment has a small amount of group accounts. Some that function as announcement spaces to several hundred employees in areas where there is high turnover, flex and seasonal employment where individual paid accounts is unrealistic and impractical. The free tier allows bypassing the NamedUser requirement and the Deployed Knowledge Worker count for True Forwarding. There are a very small number of group accounts that serve as functional Workspace accounts due to narrowly defined use cases and those users who use these accounts each have their own personal, paid license. One group account within IT that serves as the system archtitect service and break-glass account.

- **B2B Guest Exploration:** Initiate a long term roadmap to migrate Board members to Entra ID B2B Guest accounts to eventually eliminate Basic Authentication of this group.

## Pre Deployment Validation (Friday before Go-Live)
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
### Phase 1: Communication (Monday before Go-Live)
- [ ] **Public Notice** Send out internal public notice communication of upcoming Webex SSO change and link public internal Conflunce Q&A documentation. Send out at 8AM for highest visibility.

### Phase 1.1: Communication (Wednesday before Go-live)
- [ ] **Public Notice** Send out internal public notice communication of upcoming Webex SSO change and link public internal Conflunce Q&A documentation. Send out at 8AM for highest visibility.
- [ ] **Break-glass account** Confirm break-glass account passwords are accessible and stored securely.
- [ ] **TAC Support** Pre-open Cisco TAC case or have TAC contact information ready.
      
### Phase 2: Go-Live Day and Functional Validation
- [ ] **TAC Support** If not done the day prior, pre-open Cisco TAC case or have TAC contact information ready. Do beofre 12noon.

### Phase 2.1: Go-Live Time
- [ ] **Two Browsers** Open two browser sessions. Control Hub as logged in as an Admin and one with the `generic-account` break glass account standing by.
- [ ] **Calendar** Final confirmation check Hybrid Calendar Service is functioning correctly in Control Hub.
- [ ] **Primary IDP:** Enable Entra ID SAML.
- [ ] **Secondary IDP:** Enable Webex Basic Auth specifically for the "Break-Glass" and Group accounts.
- [ ] **Enforcement:** Activate SSO enforcement across the organization.
- [ ] **Confirm** Confirm SSO enforcement is active.
- [ ] **Test** Immediately test `generic-account` break glass account login and confirm it still bypasses SSO.
- [ ] **Test** Test your own Webex Admin login via Entra ID SSO.
- [ ] **Test** Test external test account to confirm external users are unaffected.
- [ ] **Test** Confirm Hybrid Calendar Service is still functioning post switchover by creating a meeting. This will confirm conference room calendar accounts are unaffected.

## Emergency Rollback Plan
In the event of a critical authentication failure:
1. Authenticate via **Break-Glass** bypass account.
2. Navigate to `Control Hub -> Authentication`.
3. Revert Primary IDP to **Webex Basic Auth**.
4. Trigger Cisco TAC P1 Incident protocol.

## Post-Migration Roadmap
* **Short-Term:** 24 hour monitoring for login failures.
* **Long-Term:** Evaluate Entra ID B2B Guest accounts for Board members to further unify the security perimeter.
