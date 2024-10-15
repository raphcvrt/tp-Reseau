# TP5 : Un ptit LAN à nous

# I. Setup

- ```
  [root@routeur ~]# ip a
  2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
      link/ether 08:00:27:70:21:d1 brd ff:ff:ff:ff:ff:ff
      inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s3
         valid_lft forever preferred_lft forever
      inet6 fe80::a00:27ff:fe70:21d1/64 scope link
         valid_lft forever preferred_lft forever
  ```

  ```
  [root@routeur ~]# hostname
  routeur.tp5.b1
  ```

  ```
  paph@client1:~$ ip a
  2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
      link/ether 08:00:27:70:89:a2 brd ff:ff:ff:ff:ff:ff
      inet 10.5.1.11/24 brd 10.5.1.255 scope global enp0s3
         valid_lft forever preferred_lft forever
  ```

  ```
  paph@client1:~$ hostname
  client1.tp5.b1
  ```

  ```
  paph@client2:~$ ip a
  2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
      link/ether 08:00:27:70:89:a2 brd ff:ff:ff:ff:ff:ff
      inet 10.5.1.12/24 brd 10.5.1.255 scope global enp0s3
         valid_lft forever preferred_lft forever
  ```

  ```
  paph@client2:~$ hostname
  client2.tp5.b1
  ```

  ```
  PS C:\Windows\System32> ping 10.5.1.254

  Envoi d’une requête 'Ping'  10.5.1.254 avec 32 octets de données :
  Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64

  Statistiques Ping pour 10.5.1.254:
      Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
  Durée approximative des boucles en millisecondes :
      Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
  PS C:\Windows\System32> ping 10.5.1.12

  Envoi d’une requête 'Ping'  10.5.1.12 avec 32 octets de données :
  Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64

  Statistiques Ping pour 10.5.1.12:
      Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
  Durée approximative des boucles en millisecondes :
      Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
  PS C:\Windows\System32> ping 10.5.1.11

  Envoi d’une requête 'Ping'  10.5.1.11 avec 32 octets de données :
  Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
  Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64

  Statistiques Ping pour 10.5.1.11:
      Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
  Durée approximative des boucles en millisecondes :
      Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
  ```

# II. Accès internet pour tous

## 1. Accès internet routeur

```
[root@routeur ~]# ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=47 time=30.3 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=47 time=56.3 ms
...
```

```
[root@routeur ~]# sudo firewall-cmd --add-masquerade --permanent
success
[root@routeur ~]# sudo firewall-cmd --reload
success
```

## 2. Accès internet clients

```
paph@client2:~$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=46 time=47.0 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=46 time=77.2 ms
```

```
paph@client1:/etc/netplan$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=46 time=40.0 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=46 time=42.2 ms
```

```
paph@client1:/etc/netplan$ sudo cat /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [10.5.1.11/24]
      gateway4: 10.5.1.254
      nameservers:
        addresses: [1.1.1.1]
```

# III. Serveur SSH

```
[root@routeur ~]# sudo ss -lnpt | grep 22
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=747,fd=3))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=747,fd=4))
```

```
[root@routeur ~]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports:
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

```

```
[root@routeur ~]# cat /etc/services | grep ssh
ssh             22/tcp                          # The Secure Shell (SSH) Protocol
```

# IV. Serveur DHCP

## 3. Rendu attendu

### A. Installation et configuration du serveur DHCP

```
[root@routeur ~]# dnf -y install dhcp-server
[root@routeur ~]# sudo nano /etc/dhcp/dhcpd.conf
```

```
option domain-name-servers     routeur.tp5.b1.srv.world;
subnet 10.5.1.0 netmask 255.255.255.0 {
    range dynamic-bootp 10.5.1.137 10.5.1.237;
    option broadcast-address 10.0.0.255;
    option routers 10.5.1.254;
    option domain-name-servers 1.1.1.1;
}
```


### B. Test avec un nouveau client

```
paph@paph:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:70:89:a2 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s3
       valid_lft 486sec preferred_lft 486sec
    inet6 fe80::a00:27ff:fe70:89a2/64 scope link 
       valid_lft forever preferred_lft forever
paph@paph:~/Desktop$ ip r s 
default via 10.5.1.254 dev enp0s3 proto dhcp src 10.5.1.137 metric 100 
10.5.1.0/24 dev enp0s3 proto kernel scope link src 10.5.1.137 metric 100 
paph@paph:~/Desktop$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 1.1.1.1
       DNS Servers: 1.1.1.1
```

### C. Consulter le bail DHCP

```
[root@routeur ~]# cd /var/lib/dhcpd
[root@routeur dhcpd]# ls
dhcpd6.leases  dhcpd.leases  dhcpd.leases~
[root@routeur dhcpd]# cat dhcpd.leases
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

lease 10.5.1.137 {
  starts 2 2024/10/15 15:03:32;
  ends 2 2024/10/15 15:13:32;
  tstp 2 2024/10/15 15:13:32;
  cltt 2 2024/10/15 15:03:32;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:70:89:a2;
  uid "\001\010\000'p\211\242";
  client-hostname "paph";
}
```

```
paph@paph:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:70:89:a2 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s3
       valid_lft 520sec preferred_lft 520sec
    inet6 fe80::a00:27ff:fe70:89a2/64 scope link 
       valid_lft forever preferred_lft forever

```
