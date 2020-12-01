# Montagem e curadoria de genomas
Passo a passo para montagem de genomas

## Estrutura de diretórios

## Pré-processamento

Para investigar a qualidade do sequenciamento pode-se usar o FastQC:
```
fastqc reads_R1.fastq reads_R2.fastq -o FastQC
```
Para facilitar a investigação os resultados podem ser compilados em gráficos únicos interativos, via multiqc:
```
multiqc --interactive FastQC
```

Amostrar reads:
```
seqtk sample <file.fastq> <fraction>|<number> > <fastq_VALUE.fastq>
```

Trimagem de reads:
```
java -jar trimmnomatic.jar <options>
```
http://www.usadellab.org/cms/?page=trimmomatic

## Montagem

Spades:
```
spades -1 reads_R1.fastq -2 reads_R2.fastq -o spadesAssembly
```
Edena:
```
edena -paired reads_R1.fastq reads_R2.fastq
edena -edenaFile out.ovl
```

## Scaffolding

Contiguator:
```
python contiguator -c <Contigs> -r <reference.fasta> -f <PREFIX>
```

Fechamento de gaps:
```
java -Xms2G -Xmx4G -jar GenomeFinisher.jar -i <PseudoContig.fasta> -ds <Contigs.fasta> -ref <reference.fasta> -o <output_dir>
``` 
## Curadoria
