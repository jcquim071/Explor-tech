# Gaussian 
## Example of Gaussian Job Script : Run a Gaussian job for one day using the version (Gaussian/09/pgi) with 16 slurm tasks requested and one node ivy

This Example contains two parts:

 - First one contain example of Gaussian09 input file which includes several options importants such as number of processors for shared memory, and the amount of dynamic memory (kB, MB, and GB)
 - Second one contain example of Gaussian09 job script run for one day with 16 slurm tasks requested and one node ivy

### Example of Gaussian input file:

!!! note 
    Before submit a gaussian job, you should verify that the number of processors (```%NProcShared=16```) and the total number of slurm task requested (```#SBATCH -n 16```) are the same

    For the memory at Gaussian input file, it depend on the partition:

      * hf  : 15GB /core or 120GB/node
      * ivy : 3.2GB/core or  50GB/node
      * std : 3.2GB/core or 100GB/node

    Its important to know that hf and ivy partitions are better/faster for using Gaussian09

    Please don't forget to create the checkpoint file

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

### Example of Gaussian09 Job Script

```
#!/bin/bash
## Partition
#SBATCH -p ivy
## Number of nodes
#SBATCH -N 1
## Total number of slurm tasks requested
#SBATCH -n 16
## Name of a job
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
