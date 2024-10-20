# TP6 : Des bo services dans des bo LANs

# I. Le setup

```
[root@dhcp ~]# ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=53 time=18.7 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=53 time=20.6 ms
```

```
[root@dns ~]# ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=53 time=19.8 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=53 time=20.6 ms
```

```
[root@dhcp ~]# ping 10.6.2.12
PING 10.6.2.12 (10.6.2.12) 56(84) bytes of data.
64 bytes from 10.6.2.12: icmp_seq=1 ttl=63 time=1.04 ms
64 bytes from 10.6.2.12: icmp_seq=2 ttl=63 time=2.23 ms
```

## II. LAN clients

## 2. Client

```
paph@client1:~/Desktop$ ip a
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:6b:24:04 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s3
       valid_lft 435sec preferred_lft 435sec
    inet6 fe80::a00:27ff:fe6b:2404/64 scope link 
       valid_lft forever preferred_lft forever
```

```
paph@client1:~/Desktop$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 1.1.1.1
       DNS Servers: 1.1.1.1
```

```
paph@client1:~/Desktop$ ip r s
default via 10.6.1.254 dev enp0s3 proto dhcp src 10.6.1.37 metric 100 
1.1.1.1 via 10.6.1.254 dev enp0s3 proto dhcp src 10.6.1.37 metric 100 
10.6.1.0/24 dev enp0s3 proto kernel scope link src 10.6.1.37 metric 100 
10.6.1.254 dev enp0s3 proto dhcp scope link src 10.6.1.37 metric 100 
```

```
paph@client1:~/Desktop$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=54 time=30.6 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=54 time=25.9 ms
```

# III. LAN serveurzzzz

## 1. Serveur Web

```
[root@web ~]# sudo ss -lntp | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1647,fd=6),("nginx",pid=1646,fd=6),("nginx",pid=1645,fd=6),("nginx",pid=1644,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1647,fd=7),("nginx",pid=1646,fd=7),("nginx",pid=1645,fd=7),("nginx",pid=1644,fd=7))
[root@web ~]# sudo firewall-cmd --permanent --add-port=80/tcp
success
[root@web ~]# sudo firewall-cmd --reload
success
```

```
paph@client1:~/Desktop$ curl http://10.6.2.11
<!doctype html>
<html>
  <head>

```

## 2. Serveur DNS

```
[root@dns ~]# sudo ss -lnpu |grep 53
UNCONN 0      0          10.6.2.12:53        0.0.0.0:*    users:(("named",pid=1959,fd=52))
UNCONN 0      0          10.6.2.12:53        0.0.0.0:*    users:(("named",pid=1959,fd=53))
UNCONN 0      0          10.6.2.12:53        0.0.0.0:*    users:(("named",pid=1959,fd=54))
UNCONN 0      0          127.0.0.1:53        0.0.0.0:*    users:(("named",pid=1959,fd=44))
UNCONN 0      0          127.0.0.1:53        0.0.0.0:*    users:(("named",pid=1959,fd=43))
UNCONN 0      0          127.0.0.1:53        0.0.0.0:*    users:(("named",pid=1959,fd=45))
UNCONN 0      0              [::1]:53           [::]:*    users:(("named",pid=1959,fd=58))
UNCONN 0      0              [::1]:53           [::]:*    users:(("named",pid=1959,fd=60))
UNCONN 0      0              [::1]:53           [::]:*    users:(("named",pid=1959,fd=59))
[root@dns ~]# sudo ss -lnpt |grep 53
LISTEN 0      10         10.6.2.12:53        0.0.0.0:*    users:(("named",pid=1959,fd=56))
LISTEN 0      10         10.6.2.12:53        0.0.0.0:*    users:(("named",pid=1959,fd=57))
LISTEN 0      10         10.6.2.12:53        0.0.0.0:*    users:(("named",pid=1959,fd=55))
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=1959,fd=47))
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=1959,fd=46))
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=1959,fd=48))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=1959,fd=61))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=1959,fd=63))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=1959,fd=62))
```

```
[root@dns ~]# sudo firewall-cmd --permanent --add-port=53/tcp
success
[root@dns ~]# sudo firewall-cmd --permanent --add-port=53/udp
success
[root@dns ~]# sudo firewall-cmd --reload
success
```

( j'ai mis que la section reponse )

```
[root@dns ~]# dig web.tp6.b1 @10.6.2.12

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 1 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Sun Oct 20 13:46:42 CEST 2024
;; MSG SIZE  rcvd: 83

[root@dns ~]# dig dns.tp6.b1 @10.6.2.12

;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.2.12

;; Query time: 1 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Sun Oct 20 13:48:37 CEST 2024
;; MSG SIZE  rcvd: 83

[root@dns ~]# dig ynov.com @10.6.2.12
;; ANSWER SECTION:
ynov.com.               300     IN      A       104.26.10.233
ynov.com.               300     IN      A       172.67.74.226
ynov.com.               300     IN      A       104.26.11.233

;; Query time: 659 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Sun Oct 20 13:50:48 CEST 2024
;; MSG SIZE  rcvd: 113

[root@dns ~]# dig -x 10.6.2.11 @10.6.2.12

;; ANSWER SECTION:
11.2.6.10.in-addr.arpa. 86400   IN      PTR     web.tp6.b1.

;; Query time: 2 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Sun Oct 20 13:53:16 CEST 2024
;; MSG SIZE  rcvd: 103

[root@dns ~]# dig -x 10.6.2.12 @10.6.2.12

;; ANSWER SECTION:
12.2.6.10.in-addr.arpa. 86400   IN      PTR     dns.tp6.b1.

;; Query time: 1 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Sun Oct 20 13:53:30 CEST 2024
;; MSG SIZE  rcvd: 103

```

```
paph@client1:~$ dig web.tp6.b1 @10.6.2.12

;; ANSWER SECTION:
web.tp6.b1.		86400	IN	A	10.6.2.11

;; Query time: 1 msec
;; SERVER: 10.6.2.12#53(10.6.2.12) (UDP)
;; WHEN: Sun Oct 20 13:57:20 CEST 2024
;; MSG SIZE  rcvd: 83

```

## 3. Serveur DHCP

```
paph@client2:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:9e:4a:b0 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s3
       valid_lft 553sec preferred_lft 553sec
    inet6 fe80::a00:27ff:fe9e:4ab0/64 scope link 
       valid_lft forever preferred_lft forever
paph@client2:~/Desktop$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
       DNS Servers: 10.6.2.12
```

```
paph@client2:~/Desktop$ curl http://web.tp6.b1
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
```
