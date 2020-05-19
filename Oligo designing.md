# Oligo designing

First of all, to understand why a ~20bp sequence can be unique in the whole genome, you may do the calculation below:  

- In general, you may assume that for a nucleotide, the probability of it to be A, T, C, or G is <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{4}">.
- Then, for an oligo with a length of N bp, the probability of a specific sequence is <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{4} ^{N}">.
- Human genome is about 3 billion bp, we can calculate the N that the sequence only shows up once in the genome by solving the equation: <img src="https://render.githubusercontent.com/render/math?math=3\times10^{9} \times \frac{1}{4} ^{N}=1">
- <img src="https://render.githubusercontent.com/render/math?math=N = 15.74">, so when N >= 16, a sequence can be considered as unique in the whole genome

- Second, 3 ways to 

## Primers for PCR and genotyping
- ~500bp fragment
- Forward and reverse
- Tm: 58-60 °C
- Length 16-30bp

> Usually GC%, but if Tm and Length are within range, GC% will be good

## Primers for whole coding region sequencing
PCR


## Guide RNAs for gene knock-out



## Prime editing gRNAs for variants knock-in

### pegRNA for the strand to be edited

### gRNA for the non-edited strand 


## Appendix

Tm calculator for specific PCR enzymes/kits:
[Tm calculator](http://tmcalculator.neb.com/)

Calculate molecular weight by sequence:

[Calculator 1](http://molbiol.edu.ru/eng/scripts/01_07.html)
[Calculator 2](https://www.bioinformatics.org/sms2/dna_mw.html)
