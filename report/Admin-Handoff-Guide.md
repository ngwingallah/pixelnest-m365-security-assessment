# PixelNest Administrator Handoff Guide

For the person who manages PixelNest after this assessment. Assumes Microsoft 365 basics, not knowledge of this tenant.

## Accounts and roles
| Account | Role | Why |
|---------|------|-----|
| admin@ | Global Administrator | Break-glass account 1 |
| breakglass2@ | Global Administrator | Break-glass account 2 (create before removing Daniel Kim's role) |
| adm-jordan.blake@ | User Administrator | Day-to-day user admin, separate from Jordan's mailbox account |

- Store break-glass credentials in the password manager, not in email.
- Use break-glass accounts only when normal admin sign-in fails.
- Sign in to each once a month to confirm it works.
- Nobody uses an admin role from a licensed, everyday account.

## New starter
1. Create the user with department and job title filled in.
2. Assign Microsoft 365 Business Premium.
3. Add to one department group only.
4. Confirm MFA registration on first sign-in.

## Role change
1. Remove old groups first, then add new ones.
2. Check for direct file shares from the old role (Manage access on each library).

## Leaver
1. admin.microsoft.com > Users > the user: Block sign-in, Sign out of all sessions, Reset password.
2. Remove groups and roles.
3. Transfer OneDrive files to the manager when deleting the user.
4. Remove the license.

## Guests
1. The Operations Manager approves every guest.
2. Guests join Client-Projects only.
3. Record an end date. Remove the guest when the project ends.
4. Share client files through group membership, not direct shares.

## Monthly checks
- Admin role members (Entra > Roles & admins)
- Guest last sign-in dates and invite status
- Secure Score (baseline 83.11% on 3 October 2026)
- Anyone links in SharePoint
- Audit log search for new sharing

## Quarterly checks
- Group membership against departments
- Firewall rules against the rule table in docs/architecture.md
- Teams channel sites and external domains list

## Firewall changes
1. Back up the config first (System > Configuration > Backups).
2. Give every rule a clear description and owner. No "Testing" or "Temp" rules.
3. Never expose RDP, SSH, SMB or FTP to the WAN. Use the VPN.
4. Turn on logging for any WAN pass rule.
5. Record every change in remediation/change-log.xlsx.
