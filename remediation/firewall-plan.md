# Firewall remediation plan

Status: applied on Day 6. After screenshots and the after scan were not captured.

Date: 28/10/2026  
Config backup: D5-01-config-before.xml (kept offline; sanitized excerpt in [configs/](../configs/opnsense-config-excerpt-sanitized.xml))  
Rollback for every change: System > Configuration > Backups > Restore, select D5-01-config-before.xml, reboot.

Apply changes one at a time and test after each.

## F-01: WAN allow any to any (Testing)
- Action: Delete the rule (seq 311), then Apply changes.
- Replacement: None. The default deny handles unmatched inbound traffic.
- Test: WAN rule list shows no pass rules. Browsing from Ubuntu still works.

## F-02: WAN allow TCP 3389 to 192.168.1.126 (Temp remote access)
- Action: Delete the rule (seq 111).
- Replacement: Remote access through a WireGuard VPN on OPNsense with MFA-protected accounts. The rule exists because someone needed remote access; deleting it without a replacement invites someone to re-open it.
- Test: Rule gone. Re-run the nmap scan and confirm 3389 is not listed.

## F-04: WAN allow TCP 21 to 192.168.1.126 (Old client file transfer)
- Action: Delete the rule (seq 211).
- Replacement: Share client files through the Client-Projects SharePoint site with Specific people links.
- Test: Rule gone.

## F-16: Rule hygiene
- Action: Delete the 2 disabled default LAN rules (seq 1 and 11). Turn on logging for any WAN pass rule that remains (none should).
- Test: LAN list shows only the anti-lockout, DNS and web rules.

## F-19: Firmware and GUI exposure
- Action: Take a new config backup, then System > Firmware > Updates to move from 26.7 to 26.7.5. Under System > Settings > Administration, limit the GUI listen interface to LAN.
- Test: Dashboard shows the new version. GUI still loads from 192.168.1.126.

## After the changes
1. Download a new config backup. Save as D6-config-after.xml.
2. Re-run `sudo nmap -sS -sV 192.168.1.1 -oN nmap-firewall-after.txt`. Save as D6-nmap-after.txt.
3. Log each change in [change-log.xlsx](change-log.xlsx).
