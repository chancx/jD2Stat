# jD2Stat
jD2Stat (previously known as JIWA*) is a Java package that utilises a series of D~2~ statistics to
extract k-mers (subsequences at defined k length) from a set of biological sequences, and generate
pairwise distances for each possible pair. This distance can be used directly for phylogenetic inference
using neighbour-joining.

*: This program is not to be confused with, and has no relation to, the proprietary trademark and
software of Jiwa Financials, North Sydney, Australia.

The D<sub>2</sub> methods included are:
- D<sub>2</sub> based on exact k-mer counts (<code>D2</code>)
- D<sub>2</sub><sup>S</sup> - similar to D<sub>2</sub>, normalised based on probability of occurrences of specific k-mers (<code>D2S</code>)
- D<sub>2</sub><sup>∗</sup> - similar to D<sub>2</sub>, normalised based on means and variance (<code>D2St</code>)
- D<sub>2</sub><sup>n</sup> - extension of D<sub>2</sub> to allow for *n* number of wildcards (n neighbourhood)

## Requirements
jD2Stat runs on all platforms that support the Java Runtime Environment JRE 1.7.x or higher. jD2Stat
comes in a .jar file that can be invoked on command line directly under JRE, so no compilation or
installation is necessary. In the rare occasion that you have no Java installed on your computer, Java
is freely available from http://www.java.com/.
Memory requirement varies depending on the number and length of the sequences, overall sequence
similarity and the k-mer length, for obvious reasons. RAM of 1GB would be sufficient for most
simple analyses. For instance, in our analysis of 5000 16S rRNA sequences, the memory usage is
about 2.5GB.

## Input
jD2Stat accepts DNA and protein sequences in FASTA format. A file should contain a set of two or
more sequences, and MUST have any one of these extensions: .faa, .fas, .fasta, .ffn, .fna or .frn. Both
single- and multi-line FASTA format are accepted.

IMPORTANT: Note that jD2Stat considers only conventional nucleotide and amino acid characters in the analysis: A, C, G and T for DNA, and the standard 20 amino acids (single-letter code) for proteins. The presence of any non-conventional characters in the sequences will result in an error.

## Output
For each D<sub>2</sub> analysis, jD2Stat generates a pairwise distance matrix in PHYLIP format, which can be
used as input for <code>neighbor</code> in PHYLIP to infer a phylogenetic tree using neighbour-joining.

## Implementation
jD2Stat can be invoked directly on command line:
```
java –Xmx<vmem> –jar jD2Stat_1.0.jar <options> -i <input> -o <output>
```
## Quick start

In following examples: input sequences in <code>myseq.fas</code>, output matrix file named <code>myseq.matrix</code>.
```
java –Xmx4g –jar jD2Stat_1.0.jar –d D2 –k 8 -i myseq.fas -o myseq.matrix
```

The above command runs D<sub>2</sub> statistic on DNA sequences at *k*-mer length 8 with max memory set at 4GB.

```
java –Xmx4g –jar jD2Stat_1.0.jar –a aa –d D2St –k 4 -i myseq.fas -o myseq.matrix
```

The above command runs D<sub>2</sub><sup>*</sup> statistic on protein sequences at *k*-mer length 4 with max memory set at 4GB.

```
java –Xmx8g –jar jD2Stat_1.0.jar –n 1 –k 8 -i myseq.fas -o myseq.matrix
```

The above command runs D<sub>2</sub><sup>n</sup> (with neighbourhood *n* = 1) on DNA sequences at *k*-mer length 8 with max memory set at 8GB.

```
java –Xmx12g –jar jD2Stat_1.0.jar –a aa –d all –k 4 -i myseq.fas
```

The above command runs all three D<sub>2</sub>, D<sub>2</sub><sup>S</sup>, and D<sub>2</sub><sup>*</sup> independently on protein sequences at *k*-mer length 4 with max memory set at 12GB. Three distance matrices in separate files will be generated.

## Parameters

| Parameter | Description |
| --- | --- | 
| ```-a <a>```      | ```<a>``` is the alphabet/character type of the sequences: ```dna``` (default) or ```aa``` (amino acid). |
| ```-d <d>```      | ```<d>``` is the choice of D<sub>2</sub> method: ```D2``` (default), ```D2S```, ```D2St``` or ```all``` to run all three methods of D<sub>2</sub>, D<sub>2</sub><sup>S</sup>, and D<sub>2</sub><sup>*</sup>; ```–d all``` yields all three matrices in separate files even without ```–o``` specification. |
| ```-h```          | Display all available options on the screen        |
| ```-k <k>```      | ```<k>``` is the length of *k*-mers to be used in the analysis. Default: 8 |
| ```-n <n>```      | ```<n>```is the neighbourhood value of n in D<sub>2</sub><sup>n</sup>. For instance, ```–n 1``` specifies D<sub>2</sub><sup>n=1</sup>. When ```-n``` is specified, only D<sub>2</sub><sup>n</sup> is run regardless of specification in -d. |
| ```-t <t>```      | ```<t>``` is the number of threads to use in the analysis. Default: 4 |

## Citation
If you use jD2Stat or D<sub>2</sub><sup>n</sup> in your work, please cite:

Chan CX, Bernard G, Poirion O, Hogan JM and Ragan MA (2014). Inferring phylogenies without multiple sequence alignment. *Scientific Reports* **4:** 6504. http://dx.doi.org/10.1038/srep06504.

This replaces the the original URL indicated in the paper, hosted on bioinformatics.org.au.
