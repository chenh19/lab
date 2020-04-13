# Preliminary *in silico* research for variants identified by NGS
When you have filtered the variants from raw NGS data, you may find there are still too many of them and it's hard to decide which ones are more valuable for downstream experimental research. Therefore, you should do *in silico* research to get as much info about the variants as possible.  
*Current version: v1.0.0*


## Understand the basic variant info
- The most basic variant info contains four parameters: **chromosome**, **position**, **reference**, **alternative**. These four parameters may be separated or concatenated with delimiters.  
- Here is a variant example, ```chr9-5073770-G-T```, which means this variant is located at the 5073770th nucleotide of chromosome 9, and the change is from guanine (G) to thymine (T).  
- One thing to note here is that the **position** may vary according to your [reference genome](https://en.wikipedia.org/wiki/Reference_genome), so please double check which one was used when these variants were being processed: **GRCh37/hg19** or **GRCh38**.  


## Check variants in the genome
You may first check the variant location in human genome, which can give you the info about:  

- the context of the variant (exon/intron/sequence context), so that you can easily find the variant in the reference sequence of the gene
- the NGS reads quality (variants at the end of amplicons are usually false, especially insertion or deletion; read depth; variant allele frequency)
- the rsID for the variant


### 1. IGV
[**Integrative Genomics Viewer (IGV)**](https://software.broadinstitute.org/software/igv/) for genome browsing  

- IGV has both original desktop applications and a newer web application. Here I'm using desktop version as an example
- To search for specific location in the genome, first open an IGV instance and select genome version, and then search by: ```chr:pos```(e.g., ```chr9:5073770```)
![](fig/2-1.png)
 
- If you have .bam files (along with .bai files in the same folder), you may directly open the .bam files with IGV and check the sequencing reads with the same way of searching
![](fig/2-2.png)


### 2. NCBI variation viewer
[**NCBI variation viewer**](https://www.ncbi.nlm.nih.gov/variation/view/) for genome browsing 

- NCBI variation viewer is an online genome visualizing tool integrated with more variant info
- To search for specific location in the genome, first select genome version, and then search by the same format: ```chr:pos```(e.g., ```chr9:5073770```)
![](fig/2-3.png)
- rsID can be useful for the following steps, such as retrieving variant consequences from online databases
- In some cases, rsID may not be automatically annotated for variants, which may require manual checking for rsID by this way


## Retrieve more info from online databases
Once you have checked the quality and context of the variant, you can retrieve more variant-related info from online databases

### 1. GnomAD
- [GnomAD](https://gnomad.broadinstitute.org/) is an extensive and trusted database, we use it for raw variant data annotating
- GnomAD has two versions, v2.1.1 is equal to GRCh37/hg19, while v3 is equal to GRCh38, make sure you select the right version before searching  
- In GnomAD, you may search for gene names and then search for special variants. You may also use the "Export to CSV" function to make variant reference for the genes that you are interested in
![](fig/2-4.png)
![](fig/2-5.png)
- Or, you may directly search for variants by: ```chr-pos-ref-alt```(e.g.,```9-5073770-G-T```)  
- On a variant page, there are three pieces of most important information: **Annotations**, **Population Frequencies**, and **References**
![](fig/2-6.png)
![](fig/2-7.png)
- In Annotations section, you can find the consequences (e.g., missense, frameshift, etc.), changes (e.g., amino acid and nucleotide changes), and deleteriousness predictions (e.g., benign or deleterious)
- In Population Frequencies section, you can find the frequency of the varianst in each population. Some variants might be rare globally but common in a specific population
- In References section, the info we use most is the rsID from dbSNP. Also, the rsID is hyperlinked to the NCBI SNP page, where you can find more details of the consequences and changes of the variants


### 2. NCBI
[**NCBI SNP**](https://www.ncbi.nlm.nih.gov/snp/)

- Search by ```rsID``` (e.g., ```rs77375493```)
![](fig/2-8.png)
- You may first check if the Alleles are correct. In some cases, you may be directed to a SNP page according to the location of the variant, but the allele change is actually novel and not available in the database. You may consider this to be a novel variant
![](fig/2-9.png)
- In Genomic Placements section, you can find the positions of the same variant in different genomic reference sequences
![](fig/2-10.png)
- In Gene section, you can see the consequences and changes of the same variant varying in different RNA and protein isoforms. If you use GnomAD as variant reference library to annotate the variants, you'll find that GnomAD always use canonical sequences for genes. In many cases, the canonical sequences are not necessarily the most prevalent or relevant sequences, and you'll need to do some extra work to determine the isoforms you want to study. Once the isoforms are determined, you can get the actual RNA or protein changes in the Gene section

[**NCBI Nucleotide**](https://www.ncbi.nlm.nih.gov/nucleotide/) for RNA refseq

- The most common sequences we use for genes are mRNA sequences
- You may search refseq by ```gene homo sapiens```, and then select mRNA on the left
![](fig/2-11.png)
- There might be multiple refseqs, select the one refseqs for your interested isoforms
- There might also be multiple refseqs for the same isofroms from different accessions, I would suggest select the ones with refseq starting with "NM_" ([difference between XM_ and NM_](https://www.ncbi.nlm.nih.gov/books/NBK50679/#RefSeqFAQ.what_is_the_difference_between))  
- You may download the refseq for following steps
![](fig/2-12.png)

[**NCBI PubMed**] for existing functional study (JAK2 V617F paper)

- You may search for previous research on the variants you are interested in
- The most common search format is: ```gene amino_acid_change disease``` (e.g., ```JAK2 V617F Myeloproliferative Neoplasm```)
![](fig/2-13.png)

### 3. Genecard
[Genecard](https://www.genecards.org/) for gene summaries

- You can find summaries of genes and their related disease, which can be very useful in some cases
![](fig/2-14.png)

### 4. Uniprot
[Uniprot](https://www.uniprot.org/) for protein info

- Uniprot is a protein database where you can find details of the gene products, including protein functions, domains, active sites, isoforms, diseases, interacting proteins, subcellular locations, etc.
- You may check whether the variants are or close to active sites
- You may also check which domains or regions the variants are located in, which may give you some hints of the functional results of the variants

### 5. PDB
[PDB](https://www.rcsb.org/) for protein structures

- PDB is a protein structure database, if your interested proteins have been structurally determined by previous study, you may utilize the structure models to see the 3D location of the variants and may use them as templates to do structural changes prediction
![](fig/2-15.png)

### 6. Hotspots
[3D Hotspots](https://www.3dhotspots.org/)  
![](fig/2-16.png)
[Cancer Hotspots](https://www.cancerhotspots.org/)  
![](fig/2-17.png)

- Some variants may happen at hotspots, which may give you some extra info of the variants


## Predict variant deleteriousness
Although you can find varaint deleteriousness in online databases like GnomAD, you may still want to do the prediction manually sometimes. There are many prediction tools with different algorithms (based on conservation, structure, etc.) available online. The table 2 in this paper has well summarized these tools: [DOI:10.1038/gim.2015.30](https://doi.org/10.1038/gim.2015.30). The most common tools we use are PROVEAN and PolyPhen, here I'll show how to do predictions with them. Other prediction tools should function in a very similar way.  

Your priority should be protein predictions, if protein prediction is not applicable, such as splice varaints, you can do genome prediction instead.  

[Provean Protein](http://provean.jcvi.org/protein_batch_submit.php?species=human)

- input
![](fig/2-18.png)
- output
![](fig/2-19.png)

[Provean Genome](http://provean.jcvi.org/genome_submit_2.php?species=human)

- input
![](fig/2-20.png)
- output
![](fig/2-21.png)

[PolyPhen](http://genetics.bwh.harvard.edu/pph2/bgi.shtml)

- input
![](fig/2-22.png)
- output
![](fig/2-23.png)


## Predict protein modification site
Post-translational modifications are important for protein property, structure and function. There are many prediction tools available online: [ExPASy](https://www.expasy.org/tools/#ptm), [DTU bioinfo](http://www.cbs.dtu.dk/databases/PTMpredictions/). Here I'll use phosphorylation prediction as an example. Other prediction tools should function in a very similar way.  

[NetPhos](http://www.cbs.dtu.dk/services/NetPhos/)

- Put in your sequence ([fasta format](https://en.wikipedia.org/wiki/FASTA_format))  
![](fig/2-24.png)
- Set parameters according to the guidance provided by with the tool
![](fig/2-25.png)
- Submit and run
- Output
![](fig/2-26.png)


## Predict protein structural changes
Predict the structures of proteins with variants and compare them with wild type structures.

### I-TASSER prediction

[I-TASSER server](https://zhanglab.ccmb.med.umich.edu/I-TASSER/)

- input
![](fig/2-27.png)

- output: also PDB files

### PyMol visualizing
PyMol is a useful desktop application for protein structure visualization. You may [download it here](https://pymol.org/2/)  

- You may also need to download the [free educational license](https://pymol.org/edu/?q=educational)  
- You can use PyMol in a very intuitive way using mouse ([a quick tutorial](https://pymol.org/dokuwiki/doku.php?id=mouse:two_button))
- Once you download the .pdb file from PDB website, you can open it with PyMol and use mouse to look at the protein
![](fig/2-28.png)

- You may want to highlight some sites on the protein where mutation happened, here is what I usually do: select, show as, color
![](fig/2-29.png)
![](fig/2-30.png)
![](fig/2-31.png)

- You may want to export the current view as an image, here is what I usually do using command lines: ```ray pixel,pixel```,  ```png filename```(e.g., ```ray 2000,2000```,  ```png export-1```), the exported file will be in the same folder as your PDB files
![](fig/2-32.png)
![](fig/2-33.png)

- Once you receive the prediction results from I-TASSER, you may want to compare the structural difference between the predicted ones and the original (wild type) ones, here is what I usually do using command lines: ```align A, B```(e.g., align NANS_WT,NANS_Variant)
![](fig/2-34.png)
![](fig/2-35.png)
Sometimes, single amino acid changes may not cause drastic protein structure changes. In that case, you may look into the proximal residues of the mutated sites.  
![](fig/2-36.png)

## Calculate odds ratio between variants and diseases
to see the association between the variants and specific diseases

[Odds ratio](https://www.wikiwand.com/en/Odds_ratio)

