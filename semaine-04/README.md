# Semaine 4 - Installation de Proxmox VE dans une VM

## 1. Objectif
Installer Proxmox VE dans une machine virtuelle afin de comprendre :
- Comment Proxmox remplace un OS classique
- Comment fonctionne l'installation
- Comment accéder à l'interface web
- Comment vérifier que tout fonctionne

---

## 2. Téléchargement de l'ISO Proxmox

Aller sur :
https://www.proxmox.com/en/downloads

Télécharger :
Proxmox VE ISO Installer

---

## 3. Création de la VM

Paramètres recommandés :
- 4 Go RAM
- 2 vCPU (1 processeur virtuel + 2 cœurs)
- 32 Go de disque (pour avoir assez d'espace pour les logs, paquets, mises à jour, templates, ISO que l'on va importer
- BIOS ou UEFI
- Carte réseau en mode Bridge (vérifier qu'il ponte bien sur la carte réseau wi-fi)
- Monter l'ISO Proxmox en CD/DVD

---

## 4. Installation de Proxmox

Étapes :
1. Boot sur l'ISO

<img src="captures/boot.png" width="600">

2. Choisir Install Proxmox VE
3. Accepter la licence
4. Choisir le disque virtuel
5. Choisir pays / fuseau / clavier
6. Définir le mot de passe root
7. Configurer le réseau (IP ou DHCP)

<img src="captures/network.png" width="600">

8. Lancer l'installation

<img src="captures/install.png" width="600">

9. Redémarrer

---

## 5. Accès à l'interface web

Accéder via :
https://<IP-de-proxmox>:8006

Exemple dans mon cas :
https://192.168.1.50:8006

Connexion :
- utilisateur : root
- mot de passe : celui défini à l'installation
- realm : Linux PAM standard authentication (Debian)

<img src="captures/login.png" width="600">
<img src="captures/web_ui.png" width="600">

---

## 6. Vérifications après installation

```bash
pveversion -v                 # Vérifie la version de Proxmox
ip a                          # Vérifie l'adresse IP
systemctl status pvedaemon    # Vérifie le service principal Proxmox
systemctl status pveproxy     # Vérifie l'interface web
df -h                         # Vérifie le stockage
```
---

## 7. Notes d'installation

- Proxmox s'installe comme un OS complet
- L'interface web est accessible sur le port 8006
- L'utilisateur root sert à administrer Proxmox
- Dans notre cas la VM doit avoir une IP accessible depuis le PC 
- 32go permettent d'avoir suffisamment d'espace pour les logs, paquests, mises à jour, templates, ISO que l'on va importer
- Vérifier que la carte réseau en mode Bridge ponte bien sur la carte réseau wi-fi dans l'éditeur de réseau virtuel
