# Webex Functional & Shared Account Governance
**Date:** May 2026  
**Status:** Audited & Verified  
**Objective:** Document business justification, licensing compliance, and governance rationale for non-personal domain accounts.

## 📋 Executive Summary
This document records the justification for non personal "Functional Accounts" operating within the enterprise Webex domain. These accounts serve specific operational needs and are structured to ensure full compliance with Cisco licensing agreements. As of May 2026, Cisco has confirmed in writing that free tier accounts do not impact the Deployed Knowledge Worker (DKW) count for True Forward purposes.

---

## 1. Functional Announcement Spaces (Free Tier)
**Accounts:** `Basic-Group1`, `Basci-Group2`, `Basic-Group3`  
**License Status:** Free (No paid licenses assigned)

### Business Justification
These accounts serve high turnover, non desk worker populations (front/back of house staff). Due to the seasonal and rotational nature of this workforce, managing individual paid licenses for every member is operationally impractical. The free tier facilitates essential communication without administrative bloat or unnecessary license consumption.

---

## 2. System Architecture & "Break-Glass" (Paid)
**Account:** `generic-architect-account`  
**License Status:** Paid (Messaging & Meetings)

### Business Justification
This is a mission-critical service account serving two mandatory functions:
1. **Hybrid Calendar Service:** Essential for on prem Exchange and Active Directory synchronization.
2. **Break-Glass Admin:** Provides emergency environment access if SSO or primary admin accounts fail.
*Note: Use is strictly limited to the Technology Department; all authorized users possess their own individual paid licenses.*

---

## 3. Functional Workspaces (Paid Meetings)
**Accounts:** `Workspace-Group1`, `Workspace-Group2`  
**License Status:** Paid Meetings / Free Messaging

### Business Justification
These accounts host role-specific events that require advanced meeting functionality. They are not general-purpose accounts; they support organizational training and recruitment workflows where recorded content must remain siloed for privacy.

---

## 4. Corporate Events & Broadcast (Paid Meetings)
**Account:** `Workspace-Internal-Events`  
**License Status:** Paid Meetings / Free Messaging

### Business Justification
`Workspace-Internal-Events` is a dedicated workspace for large-scale internal corporate broadcasts (~12/year). 
* **Privacy Logic:** A separate account was mandated to prevent broadcast recordings from mixing with confidential Workspace-Group1 or Workspace-Group2 archives.
* **Operational Need:** Facilitates events exceeding the 40-minute free tier limit and provides a 1:1 non-PSTN calling license for administrator pre-event testing.

---

## ⚖️ Governance & Compliance Notes
* **Audit Status:** All functional accounts were audited and validated in May 2026.
* **Licensing Integrity:** Paid functional accounts are used for operational necessity and are not a substitute for individual NamedUser licenses.
* **Annual Review:** This document is subject to annual review or upon significant changes to Cisco's licensing model.
