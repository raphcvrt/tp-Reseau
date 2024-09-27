# RENDU TP1

### I. Récolte d'informations
```
PS C:\Users\rapha> ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::dd8b:8b07:adba:11be%20
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.171
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254

Carte Ethernet Ethernet 2 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::56bc:7942:72ab:15ff%5
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

```
```
PS C:\Users\rapha> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Killer Wireless-n|a|ac 1535 Wireless Network Adapter
   Adresse physique . . . . . . . . . . . : 9C-B6-D0-05-18-DB
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::dd8b:8b07:adba:11be%20(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.171(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Bail obtenu. . . . . . . . . . . . . . : vendredi 27 septembre 2024 13:02:14
   Bail expirant. . . . . . . . . . . . . : samedi 28 septembre 2024 13:02:15
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
   IAID DHCPv6 . . . . . . . . . . . : 178042576
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-1D-ED-58-07-DC-FE-07-2E-9B-86
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```
Bonus :
```
PS C:\Users\rapha> Get-Service -Name MpsSvc

Status   Name               DisplayName
------   ----               -----------
Running  MpsSvc             Pare-feu Windows Defender

```

### II. Utiliser le réseau

```
PS C:\Users\rapha> ping 10.33.77.171

Envoi d’une requête 'Ping'  10.33.77.171 avec 32 octets de données :
Réponse de 10.33.77.171 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.171 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.171 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.171 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.33.77.171:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

```
PS C:\Users\rapha> ping 127.0.0.1

Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 127.0.0.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
```
PS C:\Users\rapha> ping 10.33.79.254

Envoi d’une requête 'Ping'  10.33.79.254 avec 32 octets de données :
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.

Statistiques Ping pour 10.33.79.254:
    Paquets : envoyés = 4, reçus = 0, perdus = 4 (perte 100%),
```

```
PS C:\Windows\System32> ping 10.33.66.78

Envoi d’une requête 'Ping'  10.33.66.78 avec 32 octets de données :
Réponse de 10.33.66.78 : octets=32 temps=212 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=16 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=23 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=16 ms TTL=64

Statistiques Ping pour 10.33.66.78:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 16ms, Maximum = 212ms, Moyenne = 66ms
```
```
PS C:\Windows\System32> ping ynov.com

Envoi d’une requête 'ping' sur ynov.com [104.26.11.233] avec 32 octets de données :
Réponse de 104.26.11.233 : octets=32 temps=15 ms TTL=55
Réponse de 104.26.11.233 : octets=32 temps=18 ms TTL=55
Réponse de 104.26.11.233 : octets=32 temps=17 ms TTL=55
Réponse de 104.26.11.233 : octets=32 temps=16 ms TTL=55

Statistiques Ping pour 104.26.11.233:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 15ms, Maximum = 18ms, Moyenne = 16ms
```
```
PS C:\Windows\System32> nslookup www.torproject.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.torproject.org
Addresses:  2620:7:6002:0:466:39ff:fe7f:1826
          2a01:4f8:fff0:4f:266:37ff:feae:3bbc
          2620:7:6002:0:466:39ff:fe32:e3dd
          2a01:4f8:fff0:4f:266:37ff:fe2c:5d19
          2a01:4f9:c010:19eb::1
          204.8.99.144
          116.202.120.165
          116.202.120.166
          204.8.99.146
          95.216.163.36
```
```
PS C:\Windows\System32> nslookup www.thinkerview.com
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.thinkerview.com
Addresses:  2a06:98c1:3120::7
          2a06:98c1:3121::7
          188.114.97.7
          188.114.96.7
```

```
PS C:\Windows\System32> nslookup wikileaks.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    wikileaks.org
Addresses:  51.159.197.136
          80.81.248.21
```

### III. Sniffer le réseau

[ping.pcap](ping.pcapng)
[dns.pcap](dns.pcapng)