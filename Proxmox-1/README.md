<br/>
<p align="center">
  <h2 align="center">Documentation infra Light Snoop</h2>
  <h3 align="center">Proxmox 1</h3>
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
    * [Téléchargement ISOs](#Configuration-Interne)
  * [Installation Suivante](#Installation-Suivante)
* [Roadmap](#Roadmap)
* [License](#License)

## Pour Commencer

Pour faire/refaire l'infra Light Snoop :

### Prérequis

* [Rufus](https://github.com/pbatard/rufus/releases/latest/), [Balena Etcher](https://github.com/balena-io/etcher/releases/latest/) ou tout autre logiciel du genre
* Clé/Stockage USB de 4Go minimum
* ISO de [Proxmox VE](https://proxmox.com/en/downloads/proxmox-virtual-environment/iso)
* Un serveur de 16 coeurs CPU et 22Go de RAM minimum

### Installation

#### Formatage de la clé USB

1. Téléchargez l'ISO de Proxmox VE (ici 8.0-2)
![PfSense Website](/Proxmox-1/Img/Pr_Rufus-1.png?raw=true "PfSense Website")
2. Téléchargez Rufus
![Rufus Website](/Proxmox-1/Img/Pr_Rufus-2.png?raw=true "Rufus Website")
3. Branchez la clé USB sur le PC
4. Ouvrir Rufus
![Rufus](/Proxmox-1/Img/Pr_Rufus-3.png?raw=true "Rufus")
6. Sélectionnez la clé USB
![Rufus USB](/Proxmox-1/Img/Pr_Rufus-4.png?raw=true "Rufus USB")
5. Sélectionnez l'ISO de Proxmox VE, continuez si vous avez une erreur "ISOHybrid"
![Rufus ISO error](/Proxmox-1/Img/Pr_Rufus-5.png?raw=true "Rufus ISO error")
![Rufus ISO](/Proxmox-1/Img/Pr_Rufus-6.png?raw=true "Rufus ISO")
7. Lancez le formatage
- NEED 2 IMAGES
![Rufus Format](/Proxmox-1/Img/Pr_Rufus-7.png?raw=true "Rufus Format")
![Rufus End](/Proxmox-1/Img/Pr_Rufus-8.png?raw=true "Rufus End")

#### Système

1. Branchez la clé USB sur le serveur
2. Démarrez le serveur
3. Appuyez sur F11 pour accéder au boot menu
4. Sélectionnez la clé USB
![BIOS USB](/Proxmox-1/Img/Pr_USB.png?raw=true "BIOS USB")
5. -

#### Téléchargement ISOs

1. -

### Installation Suivante

* [Proxmox VE 2](/Proxmox-2/README.md)
* [PfSense 1](/Proxmox-1/PfSense-1/README.md)
* [Windows Server 2022 Standard 1](/Proxmox-1/Windows-1/README.md)
* [Debian 11 1](/Proxmox-1/Debian-1/README.md)

## Roadmap

* Fin

## License

Distribué sous la license WTFPL. Voir [WTFPL](http://www.wtfpl.net/about/) pour plus d'information.