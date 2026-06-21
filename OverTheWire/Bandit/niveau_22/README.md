# Bandit — Niveau 21 → 22

## 📌 Informations
- **Plateforme :** OverTheWire
- **Série :** Bandit
- **Niveau :** 21 → 22
- **Difficulté :** Débutant
- **Date :** 20/06/2026

---

## 🎯 Objectif.  
Un programme est exécuté automatiquement à intervalles réguliers depuis cron, le planificateur de tâches basé sur le temps. Regardez dans /etc/cron. d/ pour la configuration et voir quelle commande est en cours d’exécution.  

  ---

## 🔍 Réflexion avant de commencer.  
trouvons un moyen de trouver le mot de passe depuis le programme cron



---

## 🛠️ Commandes données en indice

| Commande | Rôle |
|---|---|
| `man` | Permet de consulter la documentation d'une commande spécifique, il suffit de saisir man suivi du nom de la commande |
| `diff` | permet de comparer deux fichiers texte ligne par ligne.|
| `ncat` | permet de lire et d'écrire des données à travers le réseau en utilisant les protocoles TCP ou UDP. |
| `uniq` | Permet de filtrer les lignes répétées d'un fichier texte ou d'une entrée standard. |
| `strings` | Permet de rechercher et d'extraire des séquences de caractères lisibles (texte) dans des fichiers binaires ou des exécutables. |
| `base64` | Base64 est un système de codage utilisé pour convertir des données binaires en format texte en les encodant en une représentation en base 64.|

---



## 📖 Résolution

### Étape 1 — Connexion au serveur

```bash
ssh bandit21@bandit.labs.overthewire.org -p 2220
```


### Étape 2 — 

```bash
ls /etc/cron.d/
```

Résultat :
```
behemoth4_cleanup  cronjob_bandit23  leviathan5_cleanup    sysstat
clean_tmp          cronjob_bandit24  manpage3_resetpw_job
cronjob_bandit22   e2scrub_all       otw-tmp-dir


```


### Étape 3 — 
#

```bash
cat /etc/cron.d/cronjob_bandit22
```

Résultat :
```
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null


```  
```bash  
cat /usr/bin/cronjob_bandit22.sh
```  
Résultat :  
```
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

```  
### NB  
**Remarque :** le script montre que le mot de passe du niveau 22 est envoyé dans /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

```bash  
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```  
Résultat :  
```
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```
## Visuel
![image](images/a.png)  


## 🚩 Flag obtenu
```
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```  



---

## 💡 Ce que j'ai appris.  
 cron est le planificateur de tâches standard de Linux. Son rôle est d'exécuter automatiquement des scripts, commandes ou programmes en arrière-plan à une date, une heure ou un cycle récurrent défini. L'outil qui permet de configurer ces tâches s'appelle crontab.  

---

## 🔗 Références
- [Page officielle Bandit](https://overthewire.org/wargames/bandit/)