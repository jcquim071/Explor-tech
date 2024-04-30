# Gaussian 
## Exemple de script de job en Gaussian : Lancer une tache en gaussian pendant une journee en utilisant la version (Gaussian/09/pgi) avec 16 taches de slurm demandees et un Noeud ivy

Cet exemple comprend deux parties :

 - Le premier contient un exemple de fichier d'entree de Gaussian09 qui inclut plusieurs options importantes telles que le nombre de processeurs pour la memoire partagee, et la quantite de memoire dynamique (KB, MB, et GB)

 - Le second contient un exemple de script de job Gaussian09 execute pendant une journee avec 16 taches de slurm demandees et un noeud ivy


### Exemple de fichier d'entree (input) Gaussian :

!!! note 
    Avant de soumettre un job de Gaussian, vous devez verifier que le nombre de processeurs (%NProcShared=16) et le nombre total de taches de slurm demandees (#SBATCH -n 16) sont les memes     
    
    Pour la memoire du fichier d'entree gaussien, cela depend de la partition :

      * hf  : 15GB /coeur ou 120GB/noeud
      * ivy : 3.2GB/coeur ou  50GB/noeud
      * std : 3.2GB/coeur ou 100GB/noeud

     Il est important de savoir que les partitions hf et ivy sont meilleures/plus rapides pour utiliser Gaussian09

     Veuillez ne pas oublier de creer le fichier checkpoint

```
%NProcShared=16
%Mem=
%Chk=myfile.chk
# HF 6-31G* OPT

Title

0 1
O    x y z
H    x y z
H    x y z

```

### Exemple de script de job de Gaussian09

```
#!/bin/bash
## Partition
#SBATCH -p ivy
## Nombre de noeuds
#SBATCH -N 1
## Nombre de taches demandes
#SBATCH -n 16
## Nom du job
#SBATCH -J NAME
## Time of a job
#SBATCH -t 1-00:00:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=votremail@univ-lorraine.fr

## Unload all modules
module purge
## Loads module gaussian/09/pgi
module load gaussian/09/pgi

## Standard input file
G09COM=myfile.gjf
## Standard output file
G09LOG=myfile.log
## Standard check File
G09CHK=myfile.chk

hostname

## Set up the temporary directory in $SCRATCHDIR
curdir=$PWD
tmpdir=$SCRATCHDIR/$$
mkdir -p ${tmpdir}
cd ${tmpdir}

## Run the program with the working directory
g09 < $curdir/${G09GJF} > $curdir/${G09LOG}

if [ -e $G09CHK ]; then
  mv $G09CHK $curdir/
fi
```
