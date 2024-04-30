# Espaces de Stockage



**$HOMEDIR** : Espace commun à tous les utilisateurs d'un projet, y est inclus l'espace **$SHAREDIR** qui est un espace partagé entre l'ensemble des utilisateurs d'un projet.



**$SAVEDIR** : Espace de sauvegarde propre à chaque utilisateur.

**$SCRATCHDIR** : Espace de calcul temporaire utilisé exclusivement pendant la durée de vos traitements, les données seront automatiquement effacées au bout de 30 jours ou avant si la gestion de l'espace le nécessite. 

!!! warning ""
    En attendant la mise en place d'un système de fichier parallèle prévu pour début 2018, le **$SCRATCHDIR** est un répertoire local aux nœuds de calcul. 
    Les données présentes dans cet espace ne sont pas accessibles depuis l'espace utilisateur. Assurez-vous donc de copier les résultats de vos jobs sur votre espace utilisateur **$HOMEDIR**  dans votre script de soumission slurm ([voir exemples de scripts de soumission](slurm.md)) . 

|Espace de Stockage| Quota                   | Espace Partagé                       | Soumission de jobs depuis cet espace |Sauvegardé | Temporaire | 
|------------------|-------------------------|--------------------------------------|--------------------------------------|-----------|------------------|
|**$HOMEDIR**      | 1To extensible          | Non                                  | Oui (lent, déconseillé) | Non | Non
|**$SHAREDIR**     | inclus dans le **$HOMEDIR** | Oui (entre utilisateurs d'un projet) | Oui (lent,déconseillé)  | Non | Non | 
|**$SAVEDIR**      | 10Go                    | Non                                  | Non | Oui | Non |
|**$SCRATCHDIR**   | 800Go                   | Non                                  | Oui (rapide, conseillé) | Non | Oui |






