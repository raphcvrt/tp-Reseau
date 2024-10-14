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

➜ **Actuellement, tout le monde est connecté, mais les clients n'ont pas internet !**

![Conneted, no internet](./img/connected_no_internet.png)

➜ Dans cette partie, on va faire en sorte que tout le monde ait un accès internet :

- le routeur a déjà un accès internet
- les clients vont se servir du routeur comme passerelle afin d'accéder à internet

Pour ça :

- il faut que notre machine `routeur.tp5.b1` accepte de router des paquets
- il faut que chaque client
  - connaisse `routeur.tp.b1` comme sa passerelle (`10.5.1.254`)
  - connaisse l'adresse d'un serveur DNS (pour résoudre des noms comme `www.ynov.com` afin de connaître l'adresse IP associée à ce nom)

> Si l'un de ces points n'est pas correctement configuré, on est bien "connectés" (genre y'a un LAN, tout le monde se `ping`) mais sans "accès internet".

## 1. Accès internet routeur

> *Cette section 1. est à réaliser sur `routeur.tp5.b1`.*

☀️ **Déjà, prouvez que le routeur a un accès internet**

- une seule commande `ping` suffit à prouver ça, vers un nom de domaine que vous connaissez, genre `www.ynov.com` (ou autre de votre choix :d)

☀️ **Activez le routage**

- toujours sur `routeur.tp5.b1`
- la commande est dans le mémo toujours !

> Tout est normalement déjà setup avec la carte NAT ! Si vous n'avez pas internet, c'est que votre carte NAT est éteinte. Allumez-la !

## 2. Accès internet clients

> *Cette section 2. est à réaliser sur `client1.tp5.b1` et `client2.tp5.b1`. Tout est dans [le mémo réseau Ubuntu](../../cours/memo/ubuntu.md).*

➜ **Définir l'adresse IP du routeur comme passerelle pour les clients**

- il sera peut-être nécessaire de redémarrer l'interface réseau pour que ça prenne effet

➜ **Vérifier que les clients ont un accès internet**

- avec un `ping` vers une adresse IP publique vous connaissez
- à ce stade, vos clients ne peuvent toujours pas résoudre des noms, donc impossible de visiter un site comme `www.ynov.com`

➜ **Définir `1.1.1.1` comme serveur DNS que peuvent utiliser les clients**

- redémarrez l'interface réseau si nécessaire pour que ça prenne effet
- ainsi vos clients pourront spontanément envoyer des requêtes DNS vers `1.1.1.1` afin d'apprendre à quelle IP correspond un nom de domaine donné

> *`1.1.1.1` c'est l'adresse IP publique d'un serveur DNS d'une entreprise qui s'appelle CloudFlare (un gros acteur du Web). Ils hébergent gracieusement et publiquement ce serveur DNS, afin que n'importe qui puisse l'utiliser.*

☀️ **Prouvez que les clients ont un accès internet**

- avec de la résolution de noms cette fois
- une seule commande `ping` suffit

☀️ **Montrez-moi le contenu final du fichier de configuration de l'interface réseau**

- celui de `client2.tp5.b1` me suffira
- pour le compte-rendu, une simple commande `cat` pour afficher le contenu du fichier

> *Vous devriez pouvoir ouvrir un navigateur et visiter des sites sans soucis sur les clients.*

# III. Serveur SSH

> *Cette partie III. est à réaliser sur `routeur.tp5.b1`. Tout est dans [le mémo réseau Rocky](../../cours/memo/rocky.md).*

☀️ **Sur `routeur.tp5.b1`, déterminer sur quel port écoute le serveur SSH**

- pour le serveur SSH, le nom du programme c'est `sshd`
  - il écoute sur un port TCP
- dans le compte rendu je veux que vous utilisiez une syntaxe avec `... | grep <PORT>` pour isoler la ligne avec le port intéressant
  - par exemple si, vous repérez le port 8888, vous ajoutez ` | grep 8888` à votre commande, pour me mettre en évidence le por que vous avez repéré

☀️ **Sur `routeur.tp5.b1`, vérifier que ce port est bien ouvert**

- la commande est dans [le mémooooo](../../cours/memo/rocky.md) pour voir la configuration du pare-feu

> ***Si vous voyez le "service" `ssh` ouvert dans le pare-feu**, il correspond à un port bien précis. Pour voir la correspondance entre les "services" et le port associé, vous pouvez consulter le contenu du fichier `/etc/services`. Ca devrait correspondre à ce que vous avez vu juste avant !*

➜ Dernière fois que je le dis : **connectez-vous en SSH pour administrer la machine Rocky Linux**, n'utilisez pas l'interface console de VirtualBox.

# IV. Serveur DHCP

## 1. Le but

➜ On installe et configure **notre propre serveur DHCP** dans cette partie ! Le but est le suivant :

- **dès qu'un client se connecte à notre réseau, il a automatiquement internet !**
- ça **évite de faire à la main** comme vous avez fait dans ce TP :
  - choisir et configurer une adresse IP
  - choisir et configurer l'adresse d'un serveur DNS
  - configurer l'adresse de la passerelle
- **dès qu'il se connecte, il essaiera automatiquement de contacter un serveur DHCP**
- **notre serveur DHCP lui proposera alors automatiquement tout le nécessaire pour avoir un accès internet**, à savoir :
  - une adresse IP disponible
  - l'adresse d'un serveur DNS
  - l'adresse de la passerelle du réseau

![DHCP server](./img/dhcp.png)

## 2. Comment le faire

> Cette fois, je vous ré-écris pas tout, je vous laisse chercher sur internet par vous-mêmes "install dhcp server rocky 9", ou vous référer [par exemple à ce lien](https://www.server-world.info/en/note?os=Rocky_Linux_8&p=dhcp&f=1) qui résume très bien la chose.

➜ Peu importe le lien que vous suivez, **les étapes seront les suivantes** :

- installation du paquet qui contient le serveur DHCP
  - commande `dnf install`
- modification de la configuration
  - c'est un fichier texte (comme toujours)
  - donc avec `nano` ou `vim` par exemple
- (re)démarrage du service DHCP
  - avec un `systemctl start`

➜ **Et si ça fonctionne pas, c'est que tu t'es planté dans le fichier de conf, donc tu vas lire pourquoi dans les logs** :

- voir les logs d'erreur
  - avec une commande `journalctl`
  - généralement, il dit clairement l'erreur
- ajustement de la configuration
  - c'est un fichier texte (comme toujours)
  - donc avec `nano` ou `vim` par exemple
- redémarrage du service DHCP
  - avec un `systemctl restart`

> N'hésitez pas, comme d'hab, à m'appeler si vous galérez avec cette section !

## 3. Rendu attendu

> *Vous pouvez éteindre `client1.tp5.b1` et `client2.tp5.b1` pour limiter l'utilisation des ressources hein.*

⚠️⚠️⚠️ **Vous n'avez le droit d'utiliser QUE des lignes que vous comprenez dans le fichier de configuration.** Et pour lesquelles vous avez adapté les valeurs au TP. **Vous devez enlever les lignes de configuration inutiles pour notre TP.**

### A. Installation et configuration du serveur DHCP

> *Cette section A. est à réaliser sur `routeur.tp5.b1`.*

☀️ **Installez et configurez un serveur DHCP sur la machine `routeur.tp5.b1`**

- je veux toutes les commandes réalisées
- et le contenu du fichier de configuration
- le fichier de configuration doit :
  - indiquer qu'on propose aux clients des adresses IP entre `10.5.1.137` et `10.5.1.237`
  - indiquer aux clients que la passerelle dans le réseau ici c'est `10.5.1.254`
  - indiquer aux clients qu'un serveur DNS joignable depuis le réseau c'est `1.1.1.1`

### B. Test avec un nouveau client

> *Cette section B. est à réaliser sur une nouvelle machine Ubuntu fraîchement clonée : `client3.tp5.b1`. Vous pouvez éteindre `client1.tp5.b1` et `client2.tp5.b1` pour économiser des ressources.*

☀️ **Créez une nouvelle machine client `client3.tp5.b1`**

- définissez son *hostname*
- définissez une IP en DHCP
- vérifiez que c'est bien une adresse IP entre `.137` et `.237`
- prouvez qu'il a immédiatement un accès internet

### C. Consulter le bail DHCP

➜ **Côté serveur DHCP, à chaque fois qu'une adresse IP est proposée à quelqu'un, le serveur crée un fichier texte appelé *bail DHCP*** (ou *DHCP lease* en anglais).

Il contient toutes les informations liées à l'échange avec le client, notamment :

- adresse MAC du client qui a demandé l'IP
- adresse IP proposée au client
- heure et date précises de l'échange DHCP
- durée de validité du *bail DHCP*

> *A l'issue de cette durée de validité, le client devra de nouveau contacter le serveur, pour s'assurer que l'adresse IP est toujours libre. Rappelez-vous que DHCP est utilisé partout pour attribuer automatiquement des adresses IP aux clients, à l'école, chez vous, etc. C'est nécessaire que le bail expire pour pas qu'un client qui se connecte une seule fois monopolise à vie une adresse IP.*

☀️ **Consultez le *bail DHCP* qui a été créé pour notre client**

- à faire sur `routeur.tp5.b1`
- toutes les données du serveur DHCP, comme les *baux DHCP*, sont stockés dans le dossier `/var/lib/dhcpd/`
- afficher le contenu du fichier qui contient les *baux DHCP*
- on devrait y voir l'IP qui a été proposée au client, ainsi que son adresse MAC

☀️ **Confirmez qu'il s'agit bien de la bonne adresse MAC**

- à faire sur `client3.tp5.b1`
- consultez l'adresse MAC du client
- on peut consulter les adresses MAC des cartes réseau avec un simple `ip a`
