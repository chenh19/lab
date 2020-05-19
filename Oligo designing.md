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

## 1. Primers for PCR
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
- Probe Tm: ```5-10 °C higher than primers' Tm``` (some qPCR kits use SYBR and don't require probes, while some other qPCR kits use fluorescent probes, such as Taqman)

#### Adding RE sites
- In many situation, you would want to add Restriction Endonuclease cutting sites to both ends of your product, so that in can integrate your product into a vector later.
[NEB RE list](https://www.neb.com/products/restriction-endonucleases)
Taking [EcoRI](https://www.neb.com/products/r0101-ecori#Product%20Information) and [KpnI](https://www.neb.com/products/r0142-kpni#Product%20Information) as an example

#### Site-directed mutation
[NEBaseChange](http://nebasechanger.neb.com/)
> Typically used for circular plasmid. (After PCR, use DNA ligase to ligate the linear DNA and make it circular again)
> This methods can also introduce insertion or deletion, just change the desired sequence in the NEBaseChanger.


#### Extending short DNA oligos
Oligo is usually less than 60 bp. If you want a slightly longer oligos, one way is to order [DNA ultramer](https://www.idtdna.com/pages/products/custom-dna-rna/dna-oligos/ultramer-dna-oligos), another way is to extend short oligos.
For example, two 60 bp oligos with 21 bp complementary sequence. Each oligo is both template and primer in this case. Just do regular PCR and you can get the full length double strand DNA (99 bp in this case)



## 2. Primers for sanger sequencing
#### PCR product sequencing
- basically the same primers for PCR, but use **only one** primer for each sequencing (sequencing is unidirectional). If you want to sequence it in both forward and reverse manner, you can sequence twice.
- Beginning: poor quality
- Middle region: good quality
- End: poor quality

#### Whole coding region sequencing
- usually 300-400 non-overlapping sequence
- overlap the beginning and the end of each fragment



## 3. Guide RNAs for gene knock-out
When doing CRISPR, you can transfect cells with either plasmids or more direct RNP (gRNA + Cas9 protein)
CRISPR is mostly used in our lab for for gene knock-out or variant knock-in.
Gene knock-out is relatively simple, just make an DSB and use NHEJ to introduce insertion or deletion and therefore cause frameshift (gRNAs are typically at the beginning of the gene, first 1 or 2 exons)


#### Making gRNA plasmid
you may follow this protocl
when selecting the spacers, [Feng Zhang's lab](https://zlab.bio/guide-design-resources), among which IDT is most frequently used by our lab since IDT makes DNA/RNA oligos
usually, one gRNA should be enough to cause small insertions or deletions. If large deletion is needed, you may design two gRNAs at both ends of the desired deletion.

#### DNA oligo/ultramer for *in vitro* transcription
- T7 promoter
- Spacer
- Scaffold



## 4. Prime editing gRNAs for variants knock-in
Another frequent application of CRISPR is variant knock-in. Still, you can use either plasmid or RNP. But RNP is preferred, because single clones with SNP are relatively difficult to select in the pool, the higher efficiency provided by RNP can be helpful.
There are many ways to introduce a variants. We currently use the most recent prime editing. Traditional combination of [gRNAs and donor templates](https://horizondiscovery.com/en/applications/crispr-cas9/homology-directed-repair-with-a-plasmid-donor) are not covered in this tutorial. 
Prime editing is relatively complicated but also very compact and high efficient. It doesn't use cell's HDR mechanism, but use reverse transcription instead.
Prime editing uses two gRNA, one introduce the variant, another is for the non-edited strand, which is to increase the variant introduction efficiency

#### pegRNA for the strand to be edited
- T7 promoter
- Spacer
- Scaffold
- RT (reverse transcription template) + PBS (primer binding site)
- *in vitro* transcription, capping and tailing
> When designing pegRNA, the spacer near the edited site might not have high scores, which is OK, because prime editing uses nickase. If it cut offsite, it will not introduce the variant because the RT won't align, and the nick can be ligated.
> Utilizing or designing RE cutting site for variant detection

#### gRNA for the non-edited strand 
PE3b is not practical in many cases. Therefore focusing on PE3 only here.
The secondary gRNA should be 40-90 bp away from the edited site
Doesn't have RT and PBS, only introduce a nick, will not introduce any sequence change



## 5. Gene panel designing for NGS
[illumina Gene Panel & Arrary Finder](https://www.illumina.com/products/selection-tools/gene-panel-finder.html#/)
> Usually you don't have to design the paneled oligos yourself.

## Appendix

Tm calculator for specific PCR enzymes/kits:
[Tm calculator](http://tmcalculator.neb.com/)

Calculate molecular weight by sequence:

[Calculator 1](http://molbiol.edu.ru/eng/scripts/01_07.html)
[Calculator 2](https://www.bioinformatics.org/sms2/dna_mw.html)
