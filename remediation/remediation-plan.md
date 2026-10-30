# Remediation plan

Status: all fixes below were applied on Day 6. After screenshots were not captured.

Fix in rating order, Critical first. For each fix: before screenshot, change, after screenshot, test, change log row, then set the status in the risk register.

Two safety rules: never delete the admin account, and never turn off security defaults until a Conditional Access MFA policy is live.

## Before you start
Create a second break-glass account before removing Daniel Kim's role, so the tenant keeps 2 Global Administrators.
1. admin.microsoft.com > Users > Active users > Add a user. Username breakglass2. Strong random password in the password manager.
2. Create user without product license. Roles: Global Administrator.
3. Sign in once in a private window and register MFA on a different device from admin.

## Critical
| ID | Fix | Verify |
|----|-----|--------|
| F-01 | Delete WAN rule Testing. See [firewall-plan.md](firewall-plan.md). | No WAN pass rules; browsing works |
| F-02 | Delete WAN RDP rule. Plan WireGuard VPN. | 3389 absent from rules and scan |
| F-03 | Entra > Roles & admins > Global Administrator > remove Daniel Kim. | Daniel's Assigned roles is empty; Global Admins are admin and breakglass2 |

## High
| ID | Fix | Verify |
|----|-----|--------|
| F-04 | Delete WAN FTP rule. | Rule gone |
| F-05 | Remove Sofia Alvarez from Finance and HR. | HR site > Check Permissions for Sofia shows none (allow 1 hour) |
| F-06 | Delete the Anyone link on Invoices-2026.xlsx. Policies > Sharing: New and existing guests, default Specific people, default View, Anyone links expire in 7 days or off. | Old link asks for sign-in in a private window |
| F-07 | Run an MFA registration campaign. Within 30 days, replace security defaults with a Conditional Access policy requiring MFA for all users. | User registration details shows all accounts MFA capable |

## Medium
| ID | Fix | Verify |
|----|-----|--------|
| F-08 | Delete guest Alex Reed (restorable for 30 days). | Gone from All users and Design-Team |
| F-09 | Remove Taylor Morgan from Design-Team. Keep Client-Projects. | As Taylor, Design-Team site shows access denied |
| F-10 | Guest invite settings: Only users assigned to specific admin roles. Clear owner-added guests in Microsoft 365 Groups settings. | Screenshots of both settings |
| F-11 | Teams external access: allow only client domains; turn off unmanaged accounts. | External access page |
| F-12 | Set Finance, HR, Management, Design-Team, IT-Support sites to Only people in your organization. | Active sites External sharing column |
| F-13 | Require verification for anonymous join; keep anonymous users in the lobby; presenters limited to org and guests. | Meeting policy page |
| F-14 | Acme-Rebrand > Manage access > remove Taylor's direct share. | No direct entry for Taylor |
| F-15 | Remove the Business Premium license from admin. | Billing > Licenses shows one fewer in use |

## Low
| ID | Fix | Verify |
|----|-----|--------|
| F-16 | Delete disabled LAN rules. | LAN list shows anti-lockout, DNS, web only |
| F-17 | Set the Pixelnestlab team to Private, or archive it. | Teams list shows Private |
| F-18 | Restrict shared channel creation and external invites, or accept with quarterly review. | Teams policy page |
| F-19 | Back up config, update OPNsense to 26.7.5, limit GUI to LAN. | Dashboard version |

## Likely to accept
| ID | Reason |
|----|--------|
| F-18 | Channel creation supports client work. Accept with a quarterly review of channel sites. |
| Guest access in Teams | Stays On because contractors need Client-Projects. Control is group membership, reviewed quarterly. |
