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
      * [Configuration VLANs](#Configuration-VLANs)
      * [Configuration DHCP](#Configuration-DHCP)
      * [Configuration Firewall](#Configuration-Firewall)
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
</br>![PfSense Website](/Img/Pf/Pf_Rufus-1.png?raw=true "PfSense Website")
2. Téléchargez Rufus
</br>![Rufus Website](/Img/Rufus-2.png?raw=true "Rufus Website")
3. Branchez la clé USB sur le PC
4. Ouvrir Rufus
</br>![Rufus](/Img/Rufus-3.png?raw=true "Rufus")
6. Sélectionnez la clé USB
</br>![Rufus USB](/Img/Rufus-4.png?raw=true "Rufus USB")
5. Sélectionnez l'ISO de PfSense, continuez si vous avez une erreur "ISOHybrid"
</br>![Rufus ISO error](/Img/Rufus-5.png?raw=true "Rufus ISO error")
</br>![Rufus ISO](/Img/Pf/Pf_Rufus-6.png?raw=true "Rufus ISO")
7. Lancez le formatage
- NEED 2 IMAGES
</br>![Rufus Format](/Img/Pf/Pf_Rufus-7.png?raw=true "Rufus Format")
</br>![Rufus End](/Img/Pf/Pf_Rufus-8.png?raw=true "Rufus End")

#### Système

1. Branchez la clé USB sur le serveur
2. Démarrez le serveur
3. Appuyez sur F11 pour accéder au boot menu
4. Sélectionnez la clé USB
</br>![BIOS USB](/Img/Bios_USB.png?raw=true "BIOS USB")
5. Faites entrer pour démarrer l'installation
</br>![PfSense Install Start](/Img/Pf/Pf_Install-1.png?raw=true "PfSense Install Start")
6. Sélectionnez "Install"
</br>![PfSense Install](/Img/Pf/Pf_Install-2.png?raw=true "PfSense Install")
7. Sélectionnez le clavier "Auto (ZFS)"
</br>![PfSense Install ZFS](/Img/Pf/Pf_Install-3.png?raw=true "PfSense Install ZFS")
8. Faites entrer pour valider la configuration une fois le pfSense renommé (ici "Pf-WAN")
</br>![PfSense Install Conf](/Img/Pf/Pf_Install-4.png?raw=true "PfSense Install Conf")
9. Sélectionnez "Stripe"
</br>![PfSense Install Stripe](/Img/Pf/Pf_Install-5.png?raw=true "PfSense Install Stripe")
10. Sélectionnez votre disque (touche espace pour sélectionner), ici "da0"
</br>![PfSense Install Disk](/Img/Pf/Pf_Install-6.png?raw=true "PfSense Install Disk")
11. Sélectionnez "Yes"
</br>![PfSense Install Format](/Img/Pf/Pf_Install-7.png?raw=true "PfSense Install Format")
12. L'installation commence, sélectionnez "Reboot" une fois terminé
</br>![PfSense Installing](/Img/Pf/Pf_Install-8.png?raw=true "PfSense Installing")
</br>![PfSense Install Reboot](/Img/Pf/Pf_Install-9.png?raw=true "PfSense Install Reboot")

#### Configuration Interne

0. Laissez le serveur démarrer
1. Faites "a" pour détecter automatiquement l'inteface WAN et LAN, en cas d'erreur, sélectionnez les manuellement
2. Appuyez sur 2 pour configurer l'interface WAN
</br>![PfSense Conf IntWAN](/Img/Pf/Pf_Conf-1.png?raw=true "PfSense Conf IntWAN")
3. Sélectionnez l'interface WAN avec le numéro correspondant (ici 1)
</br>![PfSense Conf WAN](/Img/Pf/Pf_Conf-2.png?raw=true "PfSense Conf WAN")
4. Faites "y" pour configurer l'interface WAN en DHCP pour l'IpV4
5. Faites de même pour l'IpV6
</br>![PfSense Conf WAN DHCP](/Img/Pf/Pf_Conf-3.png?raw=true "PfSense Conf WAN DHCP")
6. Si demandé, refusez l'http pour le webconfigurator
</br>![PfSense Conf WebConf](/Img/Pf/Pf_Conf-4.png?raw=true "PfSense Conf WebConf")
7. Faites "Entrer" pour valider la configuration
8. Appuyez sur 2 pour configurer l'interface LAN
9. Sélectionnez l'interface LAN avec le numéro correspondant (ici 2)
</br>![PfSense Conf LAN](/Img/Pf/Pf_Conf-5.png?raw=true "PfSense Conf LAN")
10. Faites "n" pour configurer l'interface LAN en statique pour l'IpV4
11. L'adresse LAN est 192.168.1.254
12. Le masque est 24
13. Faites "Entrer" pour la Gateway car c'est le serveur PfSense lui-même
</br>![PfSense Conf LAN Static](/PfSense-WAN/Img/Pf-WAN_Conf-6.png?raw=true "PfSense Conf LAN Static")
15. Faites "y" pour configurer l'interface LAN en DHCP pour l'IpV6, la raison étant que nous n'en avons pas besoin dans cette infra
16. Faites "y" pour configurer le serveur DHCP pour l'IpV4
</br>![PfSense Conf LAN DHCP4](/Img/Pf/Pf_Conf-7.png?raw=true "PfSense Conf LAN DHCP4")
17. L'adresse de départ est 192.168.1.1
18. L'adresse de fin est 192.168.1.5
19. Faites "Entrer" pour valider la configuration
</br>![PfSense Conf LAN Range](/PfSense-WAN/Img/Pf-WAN_Conf-8.png?raw=true "PfSense Conf LAN Range")

#### Configuration GUI

1. Connectez un ordinateur au port LAN du serveur
2. Ouvrez un navigateur
3. Allez sur l'adresse https://192.168.1.1/
4. Acceptez et continuez malgré le certificat invalide
</br>![PfSense Gui Certif](/PfSense-WAN/Img/Pf-WAN_Gui-1.png?raw=true "PfSense Gui Certif")
4. Connectez-vous avec les identifiants par défaut (admin/pfsense)
</br>![PfSense Gui Connect](/PfSense-WAN/Img/Pf-WAN_Gui-2.png?raw=true "PfSense Gui Connect")
5. Faites "Next"
</br>![PfSense Gui Startup2](/Img/Pf/Pf_Gui-3.png?raw=true "PfSense Gui Startup2")
6. Faites "Next"
</br>![PfSense Gui Startup3](/Img/Pf/Pf_Gui-4.png?raw=true "PfSense Gui Startup3")
7. Remplissez les informations :
  * "Pf-WAN" pour le hostname
  * "1.1.1.1" pour le DNS principal
  * "8.8.8.8" pour le DNS secondaire
8. Faites "Next"
</br>![PfSense Gui Host](/PfSense-WAN/Img/Pf-WAN_Gui-5.png?raw=true "PfSense Gui Host")
9. Séléctionnez votre fuseau horaire (ici Europe/Paris)
10. Faites "Next"
</br>![PfSense Gui Date/Time](/Img/Pf/Pf_Gui-6.png?raw=true "PfSense Gui Date/Time")
11. Faites "Next", aucune modification n'est nécessaire pour le WAN
</br>![PfSense Gui WAN1](/PfSense-WAN/Img/Pf-WAN_Gui-7.png?raw=true "PfSense Gui WAN1")
</br>![PfSense Gui WAN2](/PfSense-WAN/Img/Pf-WAN_Gui-8.png?raw=true "PfSense Gui WAN2")
12. Faites "Next", aucune modification n'est nécessaire pour le LAN
</br>![PfSense Gui LAN](/PfSense-WAN/Img/Pf-WAN_Gui-9.png?raw=true "PfSense Gui LAN")
13. Changez le mot de passe de l'admin (ici "admin")
14. Faites "Next"
</br>![PfSense Gui Passwd](/Img/Pf/Pf_Gui-10.png?raw=true "PfSense Gui Passwd")
15. Faites "Reload" et attendez que le serveur redémarre
</br>![PfSense Gui Reload](/Img/Pf/Pf_Gui-11.png?raw=true "PfSense Gui Reload")
16. Une fois la page rechargée, faites "Check for updates" si l'ISO utilisée est ancienne, sinon faites "Finish"
</br>![PfSense Gui Update](/Img/Pf/Pf_Gui-12.png?raw=true "PfSense Gui Update")
17. Acceptez les conditions d'utilisation
</br>![PfSense Gui Notice](/Img/Pf/Pf_Gui-13.png?raw=true "PfSense Gui Notice")
18. Faites "Close"
</br>![PfSense Gui End](/Img/Pf/Pf_Gui-14.png?raw=true "PfSense Gui End")

#### Configuration Interfaces

##### Configuration VLANs

1. Connectez un ordinateur au port LAN du serveur
2. Ouvrez un navigateur
3. Allez sur l'adresse https://192.168.1.1/
4. Connectez-vous avec les identifiants défini (ici admin/admin)
</br>![PfSense Gui Connect](/PfSense-WAN/Img/Pf-WAN_Gui-2.png?raw=true "PfSense Gui Connect")
5. Allez dans "Interfaces" > "Assignments"
</br>![PfSense Gui Interfaces](/PfSense-WAN/Img/Pf-WAN_Int-1.png?raw=true "PfSense Gui Interfaces")
6. Allez dans "VLANs"
</br>![PfSense Gui VLANs](/PfSense-WAN/Img/Pf-WAN_Int-2.png?raw=true "PfSense Gui VLANs")
7. Cliquez sur "Add"
</br>![PfSense Gui VLANs Add](/PfSense-WAN/Img/Pf-WAN_Int-3.png?raw=true "PfSense Gui VLANs Add")
8. Sélectionnez l'interface LAN (ici em0)
9. Entrez le VLAN (ici 100)
10. Entrez une description (ici "Serv1 Light-Snoop")
11. Faites "Save"
</br>![PfSense Gui VLANs Add 100](/PfSense-WAN/Img/Pf-WAN_Int-4.png?raw=true "PfSense Gui VLANs 100")
12. Cliquez sur "Add"
</br>![PfSense Gui VLANs Add 2](/PfSense-WAN/Img/Pf-WAN_Int-5.png?raw=true "PfSense Gui VLANs Add 2")
13. Sélectionnez l'interface LAN (ici em0)
14. Entrez le VLAN (ici 200)
15. Entrez une description (ici "Serv2 Light-Snoop")
16. Faites "Save"
</br>![PfSense Gui VLANs Add 200](/PfSense-WAN/Img/Pf-WAN_Int-6.png?raw=true "PfSense Gui VLANs 200")
17. Allez dans "Interfaces Assignments"
</br>![PfSense Gui Interfaces Assignments](/PfSense-WAN/Img/Pf-WAN_Int-7.png?raw=true "PfSense Gui Interfaces Assignments")
18. Faites "Add"
</br>![PfSense Gui Int Add 100](/PfSense-WAN/Img/Pf-WAN_Int-8.png?raw=true "PfSense Gui Int Add 100")
19. Faites à nouveau "Add"
</br>![PfSense Gui Int Add 200](/PfSense-WAN/Img/Pf-WAN_Int-9.png?raw=true "PfSense Gui Int Add 200")
20. Cliquez sur l'interface OPT1 (VLAN 100)
</br>![PfSense Gui Int OPT1](/PfSense-WAN/Img/Pf-WAN_Int-10.png?raw=true "PfSense Gui Int OPT1")
21. Activez l'interface
22. Renommez l'interface (ici "Vlan 100")
22. Passez l'IPv4 en statique
23. Entrez l'adresse IP (ici 192.168.100.254)
24. Précisez le masque (ici 24)
25. Faites "Save"
</br>![PfSense Gui Int OPT1 Conf](/PfSense-WAN/Img/Pf-WAN_Int-11.png?raw=true "PfSense Gui Int OPT1 On")
26. Retournez dans "Interfaces" > "Assignments"
</br>![PfSense Gui Interfaces Assignments 2](/PfSense-WAN/Img/Pf-WAN_Int-12.png?raw=true "PfSense Gui Interfaces Assignments 2")
20. Cliquez sur l'interface OPT2 (VLAN 200)
</br>![PfSense Gui Int OPT2](/PfSense-WAN/Img/Pf-WAN_Int-13.png?raw=true "PfSense Gui Int OPT2")
21. Activez l'interface
22. Renommez l'interface (ici "Vlan 200")
22. Passez l'IPv4 en statique
23. Entrez l'adresse IP (ici 192.168.200.254)
24. Précisez le masque (ici 24)
25. Faites "Save"
</br>![PfSense Gui Int OPT2 Conf](/PfSense-WAN/Img/Pf-WAN_Int-14.png?raw=true "PfSense Gui Int OPT2 On")

##### Configuration DHCP

1. Allez dans "Services" > "DHCP Server"
</br>![PfSense Gui DHCP](/PfSense-WAN/Img/Pf-WAN_DHCP-1.png?raw=true "PfSense Gui DHCP")
2. Allez dans "OPT1"
</br>![PfSense Gui DHCP OPT1](/PfSense-WAN/Img/Pf-WAN_DHCP-2.png?raw=true "PfSense Gui DHCP OPT1")
3. Activez le serveur DHCP
4. Entrez le range d'adresse (ici 192.168.100.1 - 192.168.100.5)
5. Faites "Save"
</br>![PfSense Gui DHCP OPT1 Conf](/PfSense-WAN/Img/Pf-WAN_DHCP-3.png?raw=true "PfSense Gui DHCP OPT1 Conf")
6. Allez dans "OPT2"
</br>![PfSense Gui DHCP OPT2](/PfSense-WAN/Img/Pf-WAN_DHCP-4.png?raw=true "PfSense Gui DHCP OPT2")
7. Activez le serveur DHCP
8. Entrez le range d'adresse (ici 192.168.200.1 - 192.168.200.5)
9. Faites "Save"
</br>![PfSense Gui DHCP OPT2 Conf](/PfSense-WAN/Img/Pf-WAN_DHCP-5.png?raw=true "PfSense Gui DHCP OPT2 Conf")

##### Configuration Firewall

1. Allez dans "Firewall" > "Rules"
</br>![PfSense Gui Rules](/PfSense-WAN/Img/Pf-WAN_Firewall-1.png?raw=true "PfSense Gui Rules")
2. Allez dans "OPT1"
</br>![PfSense Gui Rules OPT1](/PfSense-WAN/Img/Pf-WAN_Firewall-2.png?raw=true "PfSense Gui Rules OPT1")
3. Faites "Add"
</br>![PfSense Gui Rules OPT1 Add IPv4](/PfSense-WAN/Img/Pf-WAN_Firewall-3.png?raw=true "PfSense Gui Rules OPT1 Add IPv4")
4. Changer le "Protocol" en "Any"
5. Changer la "Source" en "OPT1 net"
6. Mettez "Default allow LAN to any rule" en description
7. Faites "Save"
</br>![PfSense Gui Rules OPT1 Add Conf IPv4](/PfSense-WAN/Img/Pf-WAN_Firewall-4.png?raw=true "PfSense Gui Rules OPT1 Add Conf IPv4")
8. Faites "Add"
</br>![PfSense Gui Rules OPT1 Add IPv6](/PfSense-WAN/Img/Pf-WAN_Firewall-5.png?raw=true "PfSense Gui Rules OPT1 Add IPv6")
9. Changer l' "Address Family" en "IPv6"
10. Changer le "Protocol" en "Any"
11. Changer la "Source" en "OPT1 net"
12. Mettez "Default allow LAN to any rule" en description
13. Faites "Save"
</br>![PfSense Gui Rules OPT1 Add Conf IPv6](/PfSense-WAN/Img/Pf-WAN_Firewall-6.png?raw=true "PfSense Gui Rules OPT1 Add Conf IPv6")
14. Allez dans "OPT2"
</br>![PfSense Gui Rules OPT2](/PfSense-WAN/Img/Pf-WAN_Firewall-7.png?raw=true "PfSense Gui Rules OPT2")
15. Faites "Add"
</br>![PfSense Gui Rules OPT2 Add IPv4](/PfSense-WAN/Img/Pf-WAN_Firewall-8.png?raw=true "PfSense Gui Rules OPT2 Add IPv4")
16. Changer le "Protocol" en "Any"
17. Changer la "Source" en "OPT2 net"
18. Mettez "Default allow LAN to any rule" en description
19. Faites "Save"
</br>![PfSense Gui Rules OPT2 Add Conf IPv4](/PfSense-WAN/Img/Pf-WAN_Firewall-9.png?raw=true "PfSense Gui Rules OPT2 Add Conf IPv4")
20. Faites "Add"
</br>![PfSense Gui Rules OPT2 Add IPv6](/PfSense-WAN/Img/Pf-WAN_Firewall-10.png?raw=true "PfSense Gui Rules OPT2 Add IPv6")
21. Changer l' "Address Family" en "IPv6"
22. Changer le "Protocol" en "Any"
23. Changer la "Source" en "OPT2 net"
24. Mettez "Default allow LAN to any rule" en description
25. Faites "Save"
</br>![PfSense Gui Rules OPT2 Add Conf IPv6](/PfSense-WAN/Img/Pf-WAN_Firewall-11.png?raw=true "PfSense Gui Rules OPT2 Add Conf IPv6")
26. Redémarrez le serveur PfSense pour que tout les changements soient pris en compte : "Diagnostics" > "Reboot"
</br>![PfSense Gui Reboot](/PfSense-WAN/Img/Pf-WAN_Firewall-12.png?raw=true "PfSense Gui Reboot")
27. Faites "Submit" pour confirmer le redémarrage
</br>![PfSense Gui Reboot YES](/PfSense-WAN/Img/Pf-WAN_Reboot.png?raw=true "PfSense Gui Reboot YES")

#### Configuration VPN

1. -

#### Configuration OSPF

1. -

### Installation Suivante

* [Switch](/Switch/README.md)

## Roadmap

* Ajout des sous-interfaces pour le LAN (192.168.100.0 et 192.168.200.0)
* Ajout VPN vers le LAN
* Ajout de routage OSPF entre les deux PfSense interne

## License

Distribué sous la license WTFPL. Voir [WTFPL](http://www.wtfpl.net/about/) pour plus d'information.