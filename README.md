# DiscoSNP++ description

Software discoSnp is designed for discovering Single Nucleotide Polymorphism (SNP) from raw set(s) of reads obtained with Next Generation Sequencers (NGS).
Note that number of input read sets is not constrained, it can be one, two, or more. Note also that no other data as reference genome or annotations are needed.
The software is composed by two modules. First module, kissnp2, detects SNPs from read sets. A second module, kissreads, enhance the kissnp2 results by computing per read set  and for each found SNP i/ its mean read coverage and ii/ the (phred) quality of reads generating the polymorphism.

## Build image

Clone the repository and enter the directory
    
```bash
git clone https://github.com/cmonjeau/docker-discosnppp.git
cd docker-discosnppp
```


Build the dockerfile

```bash
docker build -t cmonjeau/discosnppp .
```

## Run DiscoSNP++

Print DiscoSNP++ help

```bash
docker run -it --rm cmonjeau/discosnppp
```

Run DiscoSNP++ with data (inside `/home/user/discoSNP_data` directory)

```bash
docker run -it --rm -v /home/user/discoSNP_data:/data cmonjeau/discosnppp -r "/data/reads_sequence1.fasta.gz /data/reads_sequence2.fasta.gz" -G /data/reference_genome.fa -p /data/results/discoRes
```


## Run DiscoSNP++ using [Godocker](http://www.genouest.org/godocker/)

Create a new job with these parameters:

"Container image" : cmonjeau/discosnppp

"Command" : 

```bash

#!/bin/bash

# command line example (adapt with your data)
/opt/DiscoSNP++-v2.2.9-Source/run_discoSnp++.sh -r "$GODOCKER_HOME/discoSNP_data/reads_sequence1.fasta.gz $GODOCKER_HOME/discoSNP_data/reads_sequence2.fasta.gz" -G $GODOCKER_HOME/discoSNP_data/coli.fasta -p $GODOCKER_HOME/discoSNP_data/result

```

"Mount volumes" : home(rw)


