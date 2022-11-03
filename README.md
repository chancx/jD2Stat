# jD2Stat
jD2Stat (previously known as JIWA*) is a Java package that utilises a series of 􀜦2 statistics to
extract k-mers (subsequences at defined k length) from a set of biological sequences, and generate
pairwise distances for each possible pair. This distance can be used directly for phylogenetic inference
using neighbour-joining.

*: This program is not to be confused with, and has no relation to, the proprietary trademark and
software of Jiwa Financials, North Sydney, Australia.

The D2 methods included are:
D2 based on exact k-mer counts (D2)
D2S - similar to 􀜦􀬶, normalised based on probability of occurrences of specific k-mers (D2S)
D2∗ - similar to 􀜦􀬶, normalised based on means and variance (D2St)
D2n - extension of 􀜦􀬶 to allow for n number of wildcards (n neighbourhood)

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
For each D2 analysis, jD2Stat generates a pairwise distance matrix in PHYLIP format, which can be
used as input for neighbor in PHYLIP to infer a phylogenetic tree using neighbour-joining.

