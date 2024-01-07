Tips and hints for carrying out the test:

� Focus on vulnerabilities that, directly or indirectly, allow you to access or take control of the server (always exploiting web vulnerabilities). There are more than 4 of this type, and there may also be vulnerabilities that are not exploitable and/or more challenging to exploit; this reflects the real world.


� Some tools/websites that can be useful for conducting the penetration test include:
   • Detection, scanning, information extraction, vulnerability querying, etc.
      o Nmap - Choosing the right parameters can provide many clues, especially initially.
      o BurpWP - Useful for finding vulnerabilities in plugins and themes. To work correctly with the WPScan API (and have 25 free daily requests), you need to register with WPScan and request the token.
      o Metasploit - "Scanner" type modules are very useful for this phase.
      o CVE Details - Check for possible vulnerabilities in identified technologies.
   • User listing, password brute-force, etc.
      o Burp Suite and ZAP - The go-to tools for web Pentesting.
      o Password list - In case a dictionary attack is necessary.
   • Exploiting vulnerabilities.
      o Metasploit - The most widely used tool for finding and exploiting vulnerabilities.
      o Exploit DB and GitHub - Many hackers post their exploits, PoCs, etc., on these websites. They can be easily found by searching for the name and version of the technology, CVE, etc. There's more to explore beyond Metasploit...

� In case you need to perform a brute-force attack, these can take hours. It is advisable to start with small dictionaries and, if nothing is found, try larger dictionaries with more words. For this practice, this dictionary is recommended.