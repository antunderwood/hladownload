# hladownload<br>*A tool for downloading HLA alleles, epitopes and frequencies* 
As HLA alleles, epitopes/eplets and frequencies often need to be manually downloaded and parsed, I developed several scripts which could automatically download and parse these data for my Bachelor's thesis project. In order to make this available to the public I combined these scripts and developed this tool.

With this tool you will be able to automatically download HLA allele sequencies/alignments from the [IMGT/HLA database's github](https://github.com/ANHIG/IMGTHLA), epitopes/eplets from [the eplet registry](https://www.epregistry.com.br) and HLA frequencies from [the HLA frequency database](http://www.allelefrequencies.net). 

This can either be done through the [command line program](#command-line-program) or in python through [the separate modules](#python-modules) (`hla`, `eplet` and `frequency`). When doing the latter additional functionalties will be avaiable. The `hla` module, for example, will give you access to an `HLA` object which allows you to programatically retrieve, parse and slice HLA alleles by their codon positions.

## Installation
There are several ways to use and install this program.
* ```python -m hladownload``` When this or an OS equivelant command is run in a folder with the files of this repository, the command line program can be used without any further installation. However, it is required that the python dependencies listed in `setup.py` are installed.
* ```python setup.py install``` This command must also be run in a folder with the repository files. The tool will then be installed under the current used python installation and will be available on the command line or in python through the name '`hladownload`'.
* ```pip install hladownload``` This command will download the tool through pip. **Not available yet as of now!**

## Command line program
The command line program has several arguments which will be explained and highlighted in an example here.

### Output flags
These flags will enable you to specify the desired output: HLA allele sequences, eplets or frequencies. The output can further be restricted by providing alleles for which sequences, eplets and/or frequencies should be reported (see `-a` or `-A` under [Other arguments](#other-arguments)). Not all HLA loci are available for every type of output:
* `-H, --HLA` Flag to indicate that HLA alleles should be saved as multiple sequence alignments in fasta format per locus. These allele frequencies are retrieved from [the IMGT/HLA database github](https://github.com/ANHIG/IMGTHLA).<br>*Supported loci: A, B, C, DRA, DRB1, DRB3, DRB4, DRB5, DRB345, DQA1, DQA2, DQB1, DPA1, DPB1*
* `-E, --eplet` Flag to indicate that eplets should retrieved from [the eplet registry database](https://www.epregistry.com.br) and outputted them into three csv files containing a summary (`summary_table-eplets.csv`), allele-eplet associations (`allele_table-eplets.csv`) and residues per eplet (`residue_table-eplets.csv`).<br>*Supported loci: A, B, C, DRB1, DRB3, DRB4, DRB5, DRB345, DQA1, DQB1, DPA1, DPB1*
* `-F, --frequency` Flag to indicate that HLA allele frequencies should be retrieved from [the allele frequency database](http://www.allelefrequencies.net) and outputted into two table files: One with the average allele frequency per region and the other globally (averaged over all (specified) regions). The total sample size is also calculated per row.<br>*Supported loci: A, B, C, DRB1, DQA1, DQB1, DPA1, DPB1*

### `-H` additional arguments
  * `-t, --slice_type {no_gaps,gaps,amino}` Can only be used if '-H' is given as a flag. Indicate whether the sliced codons should include gaps, no gaps or should be translated to amino acids. These gaps are only referring to those that are introduced into the reference sequence due to the alignment. Gaps are included by default.
  * `-s, --slice_range SLICE_LOCI SLICE RANGES` Can only be used if '-H' is given as a flag. Indicate the codons of the HLA alleles per locus that should be preserved in the outputted alignment files. The arguments should consist of a comma-separated list of loci, followed by a combination of ranges and comma separated numbers for the colons to preserve: e.g. `-s A,B,C 1-5,10` means codons 1 up to (but not including) 5 and 10 of loci A, B and C should be preserved. You can also specify different codons for different loci by repeating the argument, e.g. `-s A,B 1-5 -s DRB1,DRB345 5-8 etc.`. By default all codons of the aligned alleles of a locus will be preserved if that locus is not specified.

### `-E` additional arguments
* `-l, --all_eplets` Flag to indicate that all eplets should be included, as any eplets which are not associated with any (specified) alleles are removed from the output by default.

### `-F` additional arguments
* `-r, --region REGION1 REGION2 etc...` Indicate the regions separated by spaces for which the HLA frequencies should be retrieved. A region consisting of multiple words should be enclosed in quotes. If no regions are specified all of the regions will be reported. If it is specified the global frequencies will only be based on the average of those regions. <br>*Usable regions are: Australia, Europe, North Africa, North America, North-East Asia, Oceania, South and Central America, South Asia, South-East Asia, Sub-Saharan Africa, Western Asia*
* `->, --higher_resolution` Flag to indicate that frequencies of higher resolution alleles of the specified alleles (see '-a' or '-A') should also be reported.
* `-<, --lower_resolution` Flag to indicate that frequencies of lower resolution alleles of the specified alleles (see '-a' or '-A') should also be reported.

### Other arguments
* `-h, --help` Show an help message and exit.
* `-o, --output_directory OUTPUT_DIRECTORY` Directory to save the output files to. For every output flag (`-H`, `-E` or `-F`) that is enabled, a separate directory (`/alleles`, `/eplets` or `/frequencies`) will be created in the output folder with the output files. The output folder defaults to the current folder.
* `-d, --database_version DATABASE_VERSION` The IMGT/HLA database version github (https://github.com/ANHIG/IMGTHLA) to use to retrieve HLA alleles from. Defaults to the latest branch.
* `-a, --alleles ALLELES` Indicate the HLA alleles for which an alignment, frequencies and/or eplets should be outputted. The alleles can be a combination of ranges and comma separated allele names without spaces: 'A\*01:01:01:01-A\*01:01:01:09,B\*01:01:01:01'. The default is all alleles for all loci that are included in the given IMGT/HLA database version.
* `-A, --alleles_file ALLELES_FILE` Indicate in a file the HLA alleles for which an alignment, frequencies and/or eplets should be outputted. The allele names should be separated by new lines in the file. This argument overrides the alleles specified with `-a`.
* `-n, --no_null` Flag to indicate whether HLA null alleles should be excluded.
* `-g, --group_DRB345` Flag to indicate whether HLA alleles of the DRB3, -4 and -5 loci should be grouped under a single locus 'DRB345'.

### Examples
**Will be updated later!**

## Python modules
**Will be updated later!**

### HLA module

### Eplet module

### Frequency module
