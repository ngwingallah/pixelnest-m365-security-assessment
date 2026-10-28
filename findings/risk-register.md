# Risk register

All 19 findings were fixed on Day 6 following the [remediation plan](../remediation/remediation-plan.md). After screenshots were not captured, so evidence shows the state before each fix.

Scoring: Likelihood (1-5) x Impact (1-5). 20-25 Critical, 12-19 High, 6-11 Medium, 1-5 Low. The working copy with formulas is [risk-register.xlsx](risk-register.xlsx).

| ID | Finding | Area | L | I | Score | Rating | Owner | Status |
|----|---------|------|---|---|-------|--------|-------|--------|
| F-01 | WAN rule allows any to any | Firewall | 5 | 5 | 25 | Critical | IT Lead | Remediated |
| F-02 | RDP (TCP 3389) open from the WAN | Firewall | 5 | 4 | 20 | Critical | IT Lead | Remediated |
| F-03 | Designer holds Global Administrator | Roles | 4 | 5 | 20 | Critical | IT Lead | Remediated |
| F-04 | FTP (TCP 21) open from the WAN | Firewall | 4 | 3 | 12 | High | IT Lead | Remediated |
| F-05 | Designer is a member of Finance and HR | Groups | 3 | 4 | 12 | High | Operations Manager | Remediated |
| F-06 | Anyone edit link on invoice file; org allows Anyone links | SharePoint | 3 | 4 | 12 | High | IT Lead | Remediated |
| F-07 | 14 of 17 accounts not registered for MFA | MFA | 3 | 4 | 12 | High | IT Lead | Remediated |
| F-08 | Stale guest with Design-Team access | Guests | 3 | 3 | 9 | Medium | Operations Manager | Remediated |
| F-09 | Contractor in internal Design-Team | Guests | 3 | 3 | 9 | Medium | Creative Director | Remediated |
| F-10 | Anyone can invite guests; group owners can add guests | Guests | 3 | 3 | 9 | Medium | IT Lead | Remediated |
| F-11 | Teams external access open to all domains and personal accounts | Teams | 3 | 3 | 9 | Medium | IT Lead | Remediated |
| F-12 | Sensitive sites allow external sharing | SharePoint | 3 | 3 | 9 | Medium | IT Lead | Remediated |
| F-13 | Anonymous users can join meetings unverified | Teams | 2 | 3 | 6 | Medium | IT Lead | Remediated |
| F-14 | Direct edit share to a guest on a client folder | SharePoint | 2 | 3 | 6 | Medium | Creative Director | Remediated |
| F-15 | Break-glass admin is licensed with a mailbox | Roles | 2 | 3 | 6 | Medium | IT Lead | Remediated |
| F-16 | Firewall rule hygiene | Firewall | 2 | 2 | 4 | Low | IT Lead | Remediated |
| F-17 | Org-wide team is Public | Teams | 2 | 2 | 4 | Low | IT Lead | Remediated |
| F-18 | Any user can create private and shared channels | Teams | 2 | 2 | 4 | Low | IT Lead | Remediated |
| F-19 | Firewall update pending | Firewall | 2 | 2 | 4 | Low | IT Lead | Remediated |

## Detail

### F-01 WAN rule allows any to any
Rating: Critical (25)  
Area: Firewall  
Owner: IT Lead

The WAN rule Testing passes all IPv4 traffic from any source to any destination. It sits above the default deny and cancels inbound filtering, so the firewall stops protecting the LAN.

Evidence: [D1-06a-wan-rules](../evidence/day1/D1-06a-wan-rules.png)

Recommendation: Delete the rule. Rely on the default deny for unmatched inbound traffic.

### F-02 RDP (TCP 3389) open from the WAN
Rating: Critical (20)  
Area: Firewall  
Owner: IT Lead

Temp remote access passes TCP 3389 from any source to the Ubuntu host 192.168.1.126. RDP is one of the most scanned services on the internet and a common entry point for password spraying and ransomware.

Evidence: [D1-06a-wan-rules](../evidence/day1/D1-06a-wan-rules.png)

Recommendation: Delete the rule. Provide remote access through a WireGuard VPN with MFA-protected accounts.

### F-03 Designer holds Global Administrator
Rating: Critical (20)  
Area: Roles  
Owner: IT Lead

Daniel Kim (Designer) holds Global Administrator on his daily, licensed account. A phished password gives an attacker full control of the tenant.

Evidence: [D2-01-global-admins](../evidence/day2/D2-01-global-admins.png)

Recommendation: Create a second break-glass account first, then remove the role from Daniel Kim.

### F-04 FTP (TCP 21) open from the WAN
Rating: High (12)  
Area: Firewall  
Owner: IT Lead

Old client file transfer passes TCP 21 to 192.168.1.126. FTP sends credentials and files in clear text, and the client relationship it served has ended.

Evidence: [D1-06a-wan-rules](../evidence/day1/D1-06a-wan-rules.png)

Recommendation: Delete the rule. Share client files through SharePoint with Specific people links.

### F-05 Designer is a member of Finance and HR
Rating: High (12)  
Area: Groups  
Owner: Operations Manager

Sofia Alvarez (Designer) is a member of the Finance and HR groups. She can open invoices, salary data and personal records that her role does not need.

Evidence: [D2-10-members-finance](../evidence/day2/D2-10-members-finance.png), [D2-10-members-hr](../evidence/day2/D2-10-members-hr.png)

Recommendation: Remove Sofia Alvarez from Finance and HR. Keep Design-Team only.

### F-06 Anyone edit link on invoice file; org allows Anyone links
Rating: High (12)  
Area: SharePoint  
Owner: IT Lead

Invoices-2026.xlsx in the Finance site has an Anyone link with edit rights. Org sharing for SharePoint and OneDrive is set to Anyone, default permission is Edit, and Anyone links never expire.

Evidence: [D4-05-issue-8-anyone-edit-link](../evidence/day4/D4-05-issue-8-anyone-edit-link.png), [D4-01-org-sharing](../evidence/day4/D4-01-org-sharing.png), [D4-02-link-settings](../evidence/day4/D4-02-link-settings.png)

Recommendation: Delete the Anyone link. Set org sharing to New and existing guests, default link Specific people, default permission View, Anyone links off or expiring within 7 days.

### F-07 14 of 17 accounts not registered for MFA
Rating: High (12)  
Area: MFA  
Owner: IT Lead

Only admin, Olivia Grant and Priya Shah are MFA capable. Security defaults prompt the others at first sign-in, so an attacker who has a password first could register their own device.

Evidence: [D2-16-mfa-registration](../evidence/day2/D2-16-mfa-registration.png)

Recommendation: Run a registration campaign now. Move to a Conditional Access policy that requires MFA for all users.

### F-08 Stale guest with Design-Team access
Rating: Medium (9)  
Area: Guests  
Owner: Operations Manager

Alex Reed (Reed Studio) never accepted his invite, his project ended in March 2026, and he is still a member of Design-Team.

Evidence: [D2-13-guest-alex](../evidence/day2/D2-13-guest-alex.png)

Recommendation: Delete the guest account. Add a guest end date to the onboarding process.

### F-09 Contractor in internal Design-Team
Rating: Medium (9)  
Area: Guests  
Owner: Creative Director

Taylor Morgan is a contractor who needs Client-Projects only, but is also a member of Design-Team and can read internal design work.

Evidence: [D2-12-guest-taylor](../evidence/day2/D2-12-guest-taylor.png), [D2-10-members-design-team](../evidence/day2/D2-10-members-design-team.png)

Recommendation: Remove Taylor Morgan from Design-Team. Keep Client-Projects.

### F-10 Anyone can invite guests; group owners can add guests
Rating: Medium (9)  
Area: Guests  
Owner: IT Lead

Guest invite settings allow anyone in the organization, including guests, to invite guests. Microsoft 365 Groups also let owners add outside people. Both bypass any approval step.

Evidence: [D2-14-external-collab](../evidence/day2/D2-14-external-collab.png), [D3-05-m365-groups](../evidence/day3/D3-05-m365-groups.png)

Recommendation: Limit invites to users assigned specific admin roles. Turn off owner-added guests or document an approval step.

### F-11 Teams external access open to all domains and personal accounts
Rating: Medium (9)  
Area: Teams  
Owner: IT Lead

External access allows all external domains and chats with unmanaged Microsoft accounts. Anyone with a Teams account can message staff, a known route for phishing and fake IT support.

Evidence: [D3-07a-external-access](../evidence/day3/D3-07a-external-access.png), [D3-07b-external-access-unmanaged](../evidence/day3/D3-07b-external-access-unmanaged.png)

Recommendation: Allow only client domains. Turn off unmanaged Teams accounts.

### F-12 Sensitive sites allow external sharing
Rating: Medium (9)  
Area: SharePoint  
Owner: IT Lead

External sharing is On for every site, including Finance, HR and Management. Only Client-Projects needs guest sharing.

Evidence: [D4-04-sites](../evidence/day4/D4-04-sites.png)

Recommendation: Set Finance, HR, Management, Design-Team and IT-Support to Only people in your organization.

### F-13 Anonymous users can join meetings unverified
Rating: Medium (6)  
Area: Teams  
Owner: IT Lead

Anonymous users can join meetings without verification and interact with apps. Lobby bypass is already limited to people in the org and guests, which reduces the risk.

Evidence: [D3-01-meeting-policy](../evidence/day3/D3-01-meeting-policy.png), [D3-02-meeting-settings](../evidence/day3/D3-02-meeting-settings.png)

Recommendation: Keep anonymous join for clients, but require verification and keep anonymous users in the lobby. Set Who can present to people in the org and guests.

### F-14 Direct edit share to a guest on a client folder
Rating: Medium (6)  
Area: SharePoint  
Owner: Creative Director

The Acme-Rebrand folder is shared directly with Taylor Morgan with edit rights. The share survives removal from Client-Projects, so access would outlive the contract.

Evidence: [D4-05-issue-9-direct-guest-share](../evidence/day4/D4-05-issue-9-direct-guest-share.png)

Recommendation: Remove the direct share. Grant access through Client-Projects membership only.

### F-15 Break-glass admin is licensed with a mailbox
Rating: Medium (6)  
Area: Roles  
Owner: IT Lead

The admin account holds a Business Premium license and mailbox. Using it for email raises its phishing exposure. Jordan Blake's separate unlicensed admin account is the correct pattern.

Evidence: [D1-02-users](../evidence/day1/D1-02-users.png)

Recommendation: Remove the license from admin. Keep 2 unlicensed break-glass accounts.

### F-16 Firewall rule hygiene
Rating: Low (4)  
Area: Firewall  
Owner: IT Lead

No WAN pass rule logs traffic, and the two disabled default LAN rules remain in the list where they could be re-enabled by mistake.

Evidence: [D1-06b-lan-rules](../evidence/day1/D1-06b-lan-rules.png)

Recommendation: Delete the disabled rules. Log any WAN pass rule that remains.

### F-17 Org-wide team is Public
Rating: Low (4)  
Area: Teams  
Owner: IT Lead

The default team Pixelnestlab is Public with 14 members. Any member can join and read its files, so sensitive files posted there reach the whole company.

Evidence: [D3-08-teams-list](../evidence/day3/D3-08-teams-list.png)

Recommendation: Set the team to Private or archive it if unused.

### F-18 Any user can create private and shared channels
Rating: Low (4)  
Area: Teams  
Owner: IT Lead

The global Teams policy lets every user create private and shared channels and invite external users to shared channels. Each channel creates a separate SharePoint site that is easy to miss in reviews.

Evidence: [D3-04-teams-policy](../evidence/day3/D3-04-teams-policy.png)

Recommendation: Restrict shared channel creation and external invites to owners, or accept with a quarterly review.

### F-19 Firewall update pending
Rating: Low (4)  
Area: Firewall  
Owner: IT Lead

The firewall runs OPNsense 26.7 while 26.7.5 is released with security fixes. The web GUI listens on all interfaces, which the any-to-any WAN rule makes reachable.

Evidence: [D1-07a-opnsense-dashboard](../evidence/day1/D1-07a-opnsense-dashboard.png), [D5-05-nmap](../evidence/day5/D5-05-nmap.png)

Recommendation: Back up the config, then update. Limit GUI access to an admin host.
