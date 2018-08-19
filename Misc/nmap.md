# nmap

## Host discovery

### -sL (List Scan)

The idea is to simply list the hosts to scan. Therefore this option is a degenerate form of host discovery.

### -sn (no port scan)

This option tells nmap not to scan ports after host discovery

This host discovery makes use of:
* ICMP echo request
* TCP SYN to port 443
* TCP ACK to port 80
* ICMP timestamp request

In previous releases -sn was known as -sP

### -Pn (no ping)

This option treats the IP as if it were up, regardless of a response to ping

### -PS <port list> (TCP SYN Ping)

It sends an empty TCP packet with the SYN flag set.

Example: -PS22-25,80 (there can be no space between -PS and the port list)

### -PA <port list> (TCP ACK Ping)

Exactly the same as above but with the ACK flag up.

The reason for offering both SYN and ACK probes is to maximize the chances of bypassing firewalls.
It is common for firewalls to block incoming SYN packets except for those destined to public services.

### -PU <port list> (UDP Ping)

It sends a UDP packet to the given port.

### -PY <port list> (SCTP INIT Ping)

This option sends an SCTP packet containing a minimal INIT chunk.

### -PE, -PP, -PM (ICMP Ping Types)

Nmap can send the standard packets sent by ping

### -PO <port list> (Protocol Ping)

Nmap sends IP packets with the specified protocol number set in their IP header.

### -PR (ARP Ping)

ARP scan puts nmap in charge of ARP requests. If a response is received nmap does not even need to worry about the IP based ping packets since it already knows that the host is up.

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

