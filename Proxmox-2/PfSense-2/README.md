<br/>
<p align="center">
  <h2 align="center">Documentation infra Light Snoop</h2>
  <h3 align="center">PfSense 2</h3>
  <p align="center">
    Fait dans le cadre du projet de l'épreuve E5 du BTS SIO 2022-2024
    <br/>
    <br/>
  </p>
</p>



## Sommaire

* [Pour Commencer](#Pour-Commencer)
  * [Prérequis](#Prérequis)
  * [Installation](#Installation)
    * [Création de la VM](#Création-de-la-VM)
    * [Système](#Système)
    * [Configuration Interne](#Configuration-Interne)
    * [Configuration GUI](#Configuration-GUI)
    * [Installation Suricata](#Installation-Suricata)
    * [Configuration OSPF](#Configuration-OSPF)
  * [Installation Suivante](#Installation-Suivante)
* [Roadmap](#Roadmap)
* [License](#License)

## Pour Commencer

Pour faire/refaire l'infra Light Snoop :

### Prérequis

* ISO de [PfSense](https://www.pfsense.org/download/) dans le Proxmox 2 (Voir [Proxmox-2](/Proxmox-2/README.md#téléchargement-isos))

### Installation

#### Création de la VM

1. Connectez un ordinateur au port LAN du serveur ou au VPN du PfSense Externe
2. Ouvrez un navigateur
3. Allez sur l'adresse https://192.168.200.1:8006/
4. Acceptez et continuez malgré le certificat invalide
![Proxmox Gui Certif](/Proxmox-2/Img/Pr_Gui-2.png?raw=true "Proxmox Gui Certif")
5. Connectez-vous avec les identifiants par défaut (ici root/hello)
![Proxmox Gui Connect](/Img/Prox/Pr_Gui-2.png?raw=true "Proxmox Gui Connect")
6. Faites "OK" si vous avez un message d'erreur de license, vous pouvez l'ignorer ou acheter une license mais nous ne le montrerons pas ici
![Proxmox Gui License](/Img/Prox/Pr_Gui-3.png?raw=true "Proxmox Gui License")
7. Faites "Create VM"
![Proxmox Gui Create VM](/Img/Prox/Pr_Gui-4.png?raw=true "Proxmox Gui Create VM")
8. Mettez la VM ID à 100, cela sera le Template final du PfSense Interne 1 en cas de besoin
9. Nommez la VM "Template-PfSense-2"
10. Faite "Next"
![Proxmox Gui VM ID](/Proxmox-2/PfSense-2/Img/Pf-2_Pr-1.png?raw=true "Proxmox Gui VM ID")
11. Sélectionnez l'ISO de PfSense
12. Faites "Next"
![Proxmox Gui ISO](/Img/Pf/Pr/Pf_Pr-2.png?raw=true "Proxmox Gui ISO")
13. Faites "Next"
![Proxmox Gui System](/Img/Pf/Pr/Pf_Pr-3.png?raw=true "Proxmox Gui System")
14. Mettez 10Go de "Disk size"
15. Faites "Next"
![Proxmox Gui Disk](/Img/Pf/Pr/Pf_Pr-4.png?raw=true "Proxmox Gui Disk")
16. Mettez 2 "Cores"
17. Faites "Next"
![Proxmox Gui CPU](/Img/Pf/Pr/Pf_Pr-5.png?raw=true "Proxmox Gui CPU")
18. Mettez 4096 de "Memory"
19. Faites "Next"
![Proxmox Gui RAM](/Img/Pf/Pr/Pf_Pr-6.png?raw=true "Proxmox Gui RAM")
20. Faites à nouveau "Next", nous configurerons une seconde carte réseau plus tard
![Proxmox Gui Pf Network](/Img/Pf/Pr/Pf_Pr-7.png?raw=true "Proxmox Gui Network")
21. Confirmez la création de la VM sans cocher "Start after created"
![Proxmox Gui Summary](/Proxmox-2/PfSense-2/Img/Pf-2_Pr-8.png?raw=true "Proxmox Gui Summary")
22. Cliquez sur "LightSnoop-2" dans la colonne de gauche
![Proxmox Gui Network](/Proxmox-2/PfSense-2/Img/Pf-2_Pr-9.png?raw=true "Proxmox Gui Network")
23. Cliquez sur "Network"
![Proxmox Gui Network](/Img/Pf/Pr/Pf_Pr-10.png?raw=true "Proxmox Gui Network")
24. Cliquez sur "Create"
25. Cliquer sur "Linux Bridge"
![Proxmox Gui Linux Bridge](/Img/Pf/Pr/Pf_Pr-11.png?raw=true "Proxmox Gui Linux Bridge")
26. Nommez la "vmbr100" et mettez le nom de l'interface physique (ici "ens36") dans "Bridge ports"
27. Faites "Create"
![Proxmox Gui Bridge](/Img/Pf/Pr/Pf_Pr-12.png?raw=true "Proxmox Gui Bridge")
28. Cliquez sur "Template-PfSense-2" dans la colonne de gauche
![Proxmox Gui Network](/Proxmox-2/PfSense-2/Img/Pf-2_Pr-13.png?raw=true "Proxmox Gui Network")
29. Cliquez sur "Hardware"
![Proxmox Gui Hardware](/Img/Pf/Pr/Pf_Pr-14.png?raw=true "Proxmox Gui Hardware")
30. Cliquez sur "Add" puis "Network Device"
![Proxmox Gui Network Device](/Img/Pf/Pr/Pf_Pr-15.png?raw=true "Proxmox Gui Network Device")
31. Sélectionnez "vmbr100" dans "Bridge"
32. Faites "Add"
![Proxmox Gui Network Device](/Img/Pf/Pr/Pf_Pr-16.png?raw=true "Proxmox Gui Network Device")
33. Cliquez sur "Console"
![Proxmox Gui Console](/Img/Pf/Pr/Pf_Pr-17.png?raw=true "Proxmox Gui Console")
34. Cliquez sur "Start Now"
![Proxmox Gui Start](/Img/Pf/Pr/Pf_Pr-18.png?raw=true "Proxmox Gui Start")
34.a En cas d'erreur, redémarrez le serveur et recommencez à partir de l'étape 33

#### Système

0. Démarrez la VM
1. Faites entrer pour démarrer l'installation
![PfSense Install Start](/Img/Pf/Pf_Install-1.png?raw=true "PfSense Install Start")
2. Sélectionnez "Install"
![PfSense Install](/Img/Pf/Pf_Install-2.png?raw=true "PfSense Install")
3. Sélectionnez le clavier "Auto (ZFS)"
![PfSense Install ZFS](/Img/Pf/Pf_Install-3.png?raw=true "PfSense Install ZFS")
4. Faites entrer pour valider la configuration
![PfSense Install Conf](/Img/Pf/Pf_Install-4.png?raw=true "PfSense Install Conf")
5. Sélectionnez "Stripe"
![PfSense Install Stripe](/Img/Pf/Pf_Install-5.png?raw=true "PfSense Install Stripe")
6. Sélectionnez votre disque (touche espace pour sélectionner), ici "da0"
![PfSense Install Disk](/Img/Pf/Pr/Pf_Install-6.png?raw=true "PfSense Install Disk")
7. Sélectionnez "Yes"
![PfSense Install Format](/Img/Pf/Pf_Install-7.png?raw=true "PfSense Install Format")
8. L'installation commence, sélectionnez "Reboot" une fois terminé
![PfSense Installing](/Img/Pf/Pf_Install-8.png?raw=true "PfSense Installing")
![PfSense Install Reboot](/Img/Pf/Pf_Install-9.png?raw=true "PfSense Install Reboot")

#### Configuration Interne

0. Laissez le PfSense démarrer
1. Faites "a" pour détecter automatiquement l'inteface WAN et LAN, en cas d'erreur, sélectionnez les manuellement
2. Appuyez sur 2 pour configurer l'interface WAN
![PfSense Conf IntWAN](/Img/Pf/Pf_Conf-1.png?raw=true "PfSense Conf IntWAN")
3. Sélectionnez l'interface WAN avec le numéro correspondant (ici 1)
![PfSense Conf WAN](/Img/Pf/Pf_Conf-2.png?raw=true "PfSense Conf WAN")
4. Faites "y" pour configurer l'interface WAN en DHCP pour l'IpV4
5. Faites de même pour l'IpV6
![PfSense Conf WAN DHCP](/Img/Pf/Pf_Conf-3.png?raw=true "PfSense Conf WAN DHCP")
6. Si demandé, refusez l'http pour le webconfigurator
![PfSense Conf WebConf](/Img/Pf/Pf_Conf-4.png?raw=true "PfSense Conf WebConf")
7. Faites "Entrer" pour valider la configuration
8. Appuyez sur 2 pour configurer l'interface LAN
9. Sélectionnez l'interface LAN avec le numéro correspondant (ici 2)
![PfSense Conf LAN](/Img/Pf/Pf_Conf-5.png?raw=true "PfSense Conf LAN")
10. Faites "n" pour configurer l'interface LAN en statique pour l'IpV4
11. L'adresse LAN est 192.168.20.254
12. Le masque est 24
13. Faites "Entrer" pour la Gateway car c'est le serveur PfSense lui-même
![PfSense Conf LAN Static](/Proxmox-2/PfSense-2/Img/Pf-2_Conf-6.png?raw=true "PfSense Conf LAN Static")
15. Faites "y" pour configurer l'interface LAN en DHCP pour l'IpV6, la raison étant que nous n'en avons pas besoin dans cette infra
16. Faites "y" pour configurer le serveur DHCP pour l'IpV4
![PfSense Conf LAN DHCP4](/Img/Pf/Pf_Conf-7.png?raw=true "PfSense Conf LAN DHCP4")
17. L'adresse de départ est 192.168.20.1
18. L'adresse de fin est 192.168.20.5
19. Faites "Entrer" pour valider la configuration
![PfSense Conf LAN Range](/Proxmox-2/PfSense-2/Img/Pf-2_Conf-8.png?raw=true "PfSense Conf LAN Range")

#### Configuration GUI

0. Installez la VM [Debian 11 2](/Proxmox-2/Debian-2/README.md) ou [Windows Server 2022 Standard 2](/Proxmox-2/Windows-2/README.md)

1. Connectez vous à la VM [Debian 11 2](/Proxmox-2/Debian-2/README.md) ou [Windows Server 2022 Standard 2](/Proxmox-2/Windows-2/README.md) en console depuis Proxmox
2. Ouvrez un navigateur
3. Allez sur l'adresse https://192.168.20.254/
4. Acceptez et continuez malgré le certificat invalide
![PfSense Gui Certif](/Proxmox-2/PfSense-2/Img/Pf-2_Gui-1.png?raw=true "PfSense Gui Certif")
4. Connectez-vous avec les identifiants par défaut (admin/pfsense)
![PfSense Gui Connect](/Proxmox-2/PfSense-2/Img/Pf-2_Gui-2.png?raw=true "PfSense Gui Connect")
5. Faites "Next"
![PfSense Gui Startup2](/Img/Pf/Pf_Gui-3.png?raw=true "PfSense Gui Startup2")
6. Faites "Next"
![PfSense Gui Startup3](/Img/Pf/Pf_Gui-4.png?raw=true "PfSense Gui Startup3")
7. Remplissez les informations :
  * "Pf-1" pour le hostname
  * "1.1.1.1" pour le DNS principal
  * "8.8.8.8" pour le DNS secondaire
8. Faites "Next"
![PfSense Gui Host](/Proxmox-2/PfSense-2/Img/Pf-2_Gui-5.png?raw=true "PfSense Gui Host")
9. Séléctionnez votre fuseau horaire (ici Europe/Paris)
10. Faites "Next"
![PfSense Gui Date/Time](/Img/Pf/Pf_Gui-6.png?raw=true "PfSense Gui Date/Time")
11. Faites "Next", aucune modification n'est nécessaire pour le WAN
![PfSense Gui WAN1](/Proxmox-2/PfSense-2/Img/Pf-2_Gui-7.png?raw=true "PfSense Gui WAN1")
![PfSense Gui WAN2](/Proxmox-2/PfSense-2/Img/Pf-2_Gui-8.png?raw=true "PfSense Gui WAN2")
12. Faites "Next", aucune modification n'est nécessaire pour le LAN
![PfSense Gui LAN](/Proxmox-2/PfSense-2/Img/Pf-2_Gui-9.png?raw=true "PfSense Gui LAN")
13. Changez le mot de passe de l'admin (ici "hello")
14. Faites "Next"
![PfSense Gui Passwd](/Img/Pf/Pf_Gui-10.png?raw=true "PfSense Gui Passwd")
15. Faites "Reload" et attendez que le serveur redémarre
![PfSense Gui Reload](/Img/Pf/Pf_Gui-11.png?raw=true "PfSense Gui Reload")
16. Une fois la page rechargée, faites "Check for updates" si l'ISO utilisée est ancienne, sinon faites "Finish"
![PfSense Gui Update](/Img/Pf/Pf_Gui-12.png?raw=true "PfSense Gui Update")
17. Acceptez les conditions d'utilisation
![PfSense Gui Notice](/Img/Pf/Pf_Gui-13.png?raw=true "PfSense Gui Notice")
18. Faites "Close"
![PfSense Gui End](/Img/Pf/Pf_Gui-14.png?raw=true "PfSense Gui End")

#### Installation Suricata

1. -

#### Configuration OSPF

1. -

### Installation Suivante

* [Windows Server 2022 Standard 2](/Proxmox-2/Windows-2/README.md)
* [Debian 11 2](/Proxmox-2/Debian-2/README.md)

## Roadmap

* Ajout de routage OSPF entre les deux PfSense interne

## License

Distribué sous la license WTFPL. Voir [WTFPL](http://www.wtfpl.net/about/) pour plus d'information.