# Se connecter depuis un terminal unix

* Pour vous connecter à votre environnement de travail EXPLOR, lancez depuis le terminal :

	```
	$ ssh -p votre_port_de_connexion votre_identifiant@193.54.9.82
	```

!!! note ""
	Afin d'éviter de devoir spécifier le port de connexion à chaque commande ```ssh```,```scp```,```rsync```,... nous recommandons l'utilisation d'un alias SSH


## Création d'un alias SSH
 
* Créer un fichier ```~/.ssh/config```  sur votre poste personnel et éditer le

```
Host meso-explor
	HostName 193.54.9.82
	Port votre_port_de_connexion
	User votre_identifiant
```

* Modifier les droits du fichier :

	```
	$ chmod 644 ~/.ssh/config
	```

    
* Vous pouvez maintenant vous connecter au mésocentre avec la commande suivante :

	```
	$ ssh meso-explor
	```


* Pour copier un dossier depuis votre poste de travail sur votre environnement de travail EXPLOR vous pouvez alors utiliser la commande :

	```
	$ scp -r dossier_posteperso meso-explor:.
	```

* au lieu de 


	```
	$ scp -r -P votre_port_de_connexion dossier_posteperso votre_identifiant@193.54.9.82:.
	```

## Modifier le mot de passe par défaut
Pour modifier le mot de passe lancer la commande :

```
$ passwd
```

!!! warning ""
	Merci de modifier votre mot de passe à votre première connexion


## Connexion sans mot de passe
Après avoir modifié votre mot de passe, vous pouvez également opter pour une connexion sans mot de passe à l'aide d'une clé d'authentification. 

* Depuis votre poste de travail personnel lancer la commande :

	```
	$ ssh-keygen -t rsa
	```
	
* appuyer deux fois sur entrée.



* Copier la clé publique générée sur votre environnement EXPLOR :

	```
	$ scp ~/.ssh/id_rsa.pub meso-explor:.ssh/authorized_keys
	```

Vous pouvez maintenant vous connecter depuis votre poste personnel sans entrer mot de passe.

