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

1. Télécharger l'ISO de PfSense (ici 2.7.0, AMD64, DVD Image)
![PfSense Website](/PfSense-WAN/Img/Pf_Rufus-1.png?raw=true "PfSense Website")
2. Télécharger Rufus
* Image du Git de Rufus
3. Brancher la clé USB sur le PC
4. Ouvrir Rufus
* Image de Rufus
6. Sélectionner la clé USB
* Image de Rufus avec la clé USB
5. Sélectionner l'ISO de PfSense
* Image de Rufus avec l'ISO erreur
* Image de Rufus avec l'ISO sélectionné
7. Lancer le formatage
* Image de Rufus avec le formatage
* Image de Rufus avec le formatage terminé

#### Système

1. Brancher la clé USB sur le serveur
2. Démarrer le serveur
3. Appuyer sur F11 pour accéder au boot menu
4. Sélectionner la clé USB
* Image de l'écran de boot
5. Faites entrer pour démarrer l'installation
* Image de l'écran d'installation 1
6. Sélectionner "Install"
* Image de l'écran d'installation 2
7. Sélectionner le clavier "Auto (ZFS)"
* Image de l'écran d'installation 3
8. Faites entrer pour valider la configuration
* Image de l'écran d'installation 4
9. Sélectionner "Stripe"
* Image de l'écran d'installation 5
10. Sélectionner votre disque (touche espace pour sélectionner), ici "da0"
* Image de l'écran d'installation 6
11. Sélectionner "Yes"
* Image de l'écran d'installation 7
12. L'installation commence, sélectionnez "Reboot" une fois terminé
* Image de l'écran d'installation 8
* Image de l'écran d'installation 9

#### Configuration Interne

1. Laissez le serveur démarrer
2. Appuyez sur 2 pour configurer l'interface WAN
* Image de l'écran de configuration 1
3. Sélectionnez l'interface WAN avec le numéro correspondant (ici 1)
* Image de l'écran de configuration 2
4. Faites "y" pour configurer l'interface WAN en DHCP pour l'IpV4
5. Faites de même pour l'IpV6
* Image de l'écran de configuration 3
6. Si demandé, refusez l'http pour le webconfigurator
* Image de l'écran de configuration 4
7. Faites "Entrer" pour valider la configuration
8. Appuyez sur 2 pour configurer l'interface LAN
9. Sélectionnez l'interface LAN avec le numéro correspondant (ici 2)
* Image de l'écran de configuration 5
10. Faites "n" pour configurer l'interface LAN en statique pour l'IpV4
11. L'adresse LAN est 192.168.1.1
12. Le masque est 24
13. Faites "Entrer" pour la Gateway car c'est le serveur PfSense lui-même
* Image de l'écran de configuration 6
15. Faites "y" pour configurer l'interface LAN en DHCP pour l'IpV6, la raison étant que nous n'en avons pas besoin dans cette infra
16. Faites "y" pour configurer le serveur DHCP pour l'IpV4
* Image de l'écran de configuration 7
17. L'adresse de départ est 192.168.1.2
18. L'adresse de fin est 192.168.1.5
19. Faites "Entrer" pour valider la configuration
* Image de l'écran de configuration 8

#### Configuration GUI

1. Connectez un ordinateur au port LAN du serveur
2. Ouvrez un navigateur
3. Allez sur l'adresse https://192.168.1.1/
4. Acceptez et continuez malgré le certificat invalide
* Image du GUI 1
4. Connectez-vous avec les identifiants par défaut (admin/pfsense)
* Image du GUI 2
5. Faites "Next"
* Image du GUI 3
6. Faites "Next"
* Image du GUI 4
7. Remplissez les informations :
  * "Pf-WAN" pour le hostname
  * "1.1.1.1" pour le DNS principal
  * "8.8.8.8" pour le DNS secondaire
8. Faites "Next"
* Image du GUI 5
9. Séléctionnez votre fuseau horaire (ici Europe/Paris)
10. Faites "Next"
* Image du GUI 6
11. Faites "Next", aucune modification n'est nécessaire pour le WAN
* Image du GUI 7
* Image du GUI 8
12. Faites "Next", aucune modification n'est nécessaire pour le LAN
* Image du GUI 9
13. Changez le mot de passe de l'admin (ici "admin")
14. Faites "Next"
* Image du GUI 10
15. Faites "Reload" et attendez que le serveur redémarre
* Image du GUI 11
16. Une fois la page rechargée, faites "Check for updates" si l'ISO utilisée est ancienne, sinon faites "Finish"
* Image du GUI 12
17. Acceptez les conditions d'utilisation
* Image du GUI 13
18. Faites "Close"
* Image du GUI 14

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