# Ressources de calcul

## Description des ressources de calcul disponibles
### Matériel EXPLOR

| Partition | Node-id      | Matériel      | CPU | GPU | # de nœud | # de cœurs / nœud   | # de cœurs total      | Mémoire dispo / nœud              | Mémoire par défaut / cœur | Réseau          | Mode Exclusif | Tflops Total (DP) |
| ----------|------------- |--------------|-----|-----|-----------|---------------------|-----------------------|-----------------------------|---------------------------|-----------------|---------------|--------------|
| **std** | cn(a/b)[01-64] | DELL C6320    | [Intel Xeon E5-2683v4 2.1 GHz, AVX2](http://ark.intel.com/products/91766/Intel-Xeon-Processor-E5-2683-v4-40M-Cache-2_10-GHz)              | n/a  | 128          | 32             | 4096          | 120GB     | 3750MB          |Omnipath 100Gb/s | Oui | 137.6 |
| **std** | cnc[01-48]     | DELL C6420    | [Intel Xeon Gold 6130 Processor 2.1 Ghz, AVX512](https://ark.intel.com/products/120492/Intel-Xeon-Gold-6130-Processor-22M-Cache-2_10-GHz) | n/a  | 48           |      32             | 1536          | 180GB     | 5625MB          |Omnipath 100Gb/s | Oui | 63.9 |
| **std** | cnd[01-12]     | DELL C6220    | [Intel Xeon E5-2640v2 2.0 GHz, AVX](https://ark.intel.com/fr/products/75267/Intel-Xeon-Processor-E5-2640-v2-20M-Cache-2_00-GHz)           | n/a  | 12           | 16             | 192           | 60GB      | 3750MB          |Infiniband 40Gb/s| Oui | 3.1 |
| **std** | cne[01-16]     | DELL R630     | [Intel Xeon E5-2637v4 3.5 GHz, AVX2](http://ark.intel.com/fr/products/92983/Intel-Xeon-Processor-E5-2637-v4-15M-Cache-3_50-GHz)           | n/a  | 16           | 8              | 128           | 120GB     | 15000MB            |Ethernet 10Gb/s  | Non | 7.2 |
| **gpu** | gpb[01-06]     | DELL C4130    | [Intel Xeon E5-2683v4 2.1 GHz, AVX](http://ark.intel.com/products/91766/Intel-Xeon-Processor-E5-2683-v4-40M-Cache-2_10-GHz)               | [NVIDIA Tesla P100](https://www.techpowerup.com/gpudb/2888/tesla-p100-pcie-16-gb)  | 6 <br> 4xGPU/nœud        | 32                  | 192                   | 120GB                       | 3750MB                |   Omnipath 100Gb/s  |  Non |  119.3 |
| **gpu** | gpc[01-04]     | DELL T630    | [Intel Xeon E5-2683v4 2.1 GHz, AVX](http://ark.intel.com/products/91766/Intel-Xeon-Processor-E5-2683-v4-40M-Cache-2_10-GHz)               | [GEFORCE GTX 1080 Ti](https://www.techpowerup.com/gpudb/2877/geforce-gtx-1080-ti)  | 4 <br> 2xGPU/nœud        | 32                  | 128                    | 120GB                       | 3750MB                |   Omnipath 100Gb/s  |  Non |  6.9 |


**Processeurs Intel Skylake (6ème génération) :**

La partition "skylake" (**sky**) comprend 48 nœuds connectés en réseau 100Gb à basse-latence, chaque nœud disposant de deux processeurs de type Skylake [Intel Xeon Gold 6130 Processor](https://ark.intel.com/products/120492/Intel-Xeon-Gold-6130-Processor-22M-Cache-2_10-GHz) (chacun comprenant 16 cœurs cadencés à 2.10Ghz, soit 32 cœurs par nœuds) et 192 Go de RAM. Elle est adaptée aux applications massivement parallèles.

!!! note ""
    La seule véritable différence entre les processeurs Skylake (6ème génération) et Broadwell (5ème génération) est que les premiers possèdent des instructions de calcul plus efficaces.
    Donc ils sont capables de générer plus d'opérations par secondes (flops) que les Broadwell a une seule condition de recompiler les programmes avec les bonnes options pour permettre d'utiliser ces nouveaux registres (AVX512).

**Processeurs Intel Broadwell (5ème génération) :**


La partition "standard" (**std**)  comprend 128 nœuds connectés en réseau 100Gb à basse-latence, chaque nœud disposant de deux processeurs de type Broadwell [Intel Xeon E5-2683 v4](http://ark.intel.com/products/91766/Intel-Xeon-Processor-E5-2683-v4-40M-Cache-2_10-GHz) (chacun comprenant 16 cœurs cadencés à 2.10Ghz, soit 32 cœurs par nœuds) et 128 Go de RAM. Elle est adaptée aux applications massivement parallèles.

La partition  "haute-fréquence" (**hf**) comprend 16 nœuds connectés en réseau 10Gb ethernet, chaque nœud disposant de deux processeurs [Intel Xeon E5-2637 v4](http://ark.intel.com/fr/products/92983/Intel-Xeon-Processor-E5-2637-v4-15M-Cache-3_50-GHz) chacun comprenant 4 cœurs cadencés à 3.5Ghz et 128 Go de RAM. Elle est adaptée aux applications sérielles ou faiblement parallélisées.

La partition **p100** comprend 6 nœuds connectés en reseau 100Gb à basse-latence , chaque nœud diposant de deux processeurs de type Broadwell [Intel Xeon E5-2683 v4](http://ark.intel.com/products/91766/Intel-Xeon-Processor-E5-2683-v4-40M-Cache-2_10-GHz) (chacun comprenant 16 cœurs cadencés à 2.10Ghz, soit 32 cœurs par nœuds), 128 Go de RAM et de 4 cartes [NVIDIA Tesla P100](https://www.techpowerup.com/gpudb/2888/tesla-p100-pcie-16-gb).

La partition **GTX** comprend 4 nœuds connectés en reseau 100Gb à basse-latence , chaque nœud diposant de deux processeurs de type Broadwell [Intel Xeon E5-2683 v4](http://ark.intel.com/products/91766/Intel-Xeon-Processor-E5-26833
-v4-40M-Cache-2_10-GHz) (chacun comprenant 16 cœurs cadencés à 2.10Ghz, soit 32 cœurs par nœuds), 128 Go de RAM et de 2 cartes [GEFORCE GTX 1080 Ti](https://www.techpowerup.com/gpudb/288
77/geforce-gtx-1080-ti)


**Processeurs Intel de Ivy Bridge (3ème génération) :**


La partition **ivy** comprend 12 nœuds connectés en réseau Infiniband 40Gb à basse-latence, chaque nœud disposant de deux processeurs [Intel Xeon E5-2640v2 2.0 GHz](https://ark.intel.com/fr/products/75267/Intel-Xeon-Processor-E5-2640-v2-20M-Cache-2_00-GHz) chacun comprenant 8 cœurs cadencés à 2.0 Ghz et 64 Go de RAM. Elle est adaptée aux applications parallèles.


### Matériel Hébergé

Le mésocentre a également vocation a héberger du matériel. Contactez-nous  [explor-contact@univ-lorraine.fr](mailto:explor-contact@univ-lorraine.fr) pour toute demande d'informations complémentaires concernant l'hébergement de matériel.

| Partition     |Matériel      | CPU | GPU | # de nœud | # de cœurs / nœud   | # de cœurs total      | Mémoire dispo / nœud              | Mémoire par défaut / cœur | Réseau          | Mode Exclusif | Tflops Total |
| ------------- |--------------|-----|-----|-----------|---------------------|-----------------------|-----------------------------|---------------------------|-----------------|---------------|--------------|
| **mysky**     | DELL C6420| [Intel Xeon Gold 6130 Processor 2.1 Ghz, AVX512](https://ark.intel.com/products/120492/Intel-Xeon-Gold-6130-Processor-22M-Cache-2_10-GHz) | n/a  | 16  | 32 | 512 | 153.6GB | 4.80GB |Omnipath 100Gb/s | Non | 19.2 |
| ------------- |--------------|-----|-----|-----------|---------------------|-----------------------|-----------------------------|---------------------------|-----------------|---------------|--------------|
| **myhf**      | DELL C6420   | [Intel Xeon Gold 5122 Processor 3.6 Ghz, AVX2](https://ark.intel.com/content/www/fr/fr/ark/products/120475/intel-xeon-gold-5122-processor-16-5m-cache-3-60-ghz.html)   | n/a  |8 | 8 | 64  | 96GB  | 1.50GB  |Omnipath 100Gb/s | Non | 11.3  | 
| ------------- |--------------|-----|-----|-----------|---------------------|-----------------------|-----------------------------|---------------------------|-----------------|---------------|--------------|
| **mycas**      | DELL C6820  | [Intel(R) Xeon(R) Gold 6230 CPU @ 2.10GHz, AVX512](https://ark.intel.com/content/www/fr/fr/ark/products/192445/intel-xeon-gold-5222-processor-16-5m-cache-3-80-ghz.html)   | n/a  |12 | 40 | 480  | 180GB  | 4.50GB  |Omnipath 100Gb/s | Non | 80.6 |
| ------------- |--------------|-----|-----|-----------|---------------------|-----------------------|-----------------------------|---------------------------|-----------------|---------------|--------------|
| **mylhf**     | DELL R640   | [Intel Xeon Gold 5222 Processor 3.8 Ghz, AVX512](https://ark.intel.com/content/www/fr/fr/ark/products/192445/intel-xeon-gold-5222-processor-16-5m-cache-3-80-ghz.html) | n/a  |2 |8 | 16  | 7465GB  | 93.25GB  |Omnipath 100Gb/s | Non |  1.0 |
| **myt4**     | DELL R740    | [Intel(R) Xeon(R) Gold 6126 CPU @ 2.60GHz, AVX](https://ark.intel.com/content/www/fr/fr/ark/products/120483/intel-xeon-gold-6126-processor-19-25m-cache-2-60-ghz.html) | [TESLA T4](https://www.techpowerup.com/gpu-specs/tesla-t4.c3316)  | 3 <br> 3xGPU/nœud  | 32    | 96    | 84GB  | 3500MB  |   Omnipath 100Gb/s  |  Non | 11.3 |


## Limitations en durée et en ressources d'un job

Les limitations suivantes en terme de ressources et de durées sont appliquées au mésocentre pour chaque job soumis :

| Partition     | # Max de Nœuds / job                | # Max de Cœurs / job                 | Durée Maximale /job (jours)      | # Max de GPU / job                 | # Max de jobs actifs   |
| ------------- | ----------------------------------- | -------------------------------------|----------------------------------| -----------------------------------|------------------------|
| **std**   | 1 <br> 2 <br> 4 <br> 8 <br> 16 <br> 32  | 32 <br> 64 <br> 128 <br> 256 <br> 512 <br> 1024 | 16 <br> 16 <br> 8 <br> 4 <br> 4 <br> 2  | - <br> - <br> - <br> - <br> - <br> -| 32 <br> 16 <br> 16 <br> 8 <br> 4 <br> 2 |
| **hf**    | 1                                       | 8                                     | 16                                                | -               | -                     |
| **ivy**   | 12                                      | 192                                   | 16                                                | -               | -                     |
| **sky**   | 1 <br> 2 <br> 4 <br> 8 <br> 16          | 32 <br> 64 <br> 128 <br> 256 <br> 512 | 16 <br> 16 <br> 8 <br> 4 <br> 4                    | -               | 16 <br> 8 <br> 8 <br> 4 <br> 2 |
| **p100**  | 1 <br> 2 <br> 3                         | 32 <br> 64 <br> 96                    | 16 <br> 8 <br> 4                                  | 4 <br> 8 <br> 12 | - <br> - <br> -     |
| **GTX**   | 1 <br> 2                                | 32 <br> 64                            | 16 <br> 8                                         | 2 <br> 4 | - <br> -    |

## Limitations en ressources d'un utilisateur

Les limitations suivantes en terme de ressources (Nœuds, CPU, GPU)  pour chaque utilisateur :

| Partition | # Max de Nœuds / utilisateur  | # Max de CPU / utilisateur        | # Max de GPU / utilisateur       |
| --------- | ----------------------------- | --------------------------------- | -------------------------------- |
| **std**   |   32                          | 1024                              | -                                |
| **hf**    |   -                           | 64                                | -                                |
| **ivy**   |   12                          | 192                               | -                                |
| **sky**   |   24                          | 768                               | -                                |
| **p100**  |   -                           | 96                                | 12                               |
| **GTX**   |   -                           | 64                                | 4                                |

!!! note ""
    La soumission du job sera refusée si la durée maximale n'est pas spécifiée ou si les ressources demandées dépassent les limitations ci-dessus.
