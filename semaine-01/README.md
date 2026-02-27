# Semaine 1 – Installation Debian + commandes de base

## Objectif
Installer Debian dans une VM et maîtriser les commandes de base d’un serveur Linux.

## 1. Création de la VM
- Hyperviseur : VMware
- 2 vCPU (1 processeur, 2 coeurs pour le multitâche), 2 Go RAM, 20 Go disque
- ISO : Debian 13

## 2. Installation (mode graphique)
1. Démarrer la VM sur l’ISO Debian.
2. Choisir « Graphical install ».
3. Langue : Français, Clavier : Français.
4. Nom de machine : `debian-lab`.
5. Nom de domaine : debian-lab.local
6. Partitionnement : Assisté – utiliser un disque entier.
7. Créer un utilisateur : `jmy`.
8. Terminer l’installation et redémarrer.
9. Changer la langue de Debian pour English (US), plus adapté pour la documentation

## 3. Commandes de base après installation

```bash
sudo apt update && sudo apt upgrade -y
uname -a
ip a
