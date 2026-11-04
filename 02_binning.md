BBD Metagenome: Binning
================
Nora Mouer
2026-11-04

<!--
Explain what this step does and why, and copy each command you ran into a
bash chunk. R chunks run from the top of the repository.
-->

Extract bin depth and reorder Code: cat ../flye/bbd/assembly_info.txt \|
grep -v ‘\#’ \| awk ‘{OFS=“;print \$1,\$3}’ \> depths_bbd.txt cat
depths_bbd.txt \| awk ‘{print \$1}’ \| xargs samtools faidx
../flye/bbd/assembly.fasta \> assembly_bbd_ordered.fasta

Run metabat code: metabat2 -i assembly_bbd_ordered.fasta -a
depths_bbd.txt –cvExt -o bins_bbd/metabat –seed 5

Binning of the assembled contigs into genomes with MetaBAT 2. Commands
for this step were run in `metabat/`.
