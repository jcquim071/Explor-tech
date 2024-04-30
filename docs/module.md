# Les Modules

Les modules sont des fichiers de configuration qui contiennent des instructions afin de modifier votre environnement logiciel. Un fichier module contient les informations nécessaires pour rendre disponible une application ou une bibliothèque dans la session de l'utilisateur.

Les modules sont gérés par le logiciel [Lmod 7.4](https://www.tacc.utexas.edu/research-development/tacc-projects/lmod).


# Lister les modules installés

La commande ```$ module available``` ou  ```$ module av``` ou bien encore ```$ ml av``` liste les modules actuellement disponibles.

```
[dpena@vm-gce17 gce17]$ module available

--------------------------------------------- /opt/modulefiles/compilers ----------------------------------------------
   gcc/4.9.4 (D)    gcc/5.4.0    gcc/6.3.0    intel/2017.1.132    pgi/16.10

------------------------------------------------ /opt/modulefiles/mpi -------------------------------------------------
   intelmpi/2017.1.132    openmpi/2.1.0/gcc-4.9.4 (D)    openmpi/2.1.0/intel17    openmpi/2.1.0/pgi-16

--------------------------------------------- /opt/modulefiles/libraries ----------------------------------------------
   hypre/2.10.0b    metis/4.0.3    mkl/2017.1.132

------------------------------------------------ /opt/modulefiles/apps ------------------------------------------------
   quantum-espresso/5.3.0/intel17    quantum-espresso/6.0/intel17    vasp/5.4.1/intel17

----------------------------------------------- /opt/modulefiles/tools ------------------------------------------------
   advisor/2017.1.1.486553    idb/2017    inspector/2017.1.1.484836    vtune-amp/2017.1.0.486011

  Où:
   D:  Default Module

Utilisez "module spider" pour trouver tous les modules possibles.
Utilisez "module keyword key1 key2 ..." pour chercher tous les modules possibles qui correspondent à l'une des clés
(key1, key2).
```

# Opérations sur les modules
## Charger un module
Pour charger un module, par exemple le compilateur gcc dans sa version 6.9.3 il suffit de lancer la commande :

```
$ module load gcc/6.3.0
```


Pour charger le compilateur intel, les librairies MPI intel et mkl lancer la commande :

```
$ module load intel intelmpi mkl
```

!!! note ""
    Vous pouvez rajouter une commande module load  dans votre ```~/.bashrc```. Les modules seront alors automatiquement chargés à votre connexion.


## Décharger un module

Pour enlever un module de votre environnement, par exemple le module ```gcc/6.3.0``` lancer la commande :

```
$ module unload gcc/6.3.0
```

## Décharger tous les modules

Pour décharger tous les modules de votre environnement lancer la commande :

```
$ module purge
```

## Lister les modules chargés

Pour lister les modules actuellement chargés lancer la commande ```$ module list``` :

```
[dpena@vm-gce17 gce17]$ module list

Currently Loaded Modules:
  1) intel/2017.1.132      3) mkl/2017.1.132   5) hypre/2.10.0b
  2) intelmpi/2017.1.132   4) metis/4.0.3      6) advisor/2017.1.1.486553

``` 


