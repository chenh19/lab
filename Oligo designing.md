# DNA Oligo designing
*Version: v1.0.0*

![](fig/oligo-3.png)

First of all, to understand why a ~20 bp sequence can be unique in the whole genome:  

- In general, you may assume that for each nucleotide in a sequence, the probability of it to be A, T, C, or G is <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{4}">.
- Then, for a N bp sequence, the probability of it would be <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{4} ^{N}">.
- Human genome is about 3 billion bp, so you may express the frequency of the sequence in the whole genome in this way: <img src="https://render.githubusercontent.com/render/math?math=f(N)=3\times 10^{9} \times \frac{1}{4} ^{N}">
- The sequence being unique in the whole genome means: <img src="https://render.githubusercontent.com/render/math?math=f(N)\leq 1">
- Solve and function and get the result: <img src="https://render.githubusercontent.com/render/math?math=N\geq 15.74">
- Therefore when <img src="https://render.githubusercontent.com/render/math?math=N \geq 16">, a sequence can be considered as unique in the whole genome

Second, 3 ways to calculate the Tm ([Understanding melting temperature (Tm)](https://www.idtdna.com/pages/education/decoded/article/understanding-melting-temperature-(t-sub-m-sub-))):  

- using SnapGene ([Download SnapGene](https://www.snapgene.com/snapgene-viewer/))
- using online calculator: [NEB Tm calculator for specific PCR enzymes/kits](http://tmcalculator.neb.com/)
- manual calculation: <img src="https://render.githubusercontent.com/render/math?math=Tm=2\times (A %2B T) %2B 4\times (G %2B C)">, where ```A, T, C, G``` means the counts of each nucleotide in the **single-strand** oligos

> Note:   
> - For most cases (e.g., when using Phusion polymerase), SnapGene's Tm would be accurate. If you are using Q5 polymerase, make sure you use the **NEB Tm calculator** because Q5 buffer can increase the Tm.  
> - [Annealing Temperature (Ta)](https://www.labce.com/spg1025560_annealing_temperature_ta.aspx) is slightly different from Tm, although they are often mis-used interchangeably.  
> - Only include the aligned nucleotides for Tm calculation. Those nucleotides that doesn't align will not contribute to the Tm.

## Primers for PCR
DNA oligos are most frequently used in daily PCR experiments. Below are the basic principles for designing the oligos.


#### Primers for regular PCR
- DNA Oligo amount: 2 (forward primer for one strand, reverse primer for the other strand)
- Primer Tm: ```58-60 °C```
- Primer length: ```16-32 bp```
- Product length: ```~500 bp```
> - GC% is usually another specs mentioned in other tutorials, but if Tm and Length are within range, GC% will be good.  
> Note: A set of primers can also amplify a single-strand DNA template. In the first cycle, only one primer will work, but once double strand DNA template forms, the primer will amplify the double strand DNA.

#### Primers and probes for quantitative PCR (qPCR)
- DNA Oligo amount: 2 or 3 (forward primer for one strand, reverse primer for the other strand, maybe a probe in between for either strand)
- Primer Tm: ```58-60 °C```
- Primer length: ```16-32 bp```
- Product length: ```100-200 bp``` (for fast qPCR process)
- Probe Tm: ```~10 °C higher than primers' Tm``` (some qPCR kits use SYBR and don't require probes, while some other qPCR kits use fluorescent probes, such as Taqman)

#### Adding RE sites
- In many situation, you would want to add Restriction Endonuclease cutting sites to both ends of your product, so that in can integrate your product into a vector later.
[NEB RE list](https://www.neb.com/products/restriction-endonucleases)
Taking [EcoRI](https://www.neb.com/products/r0101-ecori#Product%20Information) and [KpnI](https://www.neb.com/products/r0142-kpni#Product%20Information) as an example

#### Site-directed mutation
[NEBaseChange](http://nebasechanger.neb.com/)
> Typically used for circular plasmid. (After PCR, use DNA ligase to ligate the linear DNA and make it circular again)
> This methods can also introduce insertion or deletion, just change the desired sequence in the NEBaseChanger.


#### Extending short DNA oligos



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
