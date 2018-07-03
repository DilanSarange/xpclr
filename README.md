# XP-CLR

Code to compute xp-clr values as per [Chen, Patterson & Reich 2010](https://www.ncbi.nlm.nih.gov/pubmed/20086244).
This implementation was written due to found bugs in the source of the original tool.

## Installation

Clone this git repository into your working directory and `cd`.

```
python setup.py install
```

Not yet available on PyPi/bioconda

## Use

This is a python module with a convenience script attached. 
It is designed to run on hdf5 files representing genetic data as generated using [scikit-allel](http://alimanfoo.github.io/2017/06/14/read-vcf.html).
Support is available for the text files in same format as original XPCLR tool, but has not been optimised for this. 
I hope to add support for VCF and zarr formats soon.

Interface is under development and may change/break in future.

## Documentation

```
usage: xpclr [-h] --out OUT [--hdf5 HDF5] [--gdisthdf5 GDISTHDF5]
             [--samplesA SAMPLESA] [--samplesB SAMPLESB] [--rrate RRATE]
             [--map MAP] [--popA POPA] [--popB POPB] --chr CHROM
             [--ld LDCUTOFF] [--phased] [--verbose] [--maxsnps MAXSNPS]
             [--minsnps MINSNPS] [--size SIZE] [--start START] [--stop STOP]
             [--step STEP]

Tool to calculate XP-CLR as per Chen, Patterson, Reich 2010

optional arguments:
   -h, --help            show this help message and exit
  --out OUT, -O OUT     output file
  --hdf5 HDF5, -I HDF5  input hdf5 filestem
  --gdisthdf5 GDISTHDF5
                        key for genetic position in variants table of hdf5
  --samplesA SAMPLESA, -Sa SAMPLESA
                        Which samples comprise population A. Comma separated
  --samplesB SAMPLESB, -Sb SAMPLESB
                        Which samples comprise population B. Comma separated
  --rrate RRATE, -R RRATE
                        recombination rate per base
  --map MAP             input map file as per XPCLR specs
  --popA POPA           filepath to population A genotypes
  --popB POPB           filepath to population A genotypes
  --chr CHROM, -C CHROM
                        Which contig analysis is based on
  --ld LDCUTOFF, -L LDCUTOFF
                        LD cutoff to apply for weighting
  --phased, -P          whether data is phased for more precise r2 calculation
  --verbose, -V         whether to be verbose
  --maxsnps MAXSNPS, -M MAXSNPS
                        max SNPs in a window
  --minsnps MINSNPS, -N MINSNPS
                        min SNPs in a window
  --size SIZE           window size
  --start START         start base position for windows
  --stop STOP           stop base position for windows
  --step STEP           windows step for slide
```

## File formats

`hdf5` as generated by [scikit-allel](http://alimanfoo.github.io/2017/06/14/read-vcf.html).

Or

`.geno`
Space delimited file, containing 0/1s with sample haplotypes as columns, and rows as SNPs.

`.map`
Space delimited file. 6 columns: ID, chromosome, Genetic Distance, Position, REF, ALT.

For examples of these files see the [example](https://github.com/hardingnj/xpclr/tree/master/example) folder. 

