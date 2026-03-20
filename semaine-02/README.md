# Semaine 2 – Utilisateurs, sudo, SSH et Firewall UFW

## 🎯 Objectifs
- Créer un utilisateur non-root pour travailler en sécurité
- Lui attribuer les droits sudo
- Configurer le service SSH (permet de se connecter à sa VM Debian depuis un autre ordinateur, empêcher root de se connecter en SSH, protéger la connexion)
- Installer et activer le firewall UFW (bloquer les ports, protéger le serveur)
- Vérifier que tout fonctionne correctement

---

## 1. Mise à jour du système

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Gestion des utilisateurs

```bash
# Crée l'utilisateur et demande un mot de passe
sudo adduser admin

# Ajouter l'utilisateur au groupe sudo
sudo usermod -aG sudo admin
```
## 3. Configuration SSH

```bash
# Modifier la configuration SSH
sudo nano /etc/ssh/sshd_config

# Modifier ou ajouter les lignes suivantes pour désactiver la connexion root et autoriser l'authentification par mot de passe
PermitRootLogin no
PasswordAuthentification yes

# Redémarrer SSH
sudo systemctl restart sshd
```

## 4. Firewall UFW

```bash
# Installer UFW
sudo apt install ufw -y

# Autoriser SSH (port 22)
sudo ufw allow 22/tcp

# Activer le firewall
sudo ufw enable
```

## 5. Vérifications finales
```bash
id admin               # Vérifie l’existence de l’utilisateur
sudo -l                # Vérifie les droits sudo
systemctl status ssh   # Vérifie que SSH fonctionne
ufw status             # Vérifie les règles du firewall
```



