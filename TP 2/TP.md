
1. **Simplest LAN**

```
PS C:\Windows\System32> Get-NetIPAddress -InterfaceAlias "Ethernet"

IPAddress         : fe80::f17:1113:dcc7:3e5c%11
InterfaceIndex    : 11
InterfaceAlias    : Ethernet
AddressFamily     : IPv6
Type              : Unicast
PrefixLength      : 64
PrefixOrigin      : WellKnown
SuffixOrigin      : Link
AddressState      : Preferred
ValidLifetime     : Infinite ([TimeSpan]::MaxValue)
PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
SkipAsSource      : False
PolicyStore       : ActiveStore

IPAddress         : 10.67.69.133
InterfaceIndex    : 11
InterfaceAlias    : Ethernet
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 24
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Preferred
ValidLifetime     : Infinite ([TimeSpan]::MaxValue)
PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
SkipAsSource      : False
PolicyStore       : ActiveStore
```

```
PS C:\Windows\System32> ping 10.67.69.132

Envoi d’une requête 'Ping'  10.67.69.132 avec 32 octets de données :
Réponse de 10.67.69.132 : octets=32 temps=3 ms TTL=128
Réponse de 10.67.69.132 : octets=32 temps=2 ms TTL=128
Réponse de 10.67.69.132 : octets=32 temps=3 ms TTL=128
Réponse de 10.67.69.132 : octets=32 temps=2 ms TTL=128

Statistiques Ping pour 10.67.69.132:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 2ms, Maximum = 3ms, Moyenne = 2ms
```

voir ping advm.pcap

2. **Utilisation des ports** 

***(je suis le pc client)***

```
PS C:\Users\rapha\Downloads\netcat-1.11> .\nc.exe 10.67.69.232 9999
testtest


ete

f
ef
fe
fe


dfdfd

df
df
coucou ca va
cv bien et twa
jkiff les chats smr

```

```
PS C:\Users\rapha\Downloads\netcat-1.11> netstat -a -n -b

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    10.33.70.238:9999      10.33.68.254:29873     ESTABLISHED
```

***(je deviens pc server)***

```
PS C:\Users\rapha\Downloads\netcat-1.11> netstat -b -a

Connexions actives

  TCP    0.0.0.0:9999           LAPTOP-MMJBVRQM:0      LISTENING
 [nc64.exe]
```

```
PS C:\Users\rapha\Downloads\netcat-1.11> ./nc64.exe -l -p 9999
parle moi
coucou
```

```
PS C:\Users\rapha\Downloads\netcat-1.11> netstat -b -n

Connexions actives

  TCP    10.67.69.133:9999      10.67.69.132:27021     ESTABLISHED
 [nc64.exe]
```

voir netcat 2.pcap

voir http.pcap

b. liste des apps :

- outlook
  - ```
     [Discord.exe]
      TCP    10.33.68.254:52831     20.199.120.151:443     ESTABLISHED
    ```
- discord
  - ```
    [OUTLOOK.EXE]
      TCP    10.33.68.254:17029     52.98.243.146:443      ESTABLISHED
    ```
- riot games
  - ```
     [RiotClientServices.exe]
      TCP    10.33.68.254:16801     104.16.55.40:443       ESTABLISHED
    ```
- opera gx
  - ```
     [opera.exe]
      TCP    10.33.68.254:17024     20.189.173.27:443      ESTABLISHED
    ```
- ubisoft connect
  - ```
     [UplayWebCore.exe]
      TCP    10.33.68.254:17083      185.70.42.22:7680       SYN_SENT
    ```

voir les fichiers associés
