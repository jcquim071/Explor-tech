# Questions Fréquentes (FAQ)

## Général

!!! summary "Comment remercier EXPLOR dans mes publications ?"
    En mentionnant l’utilisation d’EXPLOR dans vos communications :
    
    * Les ressources en calcul ont été fournies en partie par le Mésocentre EXPLOR hébergé par l’Université de Lorraine *
    
    * High Performance Computing resources were partially provided by the EXPLOR centre hosted by the Université de Lorraine *

!!! summary "Comment signaler à EXPLOR mes publications qui ont utilisé ses ressources ?"
    En envoyant une information à <explor-contact@univ-lorraine.fr> ou à son Directeur à <explor-dir@univ-lorraine.fr>.

## Connexion

!!! summary "Comment se connecter à EXPLOR ?"
    Vous pouvez vous connecter à votre compte utilisateur EXPLOR en utilisant SSH ou X2GO
    (-ssh; -x2go)

!!! summary "Je n’arrive pas à me connecter, qui dois-je contacter ?"
    En cas de problème de connexion, merci d’adresser un mail décrivant votre problème à <explor-support@univ-lorraine.fr>.

!!! summary "Qu'est-ce que X2Go ?"
    [x2go](graphique.md) est un logiciel qui permet d'accéder à distance à votre frontale d'accès EXPLOR de manière graphique (bureau) via une connexion ssh. Il est disponible en tant que client sous Windows, Linux et MacOS. Pour plus d'informations, vous pouvez vous réferrer au site [http://wiki.x2go.org/doku.php/download:start](http://wiki.x2go.org/doku.php/download:start).

!!! summary "Comment transférer mes fichiers vers/depuis EXPLOR ?"
    Il existe deux possibilités pour transférer vos données. Elles sont détaillées sur [la page suivante](transfert.md).

!!! summary "Pourquoi ma machine d’accès s’appelle-t-elle `vm-XXX` ?"
    Afin de garantir la confidentialité des utilisateurs, serveurs virtuels, projets et ressources, les comptes utilisateurs et les projets ont été anonymisés.

!!! summary "Est-ce que j’ai accès à internet depuis EXPLOR ?"
    Depuis votre environnement de travail (frontale d'accès), vous avez accès à internet. Par contre, les nœuds de calcul ne peuvent communiquer avec l'extérieur d'EXPLOR.

!!! summary "Je suis rattaché à deux projets, pourquoi mes paramètres de connexion sont-ils différents ?"
    Chaque projet dispose de son environnement propre (et anonymisé), accessible via une machine virtuelle dédiée (frontale d'accès). Les paramètres de connexion sont donc différents pour chaque projet.

!!! summary "Je suis rattaché à deux projets, comment puis-je transfèrer mes données d’un projet à l’autre ?"
    Les procédures relatives au transfert de données entre deux projets sont expliquées à [la page suivante](transfert.md).


!!! summary "Comment utiliser les serveurs que j’ai achetés depuis mon projet ?"
    Un mode opératoire vous sera adressé à l'installation de vos serveurs qui vous expliquera comment accéder à vos serveurs sous [SLURM](https://slurm.schedmd.com/).

## Utilisation des ressources
!!! summary "Comment soumettre un job ?"
    Depuis votre environnement, vous pourrez utiliser le gestionnaire de travaux SLURM pour soumettre vos travaux.
    Merci de consulter la documentation mis à votre disposition à [Soumission de job](http://explor-tech.univ-lorraine.fr/fr/slurm/). 

!!! summary "Comment se connecter en interactif sur un nœud de calcul ?"
    Par une réservation du nœud à travers la commande salloc
    Par exemple, si vous voulez demander un nœud de la partition std pendant 1 heure taper : 
    salloc -N1 -p std -t 1 : 00 : 00 srun –pty bash

!!! summary "Quelle partition choisir ? "
    En fonction du type de travaux et de vos besoins en ressources (CPU, mémoire, GPU, etc), vous serez amené à préférer une partition ou une autre.
    L'ensemble des partitions est décrit à la page: [Ressources de calcul disponibles](materiel.md).

    De manière générale : 

    * la partition hf est réservée aux travaux séquentielles ou peu parallèles (1 à 8 cœurs maximum). 
    * les partitions std et sky donnent accès à des nœuds de 32 cœurs reliés par un réseau basse latence et sont adaptés aux travaux parallèles (de 32 à 1024 cœurs). 
    * les partitions p100 et gtx sont adaptés aux travaux nécessitant des GPUs.

    En cas de doute, vous pouvez envoyer un mail au support à l’adresse <explor-support@univ-lorraine.fr>.
 
!!! summary "Quel temps de calcul dois-je indiquer dans mon script ?"
    Le temps de calcul maximal qui peut vous être alloué dépend de la partition et du nombre de nœuds que vous choississez. 

    Voir [Ressources de calcul disponibles](http://explor-tech.univ-lorraine.fr/fr/materiel/#limitations-en-ressources-dun-utilisateur/). 

    Nous vous conseillons de spécifier au mieux votre demande afin de permettre au gestionnaire SLURM d'optimiser l'utilisation des ressources.

!!! summary "Le job que j'ai soumis n'a pas démarré, il reste dans la file d'attente. Pourquoi ? "
 
    La commande squeue va vous donner le statut de votre job (dernière colonne « REASON »). Votre job en attente peut être en statut :

    * Ressources : votre job va bientôt démarrer, SLURM est en train de réserver la ressource nécessaire à son exécution
    * Priority : un ou plusieurs autres job sont avant vous dans la file d'attente
    * QOSGrpJobsLimit : des limites sont associés à chaque partition, projet ou utilisateur en fonction des ressources demandées. 

    Ces limites sont définies à [la page suivante](http://explor-tech.univ-lorraine.fr/fr/materiel/#limitations-en-duree-et-en-ressources-dun-job). 

    Votre job changera de statut lorsque ces limites ne seront plus atteintes.

!!! summary "Le job que j'ai soumis est en attente, quand va-t-il démarrer ?"
    L'option ```--start``` de la commande squeue peut vous donner une estimation de l'heure à laquelle SLURM pense que votre job démarrera.

!!! summary "A la soumission de mon job, j'ai l'erreur suivante : Could not select QOS, please verify resources selected ? "
    Dans votre fichier de soumission SLURM, les paramètres que vous avez spécifiés (partition, nombre de nœuds, temps de calcul, etc.) sont incorrects. 

    Vous pouvez consulter la documentation technique [Ressources de calcul](http://explor-tech.univ-lorraine.fr/fr/materiel/) et [soumission de job](http://explor-tech.univ-lorraine.fr/fr/materiel/) pour vérifier la compatibilité de vos paramètres.

!!! summary "sbatch: error: Batch job submission failed: Invalid qos specification ? "
    `Invalid qos specification` signifie que vous avez demandé une ressource à laquelle vous n’avez pas accès. 

    Pour plus d'informations, vous pouvez visiter [la page suivante](http://explor-tech.univ-lorraine.fr/fr/materiel/#limitations-en-ressources-dun-utilisateur/).

!!! summary "A quoi sert la commande module ? "
    La commande module permet de charger dans l'environnement utilisateur des logiciels, des compilateurs, etc. Pour plus d'informations sur l'utilisation de la commande module, vous pouvez vous réferrer à [la page suivante](http://explor-tech.univ-lorraine.fr/fr/module/). 

!!! summary "Est-ce que python est installé dans EXPLOR ? "
    Plusieurs versions de python sont installées dans EXPLOR. Elles sont accessibles via la commande 'module' :

    * python2 via la commande `module load anaconda/2`
    * python3 via la commande `module load anaconda/3`
    * les versions spécifiques optimisées par Intel, via les commandes `module load python/versionX/intel`

!!! summary "Mon logiciel a besoin de ressources GPU, comment puis-je spécifier ce besoin à SLURM ? "
    Dans votre script de soumission, il faut tout d'abord choisir une partition possédant des GPUs [p100, gtx ou k20](http://explor-tech.univ-lorraine.fr/fr/materiel/), puis préciser le nombre de GPUs requis en renseignant l'option –gres de la commande sbatch (ex. : --gres=gpu:2 pour demande 2 GPUs).

