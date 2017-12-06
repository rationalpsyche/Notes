## Scan types

### -sS TCP SYN

You send a SYN packet, a SYN/ACK indicates the port is *open* while a RST indicates it is *closed*.
If no response is received after several retransmissions then the port is marked as *filtered*

### -sT TCP connect

This is the default TCP scan when SYN scan is not an option (i.e. you do not have root privileges).

The previous technique is better in terms of performance and stealthiness.

### -sU UDP scan

DNS, SNMP and DHCP are the most common services runnig over UDP.

If an ICMP port unreachable error is returned the port is *closed*.
Other ICMP unreachable errors mark the port as *filtered*.
Occasionally a service will respond with a UDP packet, proving that it is *open*

### -sY SCTP init scan

SCTP INIT scan is the SCTP equivalent of a TCP SYN scan. 
You send an INIT chunk and then wait for a response. An INIT-ACK chunk indicates the port is *open*, while an ABORT chunk is indicative of a *closed* port. If no response is received after several retransmissions, the port is marked as *filtered*.

### -sN, -sF, -sX (NULL, FIN Xmas scan)

The key advantage to these scan types is that they can sneak through certain non-stateful firewalls and packet filtering routers.

### -sA TCP ACK

This scan does not determine open ports. It is used to map out firewall rulesets, determining whether they are stateful or not and which ports are filtered.

### -sW Window scan

It is exactly like the ACK scan but it exploits an implementation detail of certain systems.

### -sM Maimon scan

It is similar to NULL,FIN,Xmas scan except for the probe.

