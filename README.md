# WI-FI-DNS-Fix-  Date: 2025-03-15 
Scripts, notes, and reflections for diagnosing and fixing Wi-Fi/DNS issues on Linux/macOS terminals
Context 
After a router firmware update, my laptop lost internet connectivity while all other devices worked fine.
I needed internet to test scripts and commands into my VM. The outage simply blocked my workflow and forced me to dig into the network.
**Investigation**
Ran ifconfig: IP checked okay 
ping 8.8.8.8: No response
nslookup google.com: DNS not resolving.
Checked routing table: Default gateway correct, but DNS entries missing.
Hypothesis: Router reboot reset network configs, local DNS cache corrupted. 
Tried temporary fixes **restart NetworkManager** reboot: Didnt fully resolve the issue.
**Fix**
Edited **/etc/resolv.conf** to manually set DNS servers 8.8.8.8 and 1.1.1.1
Restarted network interface: **sudo systemctl restart NetworkManager**
Verified connectivity with **ping google.com**: Success 
OPT: Run **tracerroute google.com** to confirm routing was correct 
**Prevention** 
Keep a backup of working DNS/network configs for quick recovery.
Maintain a small quick-fix scrift script for common network issues. 
Document system or router changes to trace problems faster.
Systematic approach: Ping-DNS-Logs
**Reflection**
This experience taught me patience and the benefit of a through investigate 
Approach methondically test network for stabilty build that skill 
I feel confident in diagnosing network issues knowing I can always find a way to figure it out.
From now on ill challenge problems themselves with curiosity, calm and optimism.
