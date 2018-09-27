# ChIAPoP
ChIAPoP: an integrated tool for ChIA-PET data analysis

# Prerequisite tools
* `bowtie` (http://bowtie-bio.sourceforge.net/index.shtml) for read alignment
* `macs2` (https://github.com/taoliu/MACS) for peak calling

If `bowtie` and `macs2` are not installed in a system search path (e.g. `/usr/bin`), users will need to specify their installation directory  paths with the parameters `bowtie.path` and `macs2.path` for `bowtie` and `macs2`, respectively.  

# Download and Installation

  ```
* git clone https://github.com/wh90999/ChIAPoP
* cd ChIAPoP
* R CMD INSTALL ChIAPoP_0.99.9.5.tar.gz
```
# Documentation
The full ChIAPoP R Package manual is available at https://github.com/wh90999/ChIAPoP/blob/master/ChIAPoP-manual.pdf.

# Quick start

The simplest way to use ChIAPoP package is to use ChIAPoP’s pipeline. The pipeline takes input data of two fastq reads files (e.g., read_1.fq and read_2.fq) from ChIA-PET experiment with the original protocol, as well the basename of the genome reference index of bowtie and the associated genome reference name (e.g. hg19). In addition, users also need specify bowtie and macs2 installation paths. The pipeline then does all analysis work including: linker trimming and reads separation, reads alignment, aligned reads filtering, peaking calling, model parameter estimation, calculation of statistical significance of potentially interactive pairs of DNA regions (potential pairs), and giving the final reports with tables and figures. For more advanced analysis, users can use ChIAPoP pipeline individual functions for gaining fine control of their ChIA-PET data analysis. Please see the ChIAPoP reference manual for all functions available and their usages. A simple usage of the pipeline is given as the following.

This example is to run a full ChIAPoP analysis of a human ChIA-PET data (read_1.fq and read_2.fq) with the reference genome hg19. In this example, the two input fastq files and the bowtie index files (with prefix hg19) of the human genome reference hg19 are all in the direcotory /data_dir/ (so the basename of the genome reference index to be searched by bowtie is /data_dir/hg19). Bowtie index files for many common reference genomes are available at ftp://ftp.ccb.jhu.edu/pub/data/bowtie_indexes/, e.g., hg38/GRCh38 bowtie index and hg19 bowtie index. The pipeline also requires the full command line paths for both bowtie read alignment tool and macs2 peak calling tool if they are not in the system search paths. The example assumes both tools are in the system search paths.

Some good testing ChIA-PET datasets can be downloaded at [https://www.ebi.ac.uk/ena/data/view/PRJNA148637]. The datasets were used to study long-range chromatin interactions associated with RNA polymerase II in human cells. It is easy to modify the example codes to run the test analysis with this real ChIA-PET dataset.

The default genome reference for the pipeline is the human genome reference hg19. Users can use other genome reference and its bowite index with addtional optional parameters. The example shows all parameters for the pipeline.
```
library(ChIAPoP)
pop.pipeline(fastq.1="/data_dir/read_1.fq",
             fastq.2="/data_dir/read_2.fq",
             bowtie.index="/data_dir/hg38",
             bowtie.path="/tool_dir/bowtie", 
             macs2.path="/tool_dir/macs2", 
             gsize = "hs", chr.include = "all",
             ref.genome = "hg38");
```
