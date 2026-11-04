BBD Metagenome: Bin Quality
================
Nora Mouer
2026-11-04

<!--
Explain what this step does and why, and copy each command you ran into a
bash chunk. R chunks run from the top of the repository.
-->

We need to find the longest contig as it usually is not included code:
cat ../flye/bbd/assembly.fasta \| bioawk -c fastx ‘{print
length($seq),$name}’ \| sort -n

The largest contig was contig_116 Save contig_116 to bin and copy all
bins code: samtools faidx ../flye/bbd/assembly.fasta contig_XX \>
../metabat/bins_bbd/contig_XX.fa cp ../metabat/bins_bbd/\*.fa bins_bbd/

Create script labeled as run_checkm.bbd.sh code: !/bin/bash \#SBATCH
–time=60 \#SBATCH –ntasks=6 –mem=40gb \#echo “Starting checkm in \$(pwd)
at \$(date)”

shopt -s expand_aliases alias checkm=‘apptainer run -B /pvol/:/pvol
/pvol/data/sif/checkm.sif checkm’

checkm lineage_wf bins_bbd out -t 6 -x fa -f checkm_results_bbd.txt

echo “Finished checkm in \$(pwd) at \$(date)”

Run Sbatch code: sbatch run_checkm_bbd.sh

Sort for 15% completeness and show bin ID Code: cat
checkm_results_bbd.txt \| awk ‘\$13\>15’ cat checkm_results_bbd.txt \|
awk ‘\$13\>15{print \$1}’ cat checkm_results_bbd.txt \| awk
‘\$13\>15{print \$1}’ \> bbd_topbins.txt

Completeness and contamination of each bin, estimated with CheckM, and
selection of the most complete bins for further analysis. Commands for
this step were run in `checkm/`.
