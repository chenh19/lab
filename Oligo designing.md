# DNA Oligo designing
*Version: v1.0.0*

![](fig/oligo-3.png)
First of all, to understand why a ~20 bp sequence can be unique in the whole genome:  

- In general, you may assume that for each nucleotide in a sequence, the probability of it to be A, T, C, or G is <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{4}">.
- Then, for a N bp, the probability of it to be a specific sequence is <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{4} ^{N}">.
- Human genome is about 3 billion bp, we can calculate the N that the sequence only shows up once in the genome by solving the equation: <img src="https://render.githubusercontent.com/render/math?math=f(N)=3\times 10^{9} \times \frac{1}{4} ^{N}">
- <img src="https://render.githubusercontent.com/render/math?math=f(N)\leq 1">
- <img src="https://render.githubusercontent.com/render/math?math=N\geq 15.74">, so when <img src="https://render.githubusercontent.com/render/math?math=N \geq 16">, a sequence can be considered as unique in the whole genome

Second, 3 ways to calculate the Tm:  
- using SnapGene
- using online calculator
- manually: <img src="https://render.githubusercontent.com/render/math?math=Tm=2\times (A %2B T) %2B 4\times (G %2B C)">

## Primers for PCR

### Primers for regular PCR
- ```~500 bp``` fragment
- Forward and reverse
- Tm: ```58-60 °C```
- Length: ```16-30 bp```


### Primers and probes for quantitative PCR (qPCR)
- ```~500 bp``` fragment
- Forward and reverse
- Tm: ```58-60 °C```
- Length: ```16-30 bp```
- Probe Tm: ```~10 °C higher than primers' Tm```

> Usually GC%, but if Tm and Length are within range, GC% will be good

## Primers for sanger sequencing
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
