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

* [Pour Commencer](#getting-started)
  * [Prérequis](#prerequisites)
  * [Installation](#installation)
* [Roadmap](#roadmap)
* [Contribuer](#contributing)
* [License](#license)
* [Autheurs](#authors)

## Pour Commencer

Pour faire/refaire l'infra Light Snoop :

### Prérequis

* ISO de Proxmox
```sh
wget https://enterprise.proxmox.com/iso/proxmox-ve_8.0-2.iso
```
* Un PfSense externe connecté en WAN
* Deux serveurs de 16 coeurs CPU et 22Go de RAM minimum
* Borne WiFi (Ici Cisco Aironet AIR-PWR-B)
* Switch pour redistribuer du PfSense aux serveurs et des serveurs au Wifi
* Optionnel : ISO de PfSense, Windows Server 2022 et Debian 11

### Installation

* [Proxmox VE]()
* [PfSense]()
* [Windows Server 2022 Standard]()
* [Debian 11]()

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
