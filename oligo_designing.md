# DNA Oligo designing principles
This tutorial focuses only on the designing of DNA oligos, which is mostly based on my bench experience and might be slightly different from text books or general protocols. Basic principles of PCR, qPCR, sequencing, and CRISPR will not be discussed here.  
*Version: v1.1.0*

#### Table
1. [*Background*](https://github.com/chenh19/lab_training/blob/master/oligo_designing.md#1-background)
2. [*Primers for PCR*](https://github.com/chenh19/lab_training/blob/master/oligo_designing.md#2-primers-for-pcr)
3. [*Primers for sequencing*](https://github.com/chenh19/lab_training/blob/master/oligo_designing.md#3-primers-for-sequencing)
4. [*Guide RNAs for gene knock-out*](https://github.com/chenh19/lab_training/blob/master/oligo_designing.md#4-guide-rnas-for-gene-knock-out)
5. [*Prime editing gRNAs for variants knock-in*](https://github.com/chenh19/lab_training/blob/master/oligo_designing.md#5-prime-editing-grnas-for-variants-knock-in)
6. [*Appendix*](https://github.com/chenh19/lab_training/blob/master/oligo_designing.md#6-appendix)


## 1. Background
**First of all**, to understand why a ~20 bp sequence can be unique in the whole genome:  

- In general, you may assume that for each nucleotide in a sequence, the probability of it to be A, T, C, or G is <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{4}">
![](fig/oligo-3.png)
- Then, for a N bp sequence, the probability of it would be <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{4} ^{N}">
- Human genome is about 3 billion bp, so you may express the frequency of the sequence in the whole genome in this way: <img src="https://render.githubusercontent.com/render/math?math=f(N)=3\times 10^{9} \times \frac{1}{4} ^{N}">
- The sequence being unique in the whole genome means: <img src="https://render.githubusercontent.com/render/math?math=f(N)\leq 1">
- Solve the function and get the result: <img src="https://render.githubusercontent.com/render/math?math=N\geq 15.74">
- Therefore when <img src="https://render.githubusercontent.com/render/math?math=N \geq 16">, a sequence can be considered as unique in the whole genome

**Second**, 3 ways to calculate the Tm ([Understanding melting temperature (Tm)](https://www.idtdna.com/pages/education/decoded/article/understanding-melting-temperature-(t-sub-m-sub-))):  

- Using SnapGene ([Download SnapGene](https://www.snapgene.com/snapgene-viewer/))
![](fig/oligo-4.png)
- Using online calculator: [NEB Tm calculator for specific PCR enzymes/kits](http://tmcalculator.neb.com/)
![](fig/oligo-9.png)
- Manual calculation: <img src="https://render.githubusercontent.com/render/math?math=Tm=2\times (A %2B T) %2B 4\times (G %2B C)">, where ```A, T, C, G``` means the counts of each nucleotide in the **single-strand** oligos. Do **not** use this unless you don't have access to computers

> Note:   
> 
> - In most cases (e.g., when using Phusion polymerase), SnapGene's Tm would be accurate. If you are using Q5 polymerase, make sure you use the **NEB Tm calculator** because Q5 buffer can increase the Tm.  
> - [Annealing Temperature (Ta)](https://www.labce.com/spg1025560_annealing_temperature_ta.aspx) is slightly different from Tm, although they are often mis-used interchangeably.  
> - Only include the **aligned nucleotides** for Tm calculation. Those nucleotides that doesn't align will not contribute to the Tm.  
> - If you see a sequence without 5' and 3' annotated, by default **the left end is 5'** and **the right end is 3'**.

## 2. Primers for PCR
- DNA oligos are most frequently used in daily PCR experiments. There are different designing skills for different situations
- First of all, here is an example of making a primer in SnapGene: just select a region and use the "Add primer" tool
![](fig/oligo-6.png)
![](fig/oligo-7.png)
![](fig/oligo-8.png)

> Note:
>
> - Please try to use the annotated DNA maps (RefSeq). The annotations, such as the exons, will help you with designing.

### i. Primer sets for regular PCR
- DNA Oligo amount: 2 (forward primer for one strand, reverse primer for the other strand)
- Primer Tm: ```58-60 °C``` (This saves time because for every PCR you can just set the annealing temp of your PCR program to 58°C without going back to check your primer design)
- Primer length: ```16-32 nt``` (From the calculation in the background you can understand why the minimum length is 16 bp)
- Product length (coverage): ```~500 bp``` (500 bp is usually good for one-time Sanger sequencing)
![](fig/oligo-10.png)
![](fig/oligo-11.png)
![](fig/oligo-12.png)

> Note:   
> 
> - You may first deign a primer within the Tm range and then check whether the length is with the range as well.
> - **GC%** is usually another specs mentioned in other tutorials, but if Tm and Length are within range, GC% will be good and you don't have to worry.  
> - A set of primers can also amplify **single-strand DNA templates**. In the first cycle, only one primer will work, but once double-strand DNA template forms, both primers will work and amplify the double-strand DNA.
> - If you are doing genotyping, please remeber to use the **genomic DNA maps** for primer designing, not the mRNA/cDNA maps.

### ii. Primer and probe sets for qPCR
- DNA Oligo amount: 2 or 3 (forward primer for one strand, reverse primer for the other strand, maybe a probe in between for either strand)
- Primer Tm: ```58-60 °C``` (qPCR usually uses a 2-step program, where the temp of the second step is typically set to 60 °C)
- Primer length: ```16-32 nt```
- Product length (coverage): ```100-200 bp``` (for fast qPCR process)
- Probe Tm: ```5-10 °C higher than primers' Tm``` (some qPCR kits use SYBR and don't require probes, while some other qPCR kits use fluorescent probes, such as Taqman)
![](fig/oligo-13.png)
![](fig/oligo-14.png)
![](fig/oligo-15.png)
![](fig/oligo-16.png)

### iii. Adding RE sites
- In some cases, you would want to add Restriction Endonuclease cutting sites to both ends of your product, so that it can be later integrated into an expression vector
- NEB has a list of all its available REs: [NEB RE list](https://www.neb.com/products/restriction-endonucleases)
- In SnapGene, you can also show all the available RE sites on your gene map: 
![](fig/oligo-19.png)
![](fig/oligo-20.png)
![](fig/oligo-22.png)
- Here, taking [EcoRI](https://www.neb.com/products/r0101-ecori#Product%20Information) and [KpnI](https://www.neb.com/products/r0142-kpni#Product%20Information) as an example of adding RE sites to PCR products. Here are the RE sites of both enzymes:
![](fig/oligo-17.png)
![](fig/oligo-18.png)
- You can just add the RE sites to your primers like this:
![](fig/oligo-23.png)
![](fig/oligo-24.png)
![](fig/oligo-25.png)

> Note:
>
> - Always add 2 random nucleotides before your cutting sites. This is to trick the enzymes into believing that they are binding to the middle of a DNA instead of the ends.
> - When adding the cutting site sequences to the primers, you don't necessarily add the entire sequences, usually you can utilize a few nucleotides in the template sequences.
> - Note that only the aligned nucleotides will contribute to the Tm.

- Illustration of how the PCR will work:
![](fig/oligo-26.png)
![](fig/oligo-27.png)

### iv. Site-directed mutation
- Use the tool, [NEBaseChange](http://nebasechanger.neb.com/). Do **not** manually design site-directed mutation primers unless the ones from NEB fail
- This is typically used for **circular plasmids**. After PCR, the amplified DNA will be linear and you can use **DNA ligase** to make it circular again
- This methods can also introduce **insertion** or **deletion** into the plasmids. To design insertion or deletion primers, you can just change the **Desired sequence** in the NEBaseChanger
![](fig/oligo-28.png)
![](fig/oligo-29.png)
![](fig/oligo-30.png)
- How the site-directed mutation primers look like in SnapGene:
![](fig/oligo-31.png)

### v. Extending short DNA oligos
- DNA Oligo is usually shorter than 60 nt. If you want slightly longer oligos, one way is to order [DNA ultramers](https://www.idtdna.com/pages/products/custom-dna-rna/dna-oligos/ultramer-dna-oligos) from companies, another way is to extend short oligos
- For example, two 60 nt oligos here with 21 bp complementary sequence. Each oligo is both template and primer in this case. Just do a regular PCR and you'll get the full length double-strand DNA (99 bp in this case)
![](fig/oligo-32.png)

> Note:
>
> - For the complementary sequence, design with the same principles for regular PCR primers.



## 3. Primers for sequencing
### i. Sanger sequencing for small PCR products
- Primers for sanger sequencing are basically the same as the primers for regular PCR
- Typically you would want the PCR product to be ```~500 bp```, so that you can get the best sequencing quality with just one-time sequencing
- When mixing sequencing samples and primers, always use **only one** primer for each sample (sequencing is unidirectional). If you want to sequence it in both forward and reverse manner, you can sequence twice in separate tubes
- Here are an example of sequencing results. Beginning region (<60 bp): poor quality
![](fig/oligo-33.png)
- Middle region (60-600 bp): good quality (clean and sharp signal peaks, low background noise)
![](fig/oligo-34.png)
- End region (>600 bp): poor quality (blurry signal, high background noise)
![](fig/oligo-35.png)

> Note:
>
> - The variants detected in the poor quality regions should be considered as **false** by default.


### ii. Sanger sequencing for large regions
- To avoid false variants, use the overlapping design
- Typically ```300-400 bp``` between the primes (non-overlapping region)
- The beginning and the end of each sequencing fragment should be overlapped by another sequencing fragment
![](fig/oligo-36.png)
- Here is an example of sequencing results aligned to the template:
![](fig/oligo-37.png)

> Note:
>
> - Any variant **shows up for only once (not overlapped)** should be considered as **false**.

### iii. Gene panel designing for NGS
- Paneled-NGS uses hundreds of primers for targeted amplicons. There are many panels available online designed by companies or by community, here is an example: [illumina Gene Panel & Arrary Finder](https://www.illumina.com/products/selection-tools/gene-panel-finder.html#/)
![](fig/oligo-1.png)

> Note:
> 
> - Usually you don't have to design the paneled oligos by yourself.


## 4. Guide RNAs for gene knock-out
- CRISPR is mostly used for for gene knock-out and variant knock-in in our lab
- Gene knock-out is relatively simple since you don't need to design a repair template. You just need to make a double-strand break and then use cell's NHEJ mechanism to introduce a small insertion or deletion to the gene, which usually causes frameshift. Usually the gRNAs are designed to target the first or the second exon of the gene
- When doing CRISPR, you can transfect cells with either plasmids or more direct RNP (gRNA + Cas9 protein)

### i. Making gRNA plasmid
- First, you will need to select a spacer (20 bp sequence before a PAM, *NGG*). It is recommended to use a gRNA designing tool to get the highest efficiency. [Feng Zhang's lab](https://zlab.bio/guide-design-resources) has well listed these tools, among which [IDT](https://www.idtdna.com/site/order/designtool/index/CRISPR_CUSTOM) is most frequently used by our lab
![](fig/oligo-39.png)
- When selecting spacers for gene knock-out, the general principle is to select the ones with as high **off-target** score as possible and not too low on-target score. However, it can depends on the experimental needs. Besides, **predesigned** gRNAs are usually safer than custom ones because people has test them 
![](fig/oligo-40.png)
- Usually, one gRNA should be enough to cause small insertions or deletions. If large deletion is needed, you may design two gRNAs at both ends of the desired deletion
- Second, you may follow this protocol to generate the gRNA plasmid. Note that the first nucleotide of the spacer needs to be replaced by *G*
![](fig/oligo-2.png)

> Note:
>
> - Plasmids can be toxic to cells.
> - It can take some time for the plasmids to express in the cells.
> - You may also use an antibiotic-resistant donor plasmid when transfecting. The antibiotic-resistant gene can be inserted into the cutting sites and therefore make it easier for later selection.

### ii. DNA oligo/ultramer for *in vitro* transcription
- You may directly order a single-strand DNA oligo or ultramer, amplify it by a regular PCR, and then do *in vitro* transcription to get the gRNA
![](fig/oligo-38.png)

- **T7 promoter**: ```aagc-TAATACGACTCACTATA-GG-``` (It's recommended to add 4 **random** nucleotides before the promoter; *GG* after the promoter is necessary for reasonable yields of *in vitro* transcription)
- **Spacer**: ```20 bp``` sequence before PAM (use a gRNA designing tool to select the spacer; it's recommended **not** to replace the first nucleotide with *G*)
- **Scaffold**: ```-GTTTTAGAGCTAGAAATAGCAAGTTAAAATAAGGCTAGTCCGTTATCAACTTGAAAAAGTGGCACCGAGTCGGTGC``` (You **don't** need to change this unless you are changing to enzymes other than Cas9)

> Note:
>
> - T7 promoter is only for *in vitro* transcription. If you are directly ordering RNA, you don't need it.
> - Heating the gRNA and then cooling it down can help the scaffold fold into the structure that Cas9 protein can bind.
> - RNP is much less toxic to cells than plasmids.
> - *In vitro* transcription saves time because it skips the molecular cloning procedures.
> - gRNA is still a type of RNA and is susceptible to RNases. **Capping** and **poly-A tailing** can significantly stabilize the gRNA and therefore increase the transfection efficiency.


## 5. Prime editing gRNAs for variants knock-in
- Another frequent application of CRISPR is variant knock-in. Still, you can use either plasmid or RNP. But RNP is preferred because single clones with SNP are relatively difficult to select in the mixed cell pool, and the higher efficiency provided by RNP can be helpful
- There are many ways to introduce a variants. We currently use the tech coming out in 2019, which is called [Prime editing](https://doi.org/10.1038/s41586-019-1711-4) and uses **reverse transcription** and **mismatch repair** to introduce the variants. Traditional combination of [gRNAs and HDR repair templates](https://blog.addgene.org/crispr-101-homology-directed-repair) will not be discussed in this tutorial
![](fig/oligo-41.png)
- Prime editing is relatively complicated but also very compact and high efficient. It doesn't use cell's HDR mechanism, but uses reverse transcription instead
![](fig/oligo-42.png)
- Prime editing 3 uses two gRNAs, one introduces the variant, another introduces a nick on the non-edited strand, which is to increase the editing efficiency

### i. pegRNA for the strand to be edited
- **T7 promoter**: ```aagc-TAATACGACTCACTATA-GG-``` (It's recommended to add 4 **random** nucleotides before the promoter; *GG* after the promoter is necessary for reasonable yields of *in vitro* transcription)
- **Spacer**: ```20 bp``` sequence before PAM (it should be as close to the edited site as possible)
- **Scaffold**: ```-GTTTTAGAGCTAGAAATAGCAAGTTAAAATAAGGCTAGTCCGTTATCAACTTGAAAAAGTGGCACCGAGTCGGTGC-``` (You **don't** need to change this unless you are changing to enzymes other than Cas9)
- **RT** (reverse transcription template): no less than ```7 nt``` before the cutting site (5' to 3' direction); there is no strict resrtiction for the length of the RT, but you should try do make it as short as possible (the longer the DNA oligos/ultramers, the harder to make and the more expensive), usually RT within ```20 nt``` is good; **avoid** ```C``` at the 5' of RT (the 5' of RT is connected to the Scaffold, be careful with the direction); you may remove the ```PAM site``` with a synonymous variant if applicable; you may also introduce or remove a ```RE site``` with a synonymous variant if applicable
- **PBS** (primer binding site): ```8-15 nt``` after the cutting site (also 5' to 3' direction; if 8-15 nt is not easy to determine, check the Tm in SnapGene, ideally it should be ```40-45 °C```; PBS can anneal with the spacer, so when you can reach the Tm range, the **shorter** the PBS the better)


> Note:
>
> - T7 promoter is only for *in vitro* transcription. If you are directly ordering RNA, you don't need it.
> - Note that the cutting site of Cas9 nuclease/nickase is between the **3** and **4** nucleotides upstream of the PAM site. If the the first nucleotide of the PAM site is labeled as +1, the cutting site would be between -3 and -4 nucleotides (5' to 3' direction).
> - Note that Cas9 H840A nickase cuts the **opposite** strand of the *NGG* strand.
> - Spacer longer than 20 bp will **not** increase the affinity, therefore always use 20 bp. Don't worry about the Tm for spacers.
> - When designing pegRNAs, the spacers near the edited sites might not have high scores in gRNA designing tools (e.g., [IDT CRISPR-Cas9 gRNA checker](https://www.idtdna.com/site/order/designtool/index/CRISPR_CUSTOM)), which is OK. Prime editing uses nickase and if it cut offsite, it will not introduce the variant because the PBS won't align.
> - Although PAM is 3 nt long, it's not necessarily in frame with the amino acid coding. When you are trying to use synonymous variants to remove the PAM, make sure that your synonymous variants are not for the 3 nt PAM but for those in-frame amino acid codons.
> - When designing the RT, you should observe whether your editing can introduce or remove any RE cutting sites. You may also artificially introduce synonymous variants to the template to do that. RE sites will be beneficial in the later clone selection process. Ideally, the selected RE should only cut once in the genotyping region.
> - When adding the RT and PBS, be careful with the direction.
> - **Capping** and **poly-A tailing** are strongly recommended for *in vitro* transcription.
> - If you are labeling the variants in your SnapGene map, make sure you're labeling with the top strand sequence to avoid confusion.

### ii. gRNA for the non-edited strand 
- PE3b is not practical in many cases. Therefore, this tutorial only focuses on PE3
- The secondary gRNAs should be ```40-90 bp``` away from the edited site
- The secondary gRNAs only has **T7 promoter**, **spacer**, and **scaffold**, and don't have RT and PBS. They will only introduce a nick  and will not introduce any sequence changes
- A complete example of pegRNA designing:
![](fig/oligo-43.png)

> Note:
>
> - In this example, the genotyping primers are designed with the principles for the primers for regular PCR and they cover a region of ~500 bp.

## 6. Appendix
- Calculate molecular weight by sequence: [Calculator-1](http://molbiol.edu.ru/eng/scripts/01_07.html), [Calculator-2](https://www.bioinformatics.org/sms2/dna_mw.html)
- Amino acid codons:
![](fig/aa-2.png)  
