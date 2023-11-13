<br/>
<p align="center">
  <h2 align="center">Documentation infra Light Snoop</h2>
  <h3 align="center">PfSense Externe</h3>
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
    * [Formatage de la clé USB](#Formatage-de-la-clé-USB)
    * [Système](#Système)
    * [Configuration Interne](#Configuration-Interne)
    * [Configuration GUI](#Configuration-GUI)
    * [Configuration Interfaces](#Configuration-Interfaces)
    * [Configuration VPN](#Configuration-VPN)
    * [Configuration OSPF](#Configuration-OSPF)
  * [Installation Suivante](#Installation-Suivante)
* [Roadmap](#Roadmap)
* [License](#License)

## Pour Commencer

Pour faire/refaire l'infra Light Snoop :

### Prérequis

* [Rufus](https://github.com/pbatard/rufus/releases/latest/), [Balena Etcher](https://github.com/balena-io/etcher/releases/latest/) ou tout autre logiciel du genre
* Clé/Stockage USB de 4Go minimum
* ISO de [PfSense](https://www.pfsense.org/download/)
* Un serveur 2 coeurs et 2Go minimum **avec deux cartes réseaux**

### Installation

#### Formatage de la clé USB

1. Téléchargez l'ISO de PfSense (ici 2.7.0, AMD64, DVD Image)
![PfSense Website](/PfSense-WAN/Img/Pf_Rufus-1.png?raw=true "PfSense Website")
2. Téléchargez Rufus
![Rufus Website](/PfSense-WAN/Img/Pf_Rufus-2.png?raw=true "Rufus Website")
3. Branchez la clé USB sur le PC
4. Ouvrir Rufus
![Rufus](/PfSense-WAN/Img/Pf_Rufus-3.png?raw=true "Rufus")
6. Sélectionnez la clé USB
![Rufus USB](/PfSense-WAN/Img/Pf_Rufus-4.png?raw=true "Rufus USB")
5. Sélectionnez l'ISO de PfSense, continuez si vous avez une erreur "ISOHybrid"
![Rufus ISO error](/PfSense-WAN/Img/Pf_Rufus-5.png?raw=true "Rufus ISO error")
![Rufus ISO](/PfSense-WAN/Img/Pf_Rufus-6.png?raw=true "Rufus ISO")
7. Lancez le formatage
- NEED 2 IMAGES
![Rufus Format](/PfSense-WAN/Img/Pf_Rufus-7.png?raw=true "Rufus Format")
![Rufus End](/PfSense-WAN/Img/Pf_Rufus-8.png?raw=true "Rufus End")

#### Système

1. Branchez la clé USB sur le serveur
2. Démarrez le serveur
3. Appuyez sur F11 pour accéder au boot menu
4. Sélectionnez la clé USB
![BIOS USB](/PfSense-WAN/Img/Pf_USB.png?raw=true "BIOS USB")
5. Faites entrer pour démarrer l'installation
![PfSense Install Start](/PfSense-WAN/Img/Pf_Install-1.png?raw=true "PfSense Install Start")
6. Sélectionnez "Install"
![PfSense Install](/PfSense-WAN/Img/Pf_Install-2.png?raw=true "PfSense Install")
7. Sélectionnez le clavier "Auto (ZFS)"
![PfSense Install ZFS](/PfSense-WAN/Img/Pf_Install-3.png?raw=true "PfSense Install ZFS")
8. Faites entrer pour valider la configuration
![PfSense Install Conf](/PfSense-WAN/Img/Pf_Install-4.png?raw=true "PfSense Install Conf")
9. Sélectionnez "Stripe"
![PfSense Install Stripe](/PfSense-WAN/Img/Pf_Install-5.png?raw=true "PfSense Install Stripe")
10. Sélectionnez votre disque (touche espace pour sélectionner), ici "da0"
![PfSense Install Disk](/PfSense-WAN/Img/Pf_Install-6.png?raw=true "PfSense Install Disk")
11. Sélectionnez "Yes"
![PfSense Install Format](/PfSense-WAN/Img/Pf_Install-7.png?raw=true "PfSense Install Format")
12. L'installation commence, sélectionnez "Reboot" une fois terminé
![PfSense Installing](/PfSense-WAN/Img/Pf_Install-8.png?raw=true "PfSense Installing")
![PfSense Install Reboot](/PfSense-WAN/Img/Pf_Install-9.png?raw=true "PfSense Install Reboot")

#### Configuration Interne

1. Laissez le serveur démarrer
2. Appuyez sur 2 pour configurer l'interface WAN
![PfSense Conf IntWAN](/PfSense-WAN/Img/Pf_Conf-1.png?raw=true "PfSense Conf IntWAN")
3. Sélectionnez l'interface WAN avec le numéro correspondant (ici 1)
![PfSense Conf WAN](/PfSense-WAN/Img/Pf_Conf-2.png?raw=true "PfSense Conf WAN")
4. Faites "y" pour configurer l'interface WAN en DHCP pour l'IpV4
5. Faites de même pour l'IpV6
![PfSense Conf WAN DHCP](/PfSense-WAN/Img/Pf_Conf-3.png?raw=true "PfSense Conf WAN DHCP")
6. Si demandé, refusez l'http pour le webconfigurator
![PfSense Conf WebConf](/PfSense-WAN/Img/Pf_Conf-4.png?raw=true "PfSense Conf WebConf")
7. Faites "Entrer" pour valider la configuration
8. Appuyez sur 2 pour configurer l'interface LAN
9. Sélectionnez l'interface LAN avec le numéro correspondant (ici 2)
![PfSense Conf LAN](/PfSense-WAN/Img/Pf_Conf-5.png?raw=true "PfSense Conf LAN")
10. Faites "n" pour configurer l'interface LAN en statique pour l'IpV4
11. L'adresse LAN est 192.168.1.1
12. Le masque est 24
13. Faites "Entrer" pour la Gateway car c'est le serveur PfSense lui-même
![PfSense Conf LAN Static](/PfSense-WAN/Img/Pf_Conf-6.png?raw=true "PfSense Conf LAN Static")
15. Faites "y" pour configurer l'interface LAN en DHCP pour l'IpV6, la raison étant que nous n'en avons pas besoin dans cette infra
16. Faites "y" pour configurer le serveur DHCP pour l'IpV4
![PfSense Conf LAN DHCP4](/PfSense-WAN/Img/Pf_Conf-7.png?raw=true "PfSense Conf LAN DHCP4")
17. L'adresse de départ est 192.168.1.2
18. L'adresse de fin est 192.168.1.5
19. Faites "Entrer" pour valider la configuration
![PfSense Conf LAN Range](/PfSense-WAN/Img/Pf_Conf-6.png?raw=true "PfSense Conf LAN Range")

#### Configuration GUI

1. Connectez un ordinateur au port LAN du serveur
2. Ouvrez un navigateur
3. Allez sur l'adresse https://192.168.1.1/
4. Acceptez et continuez malgré le certificat invalide
![PfSense Gui Certif](/PfSense-WAN/Img/Pf_Gui-1.png?raw=true "PfSense Gui Certif")
4. Connectez-vous avec les identifiants par défaut (admin/pfsense)
![PfSense Gui Connect](/PfSense-WAN/Img/Pf_Gui-2.png?raw=true "PfSense Gui Connect")
5. Faites "Next"
![PfSense Gui Startup2](/PfSense-WAN/Img/Pf_Gui-3.png?raw=true "PfSense Gui Startup2")
6. Faites "Next"
![PfSense Gui Startup3](/PfSense-WAN/Img/Pf_Gui-4.png?raw=true "PfSense Gui Startup3")
7. Remplissez les informations :
  * "Pf-WAN" pour le hostname
  * "1.1.1.1" pour le DNS principal
  * "8.8.8.8" pour le DNS secondaire
8. Faites "Next"
![PfSense Gui Host](/PfSense-WAN/Img/Pf_Gui-5.png?raw=true "PfSense Gui Host")
9. Séléctionnez votre fuseau horaire (ici Europe/Paris)
10. Faites "Next"
![PfSense Gui Date/Time](/PfSense-WAN/Img/Pf_Gui-6.png?raw=true "PfSense Gui Date/Time")
11. Faites "Next", aucune modification n'est nécessaire pour le WAN
![PfSense Gui WAN1](/PfSense-WAN/Img/Pf_Gui-7.png?raw=true "PfSense Gui WAN1")
![PfSense Gui WAN2](/PfSense-WAN/Img/Pf_Gui-8.png?raw=true "PfSense Gui WAN2")
12. Faites "Next", aucune modification n'est nécessaire pour le LAN
![PfSense Gui LAN](/PfSense-WAN/Img/Pf_Gui-9.png?raw=true "PfSense Gui LAN")
13. Changez le mot de passe de l'admin (ici "admin")
14. Faites "Next"
![PfSense Gui Passwd](/PfSense-WAN/Img/Pf_Gui-10.png?raw=true "PfSense Gui Passwd")
15. Faites "Reload" et attendez que le serveur redémarre
![PfSense Gui Reload](/PfSense-WAN/Img/Pf_Gui-11.png?raw=true "PfSense Gui Reload")
16. Une fois la page rechargée, faites "Check for updates" si l'ISO utilisée est ancienne, sinon faites "Finish"
![PfSense Gui Update](/PfSense-WAN/Img/Pf_Gui-12.png?raw=true "PfSense Gui Update")
17. Acceptez les conditions d'utilisation
![PfSense Gui Notice](/PfSense-WAN/Img/Pf_Gui-13.png?raw=true "PfSense Gui Notice")
18. Faites "Close"
![PfSense Gui End](/PfSense-WAN/Img/Pf_Gui-14.png?raw=true "PfSense Gui End")

#### Configuration Interfaces

1. -

#### Configuration VPN

1. -

#### Configuration OSPF

1. -

### Installation Suivante

* [Switch](/Switch/README.md)
* [Proxmox VE 1](/Proxmox-1/README.md)
* [Proxmox VE 2](/Proxmox-2/README.md)

## Roadmap

* Ajout des sous-interfaces pour le LAN (192.168.100.0 et 192.168.200.0)
* Ajout VPN vers le LAN
* Ajout de routage OSPF entre les deux PfSense interne

## License

Distribué sous la license WTFPL. Voir [WTFPL](http://www.wtfpl.net/about/) pour plus d'information.