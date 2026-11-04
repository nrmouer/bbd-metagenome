BBD Metagenome: Assembly
================
Nora Mouer
2026-11-04

<!--
Explain what this step does and why, and copy each command you ran into a
bash chunk. R chunks run from the top of the repository.
-->

``` bash
#we changed directory into fly and made a symbolic read to bbd-data
####code
#cd ~/bbd-metagenome/flye
#ln -s /pvol/data/metagenome_assembly/bbd_0.1.fastq.gz .
#made new flye script named run_flye_bbd.sh and saved to flye 
```

Made new fly script labled run_flye.bbd.sh and saved to flye directory
Code for script: \#!/bin/bash \#SBATCH –time=720 \#SBATCH
–cpus-per-task=12 –mem=20gb

echo “Starting flye bbd in \$(pwd) at \$(date)”

flye –nano-hq bbd_0.1.fastq.gz –threads 12 –out-dir bbd –meta

echo “Finished flye bbd in \$(pwd) at \$(date)”

Run sbatch on run_flye.bbd

Assembly of the BBD nanopore reads with Flye. Commands for this step
were run in `flye/`.
