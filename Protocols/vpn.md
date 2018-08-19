# VPN

## The AH and ESP protocols

In the IPSec protocol there are two principal protocols: the Authentication Header (AH) and the Encapsulation Security Payload (ESP).

| | AH | ESP |
| --- | --- | --- |
| Source authentication | + | + |
| Data integrity | + | + |
| Confidentiality | - | + |

## Security associations

Before sending IPSec datagrams the source and destination create a network layer logical connection called *security association* (SA).

It is undirectional (hence two SA are required for a bidrectional communication).

The information about the SA includes:

* A 32 bit identifier called the Security Parameter Index (SPI)
* The origin and destination interface
* The encryption key
* The type of integrity check (HMAC with MD5)
* The authentication key

An IPSec entity stores the state information for all of its SAs in its Security Association Database (SAD) which is a data structure in the entity's OS kernel.

## The IPSec Datagram

IPSec have two different packet forms: **tunnel-mode** and **transport mode**.

We focus only on tunnel mode.

```
		      +-------------- "Enchilada" authenticated -------------------------------------+
                           +-----------------------------Encrypted---------------------------+
New IP header | ESP Header | Original IP Header | Original IP Datagram payload | ESP Trailer | ESP MAC
					|                                                               |
					V                                                               V
			   [SPI || Seq #]                                [Padding || Padding length || Next header]

```

The source and destination IP addresses that are in the new IP header are the ones of the source and destionation router interfaces at the two ends of the tunnel.

The protocol number is set to 50, designating that this is an IPSec datagram using the ESP protocol.


