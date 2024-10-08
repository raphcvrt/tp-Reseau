# I. ARP basics

**9C:B6:D0:05:18:DB**

- ```
  PS C:\Windows\System32> ipconfig /all

  Carte réseau sans fil Wi-Fi :

     Suffixe DNS propre à la connexion. . . :
     Description. . . . . . . . . . . . . . : Killer Wireless-n|a|ac 1535 Wireless Network Adapter
     Adresse physique . . . . . . . . . . . : 9C-B6-D0-05-18-DB
     DHCP activé. . . . . . . . . . . . . . : Oui
     Configuration automatique activée. . . : Oui
     Adresse IPv6 de liaison locale. . . . .: fe80::dd8b:8b07:adba:11be%20(préféré)
     Adresse IPv4. . . . . . . . . . . . . .: 10.33.68.254(préféré)
     Masque de sous-réseau. . . . . . . . . : 255.255.240.0
     Bail obtenu. . . . . . . . . . . . . . : mardi 8 octobre 2024 15:06:33
     Bail expirant. . . . . . . . . . . . . : mercredi 9 octobre 2024 13:56:20
     Passerelle par défaut. . . . . . . . . : 10.33.79.254
     Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
     IAID DHCPv6 . . . . . . . . . . . : 178042576
     DUID de client DHCPv6. . . . . . . . : 00-01-00-01-1D-ED-58-07-DC-FE-07-2E-9B-86
     Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                         1.1.1.1
     NetBIOS sur Tcpip. . . . . . . . . . . : Activé
  ```
- ```
  PS C:\Windows\System32> arp -a

  Interface : 192.168.56.1 --- 0x5
    Adresse Internet      Adresse physique      Type
    192.168.56.255        ff-ff-ff-ff-ff-ff     statique
    224.0.0.22            01-00-5e-00-00-16     statique
    224.0.0.251           01-00-5e-00-00-fb     statique
    224.0.0.252           01-00-5e-00-00-fc     statique
    230.0.0.1             01-00-5e-00-00-01     statique
    239.255.255.250       01-00-5e-7f-ff-fa     statique

  Interface : 10.33.68.254 --- 0x14
    Adresse Internet      Adresse physique      Type
    10.33.65.8            34-7d-f6-5a-20-da     dynamique
    10.33.65.32           08-71-90-c7-c7-7a     dynamique
    10.33.65.63           44-af-28-c3-6a-9f     dynamique
    10.33.70.42           9c-fc-e8-42-f1-7b     dynamique
    10.33.74.153          48-e7-da-f0-f6-6d     dynamique
    10.33.77.32           4c-5f-70-cf-7a-ab     dynamique
    10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
    10.33.79.255          ff-ff-ff-ff-ff-ff     statique
    224.0.0.22            01-00-5e-00-00-16     statique
    224.0.0.251           01-00-5e-00-00-fb     statique
    239.255.255.250       01-00-5e-7f-ff-fa     statique
    255.255.255.255       ff-ff-ff-ff-ff-ff     statique
  ```

Passerelle : 10.33.79.254

```
 PS C:\Windows\System32> arp -a

Interface : 192.168.56.1 --- 0x5
  Adresse Internet      Adresse physique      Type
10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
```

```
PS C:\Windows\System32> arp -a

Interface : 192.168.56.1 --- 0x5
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 10.33.68.254 --- 0x14
  Adresse Internet      Adresse physique      Type
  10.33.65.8            34-7d-f6-5a-20-da     dynamique
  10.33.65.32           08-71-90-c7-c7-7a     dynamique
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.70.42           9c-fc-e8-42-f1-7b     dynamique
  10.33.74.153          48-e7-da-f0-f6-6d     dynamique
  10.33.77.32           4c-5f-70-cf-7a-ab     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

```
PS C:\Windows\System32> arp -d 10.33.79.254
PS C:\Windows\System32> arp -a

Interface : 192.168.56.1 --- 0x5
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 10.33.68.254 --- 0x14
  Adresse Internet      Adresse physique      Type
  10.33.65.8            34-7d-f6-5a-20-da     dynamique
  10.33.65.13           08-8e-90-06-a2-7a     dynamique
  10.33.65.18           34-c9-3d-e4-52-69     dynamique
  10.33.65.32           08-71-90-c7-c7-7a     dynamique
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.69.17           d4-54-8b-d7-d6-88     dynamique
  10.33.70.42           9c-fc-e8-42-f1-7b     dynamique
  10.33.70.248          b8-9a-2a-0e-c2-5c     dynamique
  10.33.74.153          48-e7-da-f0-f6-6d     dynamique
  10.33.77.32           4c-5f-70-cf-7a-ab     dynamique
  10.33.77.198          de-ed-f5-cd-9e-c6     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

☀️ **Wireshark**

- voir capture  `arp1.pcap`

# II. ARP dans un réseau local

## 1. Basics

- ```
     Description. . . . . . . . . . . . . . : Killer Wireless-n|a|ac 1535 Wireless Network Adapter
  ```
- ```
  Passerelle par défaut. . . . . . . . . : fe80::fcaa:81ff:fe5d:f164%20
  172.20.10.1
  ```
- ```
    172.20.10.1           fe-aa-81-5d-f1-64     dynamique
  ```
- ipconfig avant la modification d'ip
- ```
  PS C:\Windows\System32> ipconfig /all
     Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.8(préféré)
  ```
- ipconfig apres

  ```
  PS C:\Windows\System32> ipconfig /all
     Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.6(préféré)
  ```

Ping de Adam Benaissa:

```
PS C:\Windows\System32> ping 172.20.10.4

Envoi d’une requête 'Ping'  172.20.10.4 avec 32 octets de données :
Réponse de 172.20.10.4 : octets=32 temps=9 ms TTL=128
Réponse de 172.20.10.4 : octets=32 temps=87 ms TTL=128
Réponse de 172.20.10.4 : octets=32 temps=102 ms TTL=128
Réponse de 172.20.10.4 : octets=32 temps=118 ms TTL=128

Statistiques Ping pour 172.20.10.4:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 9ms, Maximum = 118ms, Moyenne = 79ms
```

Ping de Adam Mebarki:

```
PS C:\Windows\System32> ping 172.20.10.3

Envoi d’une requête 'Ping'  172.20.10.3 avec 32 octets de données :
Réponse de 172.20.10.3 : octets=32 temps=105 ms TTL=128
Réponse de 172.20.10.3 : octets=32 temps=4 ms TTL=128
Réponse de 172.20.10.3 : octets=32 temps=5 ms TTL=128
Réponse de 172.20.10.3 : octets=32 temps=6 ms TTL=128

Statistiques Ping pour 172.20.10.3:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 4ms, Maximum = 105ms, Moyenne = 30ms
```

## 2. ARP

```
PS C:\Windows\System32> arp -a

Interface : 192.168.56.1 --- 0x5
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 172.20.10.6 --- 0x14
  Adresse Internet      Adresse physique      Type
  172.20.10.1           fe-aa-81-5d-f1-64     dynamique
  172.20.10.3           80-19-34-04-ba-b9     dynamique
  172.20.10.4           1c-ce-51-24-c7-33     dynamique
  172.20.10.15          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
```

```
PS C:\Windows\System32> arp -a -d
PS C:\Windows\System32> arp -a

Interface : 192.168.56.1 --- 0x5
  Adresse Internet      Adresse physique      Type
  224.0.0.22            01-00-5e-00-00-16     statique

Interface : 172.20.10.6 --- 0x14
  Adresse Internet      Adresse physique      Type
  224.0.0.22            01-00-5e-00-00-16     statique
```

## 3. Bonus : ARP poisoning

![ARP poisoning](./img/ARP_poisoning.svg)

> ⚠️⚠️⚠️ Si le partage de co n'a pas fonctionné, **il est hors de question que vous fassiez ça sur le réseau de l'école. Donc partage de co ou avec des VMs.**

⭐ **Empoisonner la table ARP de l'un des membres de votre réseau**

- il faut donc forcer l'injection de fausses informations dans la table ARP de quelqu'un d'autre
- on peut le faire en envoyant des messages ARP que l'on a forgé nous-mêmes
- avec quelques lignes de code, ou y'a déjà ce qu'il faut sur internet
- faites vos recherches, demandez-moi si vous voulez de l'aide
- affichez la table ARP de la victime une fois modifiée dans le compte-rendu

⭐ **Mettre en place un MITM**

- MITM pour Man-in-the-middle
- placez vous entre l'un des membres du réseau, et la passerelle
- ainsi, dès que ce PC va sur internet, c'est à vous qu'il envoie tous ses messages
- pour ça, il faut continuellement empoisonner la table ARP de la victime, et celle de la passerelle

> Au moins tous ceux veulent faire de la sécu, il faudrait faire cette partie bonus ! Prenez-vous un peu la tête pour le réaliser, avec des VMs y'aura ptet moins de trucs dans tous les sens pour une première fois. Hésitez pas à m'appeler.

![ARP sniff](./img/arp.jpg)
