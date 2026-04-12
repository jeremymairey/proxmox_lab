# Semaine 3 - Diagnostic des services Linux

## Objectifs
- Comprendre et diagnostiquer les services Linux via **systemd**
- Analyser les logs avec **journald**
- Utiliser les fichiers de logs classiques.

---

## 1. Vérifier l’état d’un service (systemd)

### Commandes essentielles
```bash
systemctl status <service>        # Affiche l'état du service + derniers logs
systemctl start <service>         # Démarre le service
systemctl stop <service>          # Arrête le service
systemctl restart <service>       # Redémarre le service (après modification)
systemctl enable --now <service>  # Active au démarrage + démarre immédiatement
```

### Points à vérifier
- État : *active (running)* ou *failed*
- Service activé au démarrage
- Erreurs visibles dans le `status`
- Dépendances non démarrées

---

## 2. Lire les logs d’un service (journald)

### Commandes utiles
```bash
journalctl -u <service>           # Affiche tous les logs du service
journalctl -u <service> -b        # Logs du service depuis le dernier boot
journalctl -u <service> -n 50     # Affiche les 50 derniers logs
journalctl -u <service> -f        # Affiche les logs en temps réel
journalctl -u <service> -p err    # Affiche uniquement les erreurs
```

### Ce qu’on cherche
- erreurs de configuration  
- ports déjà utilisés  
- permissions manquantes  
- dépendances cassées  

---

## 3. Logs classiques dans /var/log

### Emplacements importants
- `/var/log/syslog`
- `/var/log/auth.log`
- `/var/log/kern.log`
- `/var/log/<service>/error.log`

### Commandes utiles
```bash
tail -n 50 /var/log/syslog        # Affiche les 50 dernières lignes du syslog
grep -i error /var/log/syslog     # Cherche les erreurs dans le syslog
less /var/log/auth.log            # Ouvre les logs d'authentification
```

---

## 4. Méthodologie de diagnostic (procédure rapide)

1. Vérifier l’état du service  
2. Lire les logs journald  
3. Tester la configuration (\`nginx -t\`, \`sshd -t\`)  
4. Vérifier permissions & ownership  
5. Vérifier le réseau (\`ss -tulpn\`, \`curl\`)  
6. Redémarrer et revérifier
---

## 5. Exemple concret : SSH qui ne démarre pas

### Étapes
```bash
systemctl status ssh                          # Vérifie l'état du service
journalctl -u ssh -b -n 50                    # Affiche les derniers logs SSH
sudo sshd -t                                  # Teste la configuration SSH
ls -l /etc/ssh/sshd_config                    # Vérifie permissions & ownership
sudo chown root:root /etc/ssh/sshd_config     # Corrige propriétaire
sudo chmod 600 /etc/ssh/sshd_config           # Corrige permissions
sudo nano /etc/ssh/sshd_config                # Modifie la configuration si nécessaire
sudo systemctl restart ssh                    # Redémarre le service
ss -tulpn | grep ssh                          # Vérifie que SSH écoute sur le port 22
```
