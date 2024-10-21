```
paph@client2:~$ sudo cat icmpscapy.py
from scapy.all import *

ping = ICMP(type=8)

packet = IP(src="10.6.1.37", dst="10.6.1.1")

frame = Ether(src="08:00:27:9e:4a:b0", dst="0a:00:27:00:00:4c")

final_frame = frame/packet/ping

answers, unanswered_packets = srp(final_frame, timeout=10)

print(f"Pong reçu : {answers[0]}")

paph@client2:~$ sudo python3 icmpscapy.py
Begin emission:
Finished sending 1 packets.
*
Received 1 packets, got 1 answers, remaining 0 packets
Pong reçu : QueryAnswer(query=<Ether  dst=0a:00:27:00:00:4c src=08:00:27:9e:4a:b0 type=IPv4 |<IP  frag=0 proto=icmp src=10.6.1.37 dst=10.6.1.1 |<ICMP  type=echo-request |>>>, answer=<Ether  dst=08:00:27:9e:4a:b0 src=0a:00:27:00:00:4c type=IPv4 |<IP  version=4 ihl=5 tos=0x0 len=28 id=55666 flags= frag=0 ttl=128 proto=icmp chksum=0x4b3d src=10.6.1.1 dst=10.6.1.37 |<ICMP  type=echo-reply code=0 chksum=0xffff id=0x0 seq=0x0 |<Padding  load='\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00' |>>>>)
```

port pour les requetes dns : 53

```
paph@client2:~$ sudo tcpdump -i enp0s3 port 53
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on enp0s3, link-type EN10MB (Ethernet), snapshot length 262144 bytes
22:10:55.309874 IP client2.tp6.b1.54101 > dns.tp6.b1.domain: 34694+ [1au] A? client2.tp6.b1. (43)
22:10:55.310291 IP client2.tp6.b1.37557 > dns.tp6.b1.domain: 4860+ [1au] AAAA? client2.tp6.b1. (43)
22:10:55.311497 IP dns.tp6.b1.domain > client2.tp6.b1.37557: 4860 NXDomain* 0/1/1 (89)
22:10:55.311497 IP dns.tp6.b1.domain > client2.tp6.b1.54101: 34694 NXDomain* 0/1/1 (89)
22:10:55.338217 IP client2.tp6.b1.47093 > dns.tp6.b1.domain: 30610+ [1au] PTR? 12.2.6.10.in-addr.arpa. (51)
22:10:55.339496 IP dns.tp6.b1.domain > client2.tp6.b1.47093: 30610* 1/0/1 PTR dns.tp6.b1. (75)
22:10:55.340374 IP client2.tp6.b1.49036 > dns.tp6.b1.domain: 15540+ [1au] PTR? 37.1.6.10.in-addr.arpa. (51)
22:10:55.341821 IP dns.tp6.b1.domain > client2.tp6.b1.49036: 15540 NXDomain* 0/1/1 (101)
22:10:55.946362 IP client2.tp6.b1.28044 > dns.tp6.b1.domain: 0+ A? thinkerview.com. (33)
22:10:55.947345 IP dns.tp6.b1.domain > client2.tp6.b1.28044: 0 2/0/0 A 188.114.96.2, A 188.114.97.2 (65)
```

je copie-colle deux lignes de [ce site ](https://scapy.readthedocs.io/en/latest/usage.html#dns-requests)dans DNS request (et je met mes parametres)

```
paph@client2:~$ sudo cat dns_request.py
from scapy.all import *

ans = sr1(IP(dst="10.6.2.12")/UDP(sport=RandShort(), dport=53)/DNS(rd=1,qd=DNSQR(qname="thinkerview.com",qtype="A")))

print(f"l'ip correspondant a thinkerview.com est : {ans.an[0].rdata}")

paph@client2:~$ sudo python3 dns_request.py
Begin emission:
Finished sending 1 packets.
....*
Received 5 packets, got 1 answers, remaining 0 packets
l'ip correspondant a thinkerview.com est : 188.114.96.2
```
