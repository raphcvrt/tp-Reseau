# TP7 : On dit chiffrer pas crypter

# II. Serveur Web

```
[root@web ~]# sudo ss -lnpt | grep '80'
State  Recv-Q Send-Q   Local Address:Port   Peer Address:Port Process
LISTEN 0      511            0.0.0.0:80          0.0.0.0:*     users:(("nginx",pid=816,fd=6),("nginx",pid=815,fd=6))
```

```
[root@web ~]# sudo firewall-cmd --permanent --add-port=80/tcp
success
```

```
paph@client1:~$ ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=0.533 ms
```

```
paph@client1:~$ curl http://sitedefou.tp7.b1
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
```

La capture des connexions TCP avec ss n'a pas fonctionné a cause de la fermeture rapide des connexions : curl ferme les connexions trop vite donc le ss n'enregistre que mon ssh au port 22 et pas le http du port 80. J'ai une VM sans interface pour client1 donc je ne peux pas ouvrir de navigateur

```
[root@web ~]# ss -tuln | grep ':443'
tcp   LISTEN 0      511        10.7.1.11:443       0.0.0.0:*
[root@web ~]# sudo firewall-cmd --permanent --add-port=443/tcp
success
[root@web ~]# sudo firewall-cmd --permanent --remove-port=80/tcp
success
[root@web ~]# sudo firewall-cmd --reload
```

```
paph@client1:~$ curl https://sitedefou.tp7.b1
<!doctype html>
<html>
  <head>
```

j'ai enlevé le meow! a un moment je sais plus pourquoi désolé

# III. Serveur VPN

```
[paph@vpn ~]$ ip a
4: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
[paph@vpn ~]$ sudo ss -tuln
Netid      State       Recv-Q      Send-Q           Local Address:Port              Peer Address:Port      Process
udp        UNCONN      0           0                      0.0.0.0:51820                  0.0.0.0:*
[paph@vpn ~]$ sudo firewall-cmd --permanent --add-port=51820/udp
success
[paph@vpn ~]$ sudo firewall-cmd --permanent --add-port=323/udp
success
```

```
paph@client1:~$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=0.695 ms
```
