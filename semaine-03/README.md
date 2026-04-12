## 🎯 Objectif de la semaine
Comprendre et diagnostiquer les services Linux via **systemd**, analyser les logs avec **journald**, et utiliser les fichiers de logs classiques.

---

## 1. Vérifier l’état d’un service (systemd)

### Commandes essentielles
```bash
systemctl status <service>
systemctl start <service>
systemctl stop <service>
systemctl restart <service>
systemctl enable --now <service>
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
journalctl -u <service>
journalctl -u <service> -b
journalctl -u <service> -f
journalctl -p err -u <service>
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
tail -n 50 /var/log/syslog
grep -i error /var/log/syslog
less /var/log/auth.log
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
systemctl status ssh
journalctl -u ssh -b -n 50
sshd -t
nano /etc/ssh/sshd_config
systemctl restart ssh
ss -tulpn | grep ssh
```

---

## 📦 Livrable
- \`diagnostic-linux.md\` (fiche professionnelle de diagnostic)
EOF
