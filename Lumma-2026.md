# 2026-01-31 - TRAFFIC ANALYSIS EXERCISE: LUMMA IN THE ROOM-AH

[Link to exercise](https://malware-traffic-analysis.net/2026/01/31/index.html)

## Write-Up

Knowing the IP that triggered the incident, 153[.]92[.]1[.]49, we can filter to see which internal host interacted with it.

![img](https://i.ibb.co/xKB1vRZs/Infected-IP.png)

Noting 10[.]1[.]21[.]58 as having interacted with the malicious IP, this is further corroborated by inspecting the Conversations section and seeing 10[.]1[.]21[.]58 as being responsible for the bulk of traffic within the pcap.

![img](https://i.ibb.co/mV9MVBwF/5519554a8faa0b60f88614789a4b9f67.png)

Utilizing the NBNS protocol, we can filter to find more information about the infected host, such as the MAC address (00:21:5d:c8:0e:f2) and host name (DESKTOP-ES9F3ML).

![img](https://i.ibb.co/8LBQh4gz/NBNS-MAC-Host.png)

Since this incident involves AD, we can filter for Kerberos CNameString. This reveals the user "gwyatt" on the infected machine.

![img](https://i.ibb.co/QFBhQsV8/CName-Str-1.png)

Utilizing the Find Packet function, we can enter "Wyatt" and search until we find a SAMR protocol packet, revealing the user's full identity, "Gabriel Wyatt".

![img](https://i.ibb.co/JWZKXQ8V/Full-Name.png)

Pivoting back to a simple filter for the malicious IP, we can see a TLSv1.3 connection to the domain whitepepper[.]su.

![img](https://i.ibb.co/6fRZhS8/Mal-Domain.png)

From here, I consulted the malware-traffic-analysis documentation and learned there are 2 other suspicious domains involved with the Lumma Stealer whitepepper[.]su domain.

![img](https://i.ibb.co/HTH09Gtw/Domains-2.png)

