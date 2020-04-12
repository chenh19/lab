# Preliminary *in silico* research for variants identified by NGS
The purpose is to get as much info about the variants as possible. Some work can be down automatically, some might need manual work.

> JAK2 V617F as an example

## Genome
> difference between hg19 and hg38  

- IGV for genome browsing
- NCBI variation viewer for genome browsing (https://www.ncbi.nlm.nih.gov/variation/view/)
- IGV for bam file

## Online databases

- GnomAD for rsID and MAF
- NCBI SNP for aa position
- NCBI Nucleotide for refseq
- Genecard for disease
- Uniprot for function, domain, active site, isoform, disease, interacting proteins
- PDB for structure
- PubMed for existing functional study (JAK2 V617F paper)

## Consequence prediction programs

- SIFT/Provean
- PolyPhen
- more (see paper)

## Structural prediction

### I-TASSER

- sequence
- template
- results

### PyMol
- how to use pymol (display, show, etc)
- how to align two proteins (structure alignment)

```
# Structure alignment
align A, B
```

- how to render protein for imaging

```
# Render 3D model
ray 2000, 2000

# Export image
png 001


```
