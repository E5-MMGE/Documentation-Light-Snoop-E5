<br/>
<p align="center">
  <h3 align="center">Documentation infra Light Snoop</h3>

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
  * [Installation Suivante](#Installation-Suivante)
* [Roadmap](#Roadmap)
* [Contribuer](#Contribuer)
* [License](#License)
* [Autheurs](#Autheurs)

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
* Image du site de PfSense
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
4. Sélectionnez "y" pour configurer l'interface WAN en DHCP pour l'IpV4
5. Faire de même pour l'IpV6
* Image de l'écran de configuration 3


### Installation Suivante

* [Switch](/Switch/README.md)
* [Proxmox VE 1](/Proxmox-1/README.md)
* [Proxmox VE 2](/Proxmox-2/README.md)

## Roadmap

* Ajout de routage OSPF entre les deux PfSense interne

## License

Distribué sous la license WTFPL. Voir [WTFPL](http://www.wtfpl.net/about/) pour plus d'information.