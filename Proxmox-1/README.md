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
* Un serveur de 16 coeurs CPU virtualisable, 22Go de RAM minimum et 220Go de stockage

### Installation

#### Formatage de la clé USB

1. Téléchargez l'ISO de Proxmox VE (ici 8.0-2)
![Proxmox VE Website](/Img/Prox/Pr_Rufus-1.png?raw=true "PfSense Website")
2. Téléchargez Rufus
![Rufus Website](/Img/Rufus-2.png?raw=true "Rufus Website")
3. Branchez la clé USB sur le PC
4. Ouvrir Rufus
![Rufus](/Img/Rufus-3.png?raw=true "Rufus")
6. Sélectionnez la clé USB
![Rufus USB](/Img/Rufus-4.png?raw=true "Rufus USB")
5. Sélectionnez l'ISO de Proxmox VE, continuez si vous avez une erreur "ISOHybrid"
![Rufus ISO error](/Img/Rufus-5.png?raw=true "Rufus ISO error")
![Rufus ISO](/Img/Prox/Pr_Rufus-6.png?raw=true "Rufus ISO")
7. Lancez le formatage
- NEED 2 IMAGES
![Rufus Format](/Img/Prox/Pr_Rufus-7.png?raw=true "Rufus Format")
![Rufus End](/Img/Prox/Pr_Rufus-8.png?raw=true "Rufus End")

#### Système

0. Connect to the server to the Switch
1. Branchez la clé USB sur le serveur
2. Démarrez le serveur
3. Appuyez sur F11 pour accéder au boot menu
4. Sélectionnez la clé USB
![BIOS USB](/Img/Bios_USB.png?raw=true "BIOS USB")
5. Sélectionnez "Install Proxmox VE (Graphical)"
![Proxmox Install](/Img/Prox/Pr_Install-1.png?raw=true "Proxmox Install")
6. Sélectionnez "I agree" pour accepter la license d'utilisation
![Proxmox License](/Img/Prox/Pr_Install-2.png?raw=true "Proxmox License")
7. Sélectionnez le disque sur lequel vous voulez installer Proxmox VE (ici /dev/sda)
8. Puis faites "Next"
![Proxmox Disk](/Img/Prox/Pr_Install-3.png?raw=true "Proxmox Disk")
9. Sélectionnez votre pays, zone horaire et clavier (ici France, le reste s'est mis automatiquement)
10. Puis faites "Next"
![Proxmox Country](/Img/Prox/Pr_Install-4.png?raw=true "Proxmox Country")
11. Entrez un mot de passe pour le compte root et une adresse mail pour le compte admin@pam (ici "hello" et "e5@8e-couche.xyz")
12. Puis faites "Next"
![Proxmox Password](/Img/Prox/Pr_Install-5.png?raw=true "Proxmox Password")
13. Sélectionnez votre carte réseau (ici ens33)
14. Entrez un nom d'hôte (ici "LightSnoop-1.local")
15. Entrez la configuration réseau (ici 192.168.100.1/24, Gateway 192.168.100.254, DNS 192.168.100.254)
16. Puis faites "Next"
![Proxmox Network](/Proxmox-1/Img/Pr-1_Install-6.png?raw=true "Proxmox Network")
17. Vérifiez les informations, laissez "Reboot" coché et faites "Install"
![Proxmox Summary](/Proxmox-1/Img/Pr-1_Install-7.png?raw=true "Proxmox Summary")
18. Attendez que l'installation se termine et que le Proxmox redémarre
![Proxmox End](/Proxmox-1/Img/Pr-1_Install-8.png?raw=true "Proxmox End")
19. Si ce n'est pas déjà fait, faites la configuration des interfaces du [PfSense Externe](/PfSense-WAN/README.md#configuration-interfaces)

#### Téléchargement ISOs

0. Connectez-vous au Proxmox en physique, SSH ou sur la console de l'interface web (https://192.168.100.1:8006/), (ici en physique)
1. Si demandé, rentrez le mot de passe root (ici "root", "hello")
2. Naviguez jusqu'à "Var" > "Lib" > "VZ" > "Template" > "ISO"
```sh
cd /var/lib/vz/template/iso
```
![Proxmox Login + Location](/Proxmox-1/Img/Pr-1_ISO-1.png?raw=true "Proxmox Login + Location")
3. Téléchargez les ISOs avec wget
3.a Pour PfSense, récupérez le lien direct de l'ISO sur le site de [PfSense](https://www.pfsense.org/download/)
```sh	
wget https://atxfiles.netgate.com/mirror/downloads/pfSense-CE-2.7.0-RELEASE-amd64.iso.gz
tar -xvf pfSense-CE-2.7.0-RELEASE-amd64.iso.gz PfSense_2.7.0_x64.iso
rm pfSense-CE-2.7.0-RELEASE-amd64.iso.gz
```
3.b Pour Debian 11, récupérez le lien direct de l'ISO sur le site archive de [Debian](https://cdimage.debian.org/mirror/cdimage/archive/)
```sh
wget https://cdimage.debian.org/mirror/cdimage/archive/11.8.0/amd64/iso-cd/debian-11.8.0-amd64-netinst.iso
mv debian-11.8.0-amd64-netinst.iso Debian_11.8.0_x64.iso
```
3.c Pour Windows Server 2022, récupérez un lien direct de l'ISO (ici nous passerons par un site personnel)
```sh
wget https://ftp.8e-couche.xyz/Iso/WinServ_2022_x64.iso --user=sio
```
![Proxmox ISOs](/Proxmox-1/Img/Pr-1_ISO-2.png?raw=true "Proxmox wget ISOs")
4. Vérifiez que les ISOs sont bien présentes
```sh
ls
```
![Proxmox ISOs](/Proxmox-1/Img/Pr-1_ISO-3.png?raw=true "Proxmox ls ISOs")

### Installation Suivante

* [PfSense 1](/Proxmox-1/PfSense-1/README.md)
* [Windows Server 2022 Standard 1](/Proxmox-1/Windows-1/README.md)
* [Debian 11 1](/Proxmox-1/Debian-1/README.md)
* [Proxmox VE 2](/Proxmox-2/README.md)

## Roadmap

* Ajouter l'alternative des ISOs sur une clé USB

## License

Distribué sous la license WTFPL. Voir [WTFPL](http://www.wtfpl.net/about/) pour plus d'information.