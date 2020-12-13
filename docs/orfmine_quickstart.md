## Usage
Here is presented an example of the use of ORFmap with ORFold 
to annotate all the ORFs of a genome, and to characterize their fold potential
and disorder and aggregation propensities.

The inputs used in this example and the resulting outputs are 
available in the ORFmine/examples/ folder.


## Annotation and extraction of ORFs with ORfmap

### Annotation of ORFs
ORFmap takes as input (i) a FASTA file containing the nucleotide
sequences of all chromosomes or contigs, and (ii) their corresponding 
annotations in a GFF file (see 
[the GFF3 documentation](https://github.com/The-Sequence-Ontology/Specifications/blob/master/gff3.md)
for more details on the GFF3 format). 
The following command runs ORFmap on the complete genome of Escherichia
coli (Ecoli) available in the "examples" folder:

``` python
orfmap -fna ecoli.fasta -gff ecoli.gff
```
ORFmap generates a novel GFF file (available in 
ORFmine/examples/outputs/Ecoli_ORFs_XXXX.gff)
containing the annotations of all identified ORFs. 

### Extraction of noncoding ORFs in a FASTA file
The amino acid sequences of 
all annotated ORFs or specific subsets of ORFs (i.e. only noncoding 
intergenic ORFs for example) can be extracted and written in a 
FASTA file with ORFget, a tool provided with ORFmap. The following 
instruction writes the amino acid sequences of all noncoding ORFs (including 
noncoding intergenic ORFs and those that overlap with a genomic feature) 
of Ecoli in a FASTA file.


``` python
orfget -fna genome.fasta -gff mapping_orf_ecoli.gff -features_include nc -o nc_orf_ecoli
```

ORFget produces a FASTA file (nc_orf_ecoli.pfasta) containing the amino acid sequences
of all noncoding ORFs annotated by ORFmap (see [here](./orfget_run.md) for more examples 
on the use of ORFget). 

### Extraction of protein sequences of Ecoli in a FASTA file
In addition, ORFget enables the reconstruction of all protein 
sequences of Ecoli according to their definition in the **original**
GFF file.


``` python
orfget -fna ecoli.fasta -gff ecoli.gff -features_include CDS -o CDS_ecoli
```



## Characterization of the fold potential and disorder and aggregation propensities of the noncoding ORFs with ORFold


### Running ORFold
ORFold only needs a FASTA file containing the amino acid
sequences to characterize. That said, a GFF 
file containing the annotation of the input sequences can be provided
as well. In the latter case, ORFold writes the fold potential
and disorder and aggregation propensities in three GFF files respectively.
The latter can be subsequently uploaded on a genome viewer for a 
visual inspection of the distribution of these properties along
the genome. 

The following instruction enables the user to probe the fold 
potential and disorder and aggregation propensities of all noncoding
ORFs annotated by ORFmap along with those of the protein sequences
of Ecoli. The GFF file generated by ORFmap is given as well in order
to manually inspect with a genome viewer, the distribution of
the structural properties
 of the noncoding ORFs along the genome of Ecoli.

``` python
orfold -fna nc_orf_ecoli.pfasta CDS_ecoli.pfasta -options HIT -gff mapping_orf_ecoli.gff ecoli.gff
```

ORFold provides two tables (one per dataset) available in
ORFmine/examples/outputs/. Each table contains for each input 
sequence, the fold potential, disorder and aggregation propensities
based on HCA [REF], IUPred [REF] and TANGO [REF] respectively 
(see [here](./How_it_works_orfold.md) for more details on the calculation of these scores).
ORFold also generates three new GFF files containing for each
ORF present at the same time in the input FASTA and GFF files, 
its fold potential
and disorder and aggregation propensities respectively. The output
GFF files can be subsequently uploaded on a genome viewer.


### Visualization of the distribution of the fold potential with ORFplot

ORFplot enables the visualization of the distribution of the fold
potential of the noncoding ORFs and protein sequences along with the one of a reference dataset
of globular proteins taken from XXXX.

``` python
orfplot xxxx
```

The output graphic is generated in PNG and PDF formats (see 
[here](./orfplot_run.md) for other examples of use of ORFplot). Each
distribution is compared with the one of the globular protein dataset
with a Kolmogorov Smirnov test. Asterisks on the plot denote level 
of significance: * < 0.05, \**\** < 0.01, *** < 0.001.


<div class="admonition note">
    <p class="first admonition-title">
        Note
    </p>
    <p class="last">
        This section implies that IUPred and TANGO have been downloaded 
and that their paths have been correctly defined during the installation 
procedure. 
    </p>
</div>