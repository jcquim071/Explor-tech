# Slurm

[SLURM](https://slurm.schedmd.com/) est un job scheduler. Son rôle est de gérer la file d'attente et de lancer les calculs lorsque les ressources demandées sont disponibles.

## Les partitions

Les différents nœuds de calcul sont regroupés selon des partitions. Lors de la soumission d'un job, il faut choisir une partition.

Les partitions à disposition sont les suivantes :

*    std : Les nœuds standard en réseau basse latence Intel Omnipath 100GB/s.
*    hf  : Les nœuds hautes-fréquences en réseau 10GB/s.
*    ivy : Les nœuds génération Ivy-Bridge en réseau Infiniband 40GB/s
*    k20 : Les nœuds GPU Tesla K20m

Pour lister les partitions tapez la commande ```$ sinfo```

```
[cal01@vm-support01 explor-support]$ sinfo
PARTITION AVAIL    AVAIL_FEATURES   NODES   NODES(A/I/O/T) NODELIST
std          up BROADWELL,INTEL,H      16        1/15/0/16 cne[01-16]
std          up SKYLAKE,OPA,INTEL       8          1/7/0/8 cnf[01-08]
std          up CASCADELAKE,OPA,I       2          0/2/0/2 cnh[01-02]
std          up CASCADELAKE,IB,IN      28        5/23/0/28 cni[01-24,29-32]
std          up CASCADELAKE,IB,IN       8          0/8/0/8 cnk[01-08]
std          up      EPYC4,IB,AMD       2          0/2/0/2 cnl[02-03]
std          up SKYLAKE,OPA,INTEL      48       31/17/0/48 cnc[01-48]
std          up SKYLAKE,OPA,INTEL      12         3/9/0/12 cnc[53-64]
std          up IVY,IB,INTEL,NOPR      12         8/4/0/12 cnd[01-12]
std          up CASCADELAKE,OPA,I      12        2/10/0/12 cng[01-12]
std          up CASCADELAKE,IB,IN       4          3/1/0/4 cni[25-28]
std          up EPYC3,IB,AMD,NOPR      64       47/17/0/64 cnj[01-64]
std          up EPYC4,IB,AMD,NOPR       1          1/0/0/1 cnl01
std          up BROADWELL,OPA,INT     121     107/10/4/121 cna[02-17,19-39,41-64],cnb[01-08,10-12,14-52,54-55,57-64]
gpu          up CASCADELAKE,IB,RT       2          1/1/0/2 gpe[01-02]
gpu          up CASCADELAKE,L40,I       1          0/1/0/1 gpf01
gpu          up BROADWELL,OPA,P10       6          6/0/0/6 gpb[01-06]
gpu          up BROADWELL,OPA,GTX       4          3/1/0/4 gpc[01-04]
gpu          up CASCADELAKE,OPA,T       3          3/0/0/3 gpd[01-03]
(A/I/O/T): (allocated/idle/other/total)
```


## Lister les jobs soumis

Pour lister les jobs soumis taper la commande ```$ squeue```

```
[dpena@vm-gce17 ~]$ squeue 
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
              5220        hf PingPong    dpena PD       0:00      2 (Resources)
              5221        hf PingPong    dpena PD       0:00      2 (Priority)
              5222        hf PingPong    dpena PD       0:00      2 (Priority)
              5223        hf PingPong    dpena PD       0:00      2 (Priority)
              5224        hf PingPong    dpena PD       0:00      2 (Priority)
              5225        hf PingPong    dpena PD       0:00      2 (Priority)
              5226        hf PingPong    dpena PD       0:00      2 (Priority)
              5227        hf PingPong    dpena PD       0:00      2 (Priority)
              5228        hf PingPong    dpena PD       0:00      2 (Priority)
              5229        hf PingPong    dpena PD       0:00      2 (Priority)
              5230        hf PingPong    dpena PD       0:00      2 (Priority)
              5231        hf PingPong    dpena PD       0:00      2 (Priority)
              5212        hf PingPong    dpena  R       0:06      2 cne[01-02]
              5213        hf PingPong    dpena  R       0:06      2 cne[03-04]
              5214        hf PingPong    dpena  R       0:05      2 cne[05-06]
              5215        hf PingPong    dpena  R       0:03      2 cne[07-08]
              5216        hf PingPong    dpena  R       0:03      2 cne[09-10]
              5217        hf PingPong    dpena  R       0:03      2 cne[11-12]
              5218        hf PingPong    dpena  R       0:03      2 cne[13-14]
              5219        hf PingPong    dpena  R       0:03      2 cne[15-16]
```

en mode graphique, vous pouvez également taper la commande ```$ sview```.

## Soumission d'un job

Pour soumettre un job lancer la commande :

```
$ sbatch script.slurm
```
!!! note ""
    Avant de soumettre un job vous devez au préalable charger les modules nécessaires.


Quelques exemples de scripts de soumission :

### Exemple : calcul de 3 jours  mono-processeur

```
#!/bin/bash
## Partition
#SBATCH -p std
## Nombre de noeuds
#SBATCH -N 1  
## Nom du job
#SBATCH -J mono-proc
## Nombre de taches demandés
#SBATCH -n 1
#SBATCH -t 3-00:00:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=votremail@univ-lorraine.fr

module purge
module load gcc/7.1.0

## Creating temporary directory in $SCRATCHDIR
WORKDIR=$SCRATCHDIR/job.$SLURM_JOB_ID.$USER
mkdir -p $WORKDIR

## Copying files to $WORKDIR 
cp -rf input executable  $WORKDIR

## Moving to $WORKDIR
cd $WORKDIR
## Calculation
srun executable < input

## Copying back files to submit directory
cp -rf * $SLURM_SUBMIT_DIR/.
```


### Exemple : calcul de 8 jours et 30 min avec OpenMP sur 8 cœurs

```
#!/bin/bash
#SBATCH -N 1  
#SBATCH -p std
#SBATCH -J openmp
## Nombre de cpu par tache
#SBATCH -c 8
#SBATCH -t 8-00:30:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=votremail@univ-lorraine.fr

export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK

module purge
module load intel/2018.0.128 mkl/2018.0.128


## Creating temporary directory in $SCRATCHDIR
WORKDIR=$SCRATCHDIR/job.$SLURM_JOB_ID.$USER
mkdir -p $WORKDIR

## Copying files to $WORKDIR 
cp -rf input executable  $WORKDIR

## Moving to $WORKDIR
cd $WORKDIR
## Calculation
srun executable < input

## Copying back files to submit directory
cp -rf * $SLURM_SUBMIT_DIR/.
```

### Exemple : calcul de 15 jours et 3 heures avec MPI sur 2 nœuds, 32 cœurs chacun sur nœuds std

```
#!/bin/bash

#SBATCH -N 2  
#SBATCH -p std
#SBATCH -J mpi
## Nombre de taches demandés
#SBATCH -n 64 
## Nombre de taches demandés par nœud
#SBATCH --ntasks-per-node=32
#SBATCH -t 15-03
#SBATCH --mail-type=ALL
#SBATCH --mail-user=votremail@univ-lorraine.fr

module purge
module load intel/2018.0.128  intelmpi/2018.0.128 mkl/2018.0.128

## Creating temporary directory in $SCRATCHDIR
WORKDIR=$SCRATCHDIR/job.$SLURM_JOB_ID.$USER
mkdir -p $WORKDIR

## Copying files to $WORKDIR 
cp -rf input executable  $WORKDIR

## Moving to $WORKDIR
cd $WORKDIR
## Calculation
srun executable < input

## Copying back files to submit directory
cp -rf * $SLURM_SUBMIT_DIR/.
```


### Exemple : Calcul de 30min OpenMP + MPI sur 2x32 cœurs sur un nœud std

```
#!/bin/bash
#SBATCH -N 2  
#SBATCH -p std
#SBATCH -J openmp
#SBATCH --ntasks-per-node=1
#SBATCH -c 32
#SBATCH -t 30:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=votremail@univ-lorraine.fr

module purge
module load intel/2018.0.128  intelmpi/2018.0.128 mkl/2018.0.128
export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK

## Creating temporary directory in $SCRATCHDIR
WORKDIR=$SCRATCHDIR/job.$SLURM_JOB_ID.$USER
mkdir -p $WORKDIR

## Copying files to $WORKDIR 
cp -rf input executable  $WORKDIR

## Moving to $WORKDIR
cd $WORKDIR
## Calculation
srun executable < input

## Copying back files to submit directory
cp -rf * $SLURM_SUBMIT_DIR/.
```

### Exemple : Calcul de 30min MPI sur 8 cœurs et deux GPU sur un nœud gpu

```
#!/bin/bash
#SBATCH -N 1  
#SBATCH -p gpu
#SBATCH -J mpi+gpu
#SBATCH -n 8
#SBATCH --gres=gpu:2
#SBATCH -t 30:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=votremail@univ-lorraine.fr

module purge
module load intel/2018.0.128  intelmpi/2018.0.128 mkl/2018.0.128 cuda/8.0


## Creating temporary directory in $SCRATCHDIR
WORKDIR=$SCRATCHDIR/job.$SLURM_JOB_ID.$USER
mkdir -p $WORKDIR

## Copying files to $WORKDIR 
cp -rf input executable  $WORKDIR

## Moving to $WORKDIR
cd $WORKDIR
## Calculation
srun executable < input

## Copying back files to submit directory
cp -rf * $SLURM_SUBMIT_DIR/.
```

!!! note ""
    Si vous souhaitez utiliser la commande mpirun à la place de srun avec le module intelmpi il est nécessaire de rajouter dans vos scripts de soumission la commande : unset I_MPI_PMI_LIBRARY

## Annulation d'un job

Pour annuler un job soumis taper la commande ```$ scancel #JOBID```, ```#JOBID``` étant le numéro du job.



## Réservation interactive d'un nœud de calcul (pour compilation/débogage)
Nous conseillons de compiler vos codes sources sur les nœud de calcul afin de profiter de l'ensemble des optimisations et d'éviter de surcharger la frontale. 

Pour cela vous avez la possibilité de réserver un nœud et de vous y connecter en mode interactif.

Ex : pour demander un nœud de la partition std pendant 1 heure taper  :

```
[****@vm-gce17 ~]$ salloc -N1 -p std -t 1:00:00 srun --pty bash

```
```
****@cna01's password: 
Last login: Fri Apr 21 21:10:16 2017 from vm-gce17.prod.explor
[****@cna01 ~]$ 
```

Pour quitter le mode interactif, taper la commande ```$ exit``` :

```
[****@cna01 ~]$ exit
logout
Connection to cna01 closed.
salloc: Job allocation 5232 has been revoked.
```

