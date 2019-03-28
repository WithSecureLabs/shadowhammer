# Batch-mode shadowhammer MAC address checker #

Kaspersky recently discovered and analysed the 'Shadowhammer' attack (https://securelist.com/operation-shadowhammer/89992). They did some great analysis and released a tool for sysadmins to use to determine if their systems were targetted. The released tools, however, weren't very easily scriptable, so we have created this small python script to fix that. We've taken the hashes from Kaspersky's own tool and wrapped them up in a nice commandline Python interface (which can also be used offline, addressing potential privacy issues).

# Usage #

The tool, by default, will scan all network cards on the current system for their presence in the Shadowhammer malware:
```
C:\shadowhammer\>python check.py
SHADOWHAMMER MAC address checking tool from Countercept
Countercept: https://github.com/countercept and https://twitter.com/countercept
Kaspersky's analysis: https://securelist.com/operation-shadowhammer/89992
Contains hashes taken from Kaspersky's checking tool (thanks Kaspersky!)
Returns non-zero if at least one MAC address specified is targetted by SHADOWHAMMER
Checking 2 addresses..
No affected MACs detected (checked 2)
```

It can also accept MAC addresses via the commandline:
```
check.py --mac-addresses 005050613370
```

Or from a text file:
```
check.py --mac-addresses-filename toscan.txt
```
If scanning from a text file, addresses should be newline-delimited ASCII, like this:
```
005050613370
0050c0dec0de
1010c00dade0
```

You can also use colons or hyphens as delimiters in your MAC addresses.

# False positives #

The malware will filter on a few extremely common MAC addresses. These have been removed from the tool, as their presence does _not_ conclusively indicate targetting. They are:

- 0c5b8f279a64\
  This is used by every single Huawei E5573 USB modem. If you have this modem, you will have this MAC address.
- 001e101f0000\
  Similarly, this is used by all Huawei HWD12 LTE modems.
- 005056c00008\
  The default address used by VMWare workstation.

# Also see #

Countercept's twitter: https://twitter.com/countercept \
Kaspersky's initial analysis: https://securelist.com/operation-shadowhammer/89992
