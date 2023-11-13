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
  * [Installation](#nstallation)
* [Roadmap](#Roadmap)
* [Contribuer](#Contribuer)
* [License](#License)
* [Autheurs](#Autheurs)

## Pour Commencer

Pour faire/refaire l'infra Light Snoop :

### Prérequis

* [Rufus](https://github.com/pbatard/rufus/releases/latest/), [Balena Etcher](https://github.com/balena-io/etcher/releases/latest/) ou tout autre logiciel du genre
* [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) ou autre logiciel d'interaction console
* [OpenVPN](https://openvpn.net/community-downloads/)
* Clé/Stockage USB de 4Go minimum
* ISO de [Proxmox VE](https://proxmox.com/en/downloads/proxmox-virtual-environment/iso)
* Un PfSense externe connecté en WAN
* Deux serveurs de 16 coeurs CPU et 22Go de RAM minimum
* Borne WiFi (Ici Cisco Aironet AIR-PWR-B)
* Switch pour redistribuer du PfSense aux serveurs et des serveurs au Wifi
* Optionnel : ISO de PfSense, Windows Server 2022 et Debian 11

### Installation

* [PfSense Externe](/PfSense%20Externe/README.md)
* [Proxmox VE]()
* [PfSense Interne 1]()
* [PfSense Interne 2]()
* [Windows Server 2022 Standard 1]()
* [Windows Server 2022 Standard 2]()
* [Debian 11 1]()
* [Debian 11 2]()
* [Switch]()
* [Borne WiFi]()

## Roadmap

* Ajout de routage OSPF entre les deux PfSense interne
* Flashage de la borne WiFi (Cisco Aironet AIR-PWR-B)
* Configuration de la borne WiFi
* Routage interne vers la borne WiFi

## Contribuer

* Si vous avez des suggestions pour ajouter ou supprimer des projets, n'hésitez pas à [Issues](https://github.com/E5-MMGE/Documentation-Light-Snoop-E5/issues) pour en discuter, ou créez directement une demande d'extraction après avoir édité le fichier *README.md* avec les changements nécessaires.
* Créer un PR individuel pour chaque suggestion.

## License

Distribué sous la license WTFPL. Voir [WTFPL](http://www.wtfpl.net/about/) pour plus d'information.

## Autheurs

* [Nikki Devil](https://github.com/Nikki-Devil/)
* [Matis Games 35](https://github.com/MatisGames35)
* [Kriooxx](https://github.com/kriooxx)
* [Nghyy](https://github.com/nghyy)
