- JA3 hash detects equal ClientHello messages and by that identifies if two same configuration are used in different tls connections
https://engineering.salesforce.com/tls-fingerprinting-with-ja3-and-ja3s-247362855967/

## nmap flag explanation
https://explainshell.com/explain?cmd=nmap+-sU+-PN+-n


- Do two scans with nmap at different times with specified -oA flag to create output
- afterwards use git diff --no-index output.xml output2.xml to see the differences of the two network states
- 