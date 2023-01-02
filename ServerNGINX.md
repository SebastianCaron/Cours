# SAE - Réseau et Web


Temps de lecture et maitrise : 15mins

# Sommaire

* [Consignes](#consignes)
* [Demarrer le serveur](#démarrer-le-serveur)
* [Arreter le serveur](#arreter-le-serveur)
* [Diffuser les pages d'un autre répertoire](#diffuser-les-pages-dun-autre-répertoire)
* [Changer le port TCP](#changer-le-port-tcp)
* [Se connecter à un copain]()

# Consignes :

Démonstration de l'installation d'un serveur sur les machines du groupe :
* un membre du groupe choisi au hasard active son serveur web
* les autres membres du groupe s'y connectent.

On demande aux membre du groupe de savoir :
* arrêter et démarrer le serveur
* diffuser des pages web qui se trouvent dans un autre répertoire
* changer le port TCP du serveur web
* si le serveur web utilisé n'est pas celui qui avait été choisi initialement, pourquoi ?

#
Vous avez décidé d’utiliser NGINX. Le serveur Web est téléchargeable depuis cette page : 
https://nginx.org/en/download.html
<center>
<img src="https://nginx.org/nginx.png" width="400">
</center>
Attaquons les consignes point par point.


# Démarrer le Serveur :
Lancez nginx.exe ( ou équivalent sur Mac )
<center>
<img src="https://sebastiancaron.fr/images/image7.png">
</center>
<br>
Sous Windows 11 : une Fenêtre va s’ouvrir. 
<br>
Sous Windows 10 : “Rien ne se passe”, le processus est visible depuis le gestionnaire des tâches.
<br>

<center>
<img src="https://sebastiancaron.fr/images/image8.png">
</center>

> Vérifiez que le serveur fonctionne en tapant localhost dans l’url de votre navigateur préféré. Une page devrait apparaître… Si rien ne se passe ou que vous avez un message d'erreur, le serveur ne s’est pas lancé.

## Exemple :

Fonctionne : 
<center>
<img src="https://sebastiancaron.fr/images/image4.png">
</center>
Ne fonctionne pas :
<center>
<img src="https://sebastiancaron.fr/images/image1.png">
</center>

# Arreter le Serveur :
Ouvrez un invite de commande et déplacez vous dans le dossier où se trouve nginx.exe.
> Rappel : Pour ouvrir un Invite de commande : [WIN] + [R] --> "cmd" --> [RETURN]
<center>
<img src="https://sebastiancaron.fr/images/image3.png" width="300">
</center>
<center>
<img src="https://sebastiancaron.fr/images/image2.png" width="400">
</center>

> Rappel : Pour vous déplacer dans un dossier : "cd" + répertoire
<center>
<img src="https://sebastiancaron.fr/images/image12.png">
</center>

Pour fermer le serveur, tapez nginx -s quit
## Exemple
<center>
<img src="https://sebastiancaron.fr/images/image6.png">
</center>

Pour vérifier que le serveur est fermé : tapez localhost et vérifiez que vous avez un message d'erreurs (voir la partie exemple [Démarrez un serveur](#exemple))

# Diffuser les pages d'un autre répertoire :
Allez dans le dossier conf puis ouvrez le fichier nginx.conf.
<center>
<img src="https://sebastiancaron.fr/images/image14.png">
</center>

Mettez le chemin relatif de votre dossier où se trouve la page a diffuser par rapport à l'endroit où se trouve nginx.exe à coté de root.
> Supprimez html

Mettez le nom de la page à côté de index.
> Supprimez index.html index.htm

## Exemple :

Chemin vers **MON** nginx.exe **(Ne mettez pas la même chose, ça ne fonctionnera pas).**<br>
`C:\Users\sebas\Desktop\nginx-1.22.1`

Chemin vers la page à diffuser:<br>
`C:\Users\sebas\Desktop`

Chemin relatif :<br>
`../`

**EXEMPLE DE FICHIER NGINX.CONF :**
<center>
<img src="https://sebastiancaron.fr/images/image10.png">
</center>
<center>
<img src="https://sebastiancaron.fr/images/image5.png">
</center>

> Rappel : N'oubliez pas de restart le serveur à chaque modificaton

# Changer le port TCP
Choisissez un nombre supérieur à **1024** et inférieur à **65535**<br>

Exemple:  **62120**

Mettez le port à côté de listen.
<center>
<img src="https://sebastiancaron.fr/images/image11.png">
</center>

Voilà c’est fait…
> Pour le tester ajoutez :**port** a la fin de l’url.

## Exemple :
<center>
<img src="https://sebastiancaron.fr/images/image13.png">
</center>

# Se connecter à un serveur

Mettez son adresse IP locale en url plus le port de connexion

> Rappel : Par défaut le port est 80 pour le HTTP et 443 pour le HTTPS
