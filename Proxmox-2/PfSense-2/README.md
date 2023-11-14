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
    * [Configuration Interfaces](#Configuration-Interfaces)
    * [Installation Suricata](#Installation-Suricata)
    * [Configuration OSPF](#Configuration-OSPF)
  * [Installation Suivante](#Installation-Suivante)
* [Roadmap](#Roadmap)
* [License](#License)

## Pour Commencer

Pour faire/refaire l'infra Light Snoop :

### Prérequis

* ISO de [PfSense](https://www.pfsense.org/download/) dans le Proxmox (Voir [Proxmox-2/README.md](/Proxmox-2/README.md#téléchargement-isos))

### Installation

#### Création de la VM

1. -

#### Système

1. Démarrez la VM
2. Faites entrer pour démarrer l'installation
![PfSense Install Start](/Img/Pf/Pf_Install-1.png?raw=true "PfSense Install Start")
3. Sélectionnez "Install"
![PfSense Install](/Img/Pf/Pf_Install-2.png?raw=true "PfSense Install")
4. Sélectionnez le clavier "Auto (ZFS)"
![PfSense Install ZFS](/Img/Pf/Pf_Install-3.png?raw=true "PfSense Install ZFS")
5. Faites entrer pour valider la configuration
![PfSense Install Conf](/Img/Pf/Pf_Install-4.png?raw=true "PfSense Install Conf")
6. Sélectionnez "Stripe"
![PfSense Install Stripe](/Img/Pf/Pf_Install-5.png?raw=true "PfSense Install Stripe")
7. Sélectionnez votre disque (touche espace pour sélectionner), ici "da0"
![PfSense Install Disk](/Img/Pf/Pf_Install-6.png?raw=true "PfSense Install Disk")
8. Sélectionnez "Yes"
![PfSense Install Format](/Img/Pf/Pf_Install-7.png?raw=true "PfSense Install Format")
9. L'installation commence, sélectionnez "Reboot" une fois terminé
![PfSense Installing](/Img/Pf/Pf_Install-8.png?raw=true "PfSense Installing")
![PfSense Install Reboot](/Img/Pf/Pf_Install-9.png?raw=true "PfSense Install Reboot")

#### Configuration Interne

1. Laissez le serveur démarrer
2. Appuyez sur 2 pour configurer l'interface WAN
![PfSense Conf IntWAN](/Img/Pf/Pf_Conf-1.png?raw=true "PfSense Conf IntWAN")
3. Sélectionnez l'interface WAN avec le numéro correspondant (ici 1)
![PfSense Conf WAN](/Img/Pf/Pf_Conf-2.png?raw=true "PfSense Conf WAN")
4. Faites "n" pour configurer l'interface WAN en Statique pour l'IpV4
5. -

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
  * "Pf-2" pour le hostname
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

#### Configuration Interfaces

1. -

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