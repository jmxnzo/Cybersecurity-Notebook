---
tags:
  - LiteratureNote
title: Static Detection of Application Backdoors
author(s): Chris Wysopal, Chris Eng
year: "2008"
date created: "{{date}}"
link: 
conference:
---
## Application backdoors
- insert in the code base of application(after system compromise, legitimate rights)
- subvert the compiler, linker, or other components in the development tool chain


### Current State of Detection
For compiled software, a subverted development tool chain[1] or compromised distribution site requires binary analysis for backdoor detection since the backdoor only exists after compilation or linking. In addition, modern development practices often dictate the usage of frameworks and libraries where only binary code is available. When backdoor reviews
are performed at the source code level there are still
significant portions of software that are not getting reviewed.

# Application backdoor classes
#### • Special credentials
- in form of username, password, password hash
- logic: comparison to the special credential or insert credentials to store
• Hidden functionality
• Unintended network activity
• Manipulation of security critical parameters


### Detection strategies
- Identify all static variables that look like usernames or passwords (start with ASCII character set)
- variables that store MD5 or SHA1 hashes
- cryptographic keys, static variables multiple of key length
- crypto API calls where arrays or plain text data is passed in as parameter