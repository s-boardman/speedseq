#speedseq         
-------------------------------

**Current version:** 0.0.1a

Created by Colby Chiang, Ryan Layer, Greg G Faust, Michael R Lindberg, Aaron R Quinlan, and Ira M Hall.

Current support for Linux only

##Summary
--------------
The ``speedseq`` suite is a lightweight, flexible, and open source pipeline that identifies
genomic variation (Structural Variants, INDELs, and Single Nucleotide Variants). 
There are two modes of analysis supported: 

**1.) Identification of variants in a single sample.**

**2.) Comparison of two samples, i.e. tumor and matched normal**

##Constitutive Pipeline Tools (Required)
------------------------------------------

1.) [BWA](https://github.com/lh3/bwa)

2.) [FREEBAYES](https://github.com/ekg/freebayes)

3.) [GEMINI](https://github.com/arq5x/gemini)

4.) [LUMPY](https://github.com/arq5x/lumpy-sv)

5.) [PARALLEL](http://www.gnu.org/software/parallel/)

6.) [SAMBAMBA](https://github.com/lomereiter/sambamba)

7.) [SAMBLASTER](https://github.com/GregoryFaust/samblaster)

8.) [SNPEFF](https://github.com/CBMi-BiG/snpEff)

9.) [VCFLIB](https://github.com/ekg/vcflib)


##Installation
----------------

There is an automatic (coming soon) and manual installation process for ``speedseq``.

The following are required for both modes of installation:
- **cmake**
- **g++**
- **gcc**
- **git**
- **make**
- **zlib**


Use a Linux package installer to obtain these:

~~~~~~~~~~~~~~~~~~~
sudo yum -y install gcc-c++ make git gcc zlib-devel cmake cmake-gui
~~~~~~~~~~~~~~~~~~~
 
or 

~~~~~~~~~~~~~~~~~~~
sudo apt-get install gcc-c++ make git gcc zlib-devel cmake cmake-gui
~~~~~~~~~~~~~~~~~~~

###Automatic installation (coming soon)

``speedseq`` can be installed with the following commands: 
~~~~~~~~~~~~~~~~~~
	git clone https://github.com/cc2qe/speedseq
	cd speedseq
	sudo python setup.py install
	sudo cp -r bin/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~

###Manual installation

The following instructions for installation assumes that the required tools are not installed.  
It is recommended that the specified versions of tools are used for this release of ``speedseq``.  
The use of unspecified versions of any pipeline tool cannot be guaranteed to work. 

``speedseq`` can be installed with the following commands: 
~~~~~~~~~~~~~~~~~~
	git clone https://github.com/cc2qe/speedseq
	cd speedseq
	sudo cp -r bin/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~

Obtain each of the pipeline tools and install them:
	
####1.) BWA

``bwa`` can be installed and used by ``speedseq`` with the following commands: 
~~~~~~~~~~~~~~~~~~
	curl -OL http://sourceforge.net/projects/bio-bwa/files/bwa-0.7.6a.tar.bz2
	tar -xvf bwa-0.7.6a.tar.bz2
	cd bwa-0.7.6a
	make
	sudo cp bwa /usr/local/bin
~~~~~~~~~~~~~~~~~~
	
####2.) FREEBAYES

``freebayes`` can be installed and used by ``speedseq`` with the following commands: 
~~~~~~~~~~~~~~~~~~~
	git clone --recursive git://github.com/ekg/freebayes.git
	cd freebayes
	cmake
	sudo scp -r bin/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~~

####3.) GEMINI

``gemini`` can be installed and used by ``speedseq`` with the following commands: 

Python 2.7.x
grabix
samtools
tabix
bedtools
pybedtools

##1.) BEDTOOLS
	
``bedtools`` can be installed and used by ``speedseq`` with the following commands: 
~~~~~~~~~~~~~~~~~~
	curl -OL https://github.com/arq5x/bedtools2/releases/download/v2.19.0/bedtools-2.19.0.tar.gz
	tar -xvf bedtools-2.19.0.tar.gz
	cd bedtools-2.19.0
	make
	sudo scp -r bin/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~


Once the the necessary packages have been acquired, install gemini:

~~~~~~~~~~~~~~~~~~
	git clone https://github.com/arq5x/gemini
	cd gemini
	sudo python setup.py install
	sudo python gemini/install-data.py /usr/local/share/
~~~~~~~~~~~~~~~~~~

####4.) LUMPY

``lumpy-sv`` can be installed and used by ``speedseq`` with the following commands:
~~~~~~~~~~~~~~~~~~~
	curl -OL https://github.com/arq5x/lumpy-sv/releases/download/v0.1.5.tar.gz
	tar -xvf v0.1.5.tar.gz
	cd v0.1.5
	make 
	sudo cp -r bin/* /usr/local/bin/
	sudo cp -r scripts/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~~

####5.) PARALLEL

``parallel`` can be installed and used by ``speedseq`` with the following commands:
~~~~~~~~~~~~~~~~~~~
	curl -OL http://ftp.gnu.org/gnu/parallel/parallel-20100424.tar.bz2
	tar -xvf parallel-20100424.tar.bz2
	cd parallel-20100424
	make 
	sudo cp -r bin/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~~


####6.) SAMBAMBA

``sambamba`` can be installed and used by ``speedseq`` by: 

-Go to https://github.com/lomereiter/sambamba/releases

-Download sambamba_v0.4.4_centos5.tar.bz2
~~~~~~~~~~~~~~~~~~
	tar -xvf sambamba_v0.4.4_centos5.tar.bz2
	sudo scp sambamba_v0.4.4 /usr/local/bin/
~~~~~~~~~~~~~~~~~~

####6.) SAMBLASTER

``samblaster`` can be installed and used by ``speedseq`` with the following commands: 
~~~~~~~~~~~~~~~~~~
	git clone git://github.com/GregoryFaust/samblaster.git
	cd samblster
	make
	sudo cp bin/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~

####7.) SNPEFF

``snpeff`` can be installed and used by ``speedseq`` with the following commands: 
~~~~~~~~~~~~~~~~~~
	wget http://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip/download
	unzip snpEff_latest_core.zip
	cd snpEff
	sudo scp *jar /usr/local/bin/
	sudo scp snpEff.config /usr/local/bin
	sudp scp -r scripts/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~

####8.) VCFLIB

``vcflib`` can be installed and used by ``speedseq`` with the following commands: 
~~~~~~~~~~~~~~~~~~
	git clone --recursive  https://github.com/ekg/vcflib
	cd vcflib
	make
	sudo cp bin/* /usr/local/bin/
~~~~~~~~~~~~~~~~~~

For alternative installations and release issues please consult the website/creator of the tool in question.

##Example Usage
----------------------

Use ``speedseq aln`` to align and dedupe the dataset.
~~~~~~~~~~~~~~~~~~
	speedseq aln -o NA12878 human_g1k_v37.fasta NA12878.fq.gz
~~~~~~~~~~~~~~~~~~

Use ``speedseq var`` to call SNPs and indels on a single sample.
~~~~~~~~~~~~~~~~~~
	speedseq var -o NA12878 -w annotations/ceph18.b37.include.2014-01-15.bed human_g1k_v37.fasta NA12878.bam
~~~~~~~~~~~~~~~~~~

Use ``speedseq lumpy`` to call structural variants.
~~~~~~~~~~~~~~~~~~
	speedseq lumpy -o NA12878 -x annotations/ceph18.b37.exclude.2014-01-15.bed -B NA12878.bam -D NA12878.discordants.bam -S NA12878.splitters.bam
~~~~~~~~~~~~~~~~~~

Use ``speedseq somatic`` to call SNPs and indels on a tumor/normal pair.
~~~~~~~~~~~~~~~~~~
	speedseq somatic -o TCGA-B6-A0I6 -w annotations/ceph18.b37.include.2014-01-15.bed human_g1k_v37.fasta TCGA-B6-A0I6.normal.bam TCGA-B6-A0I6.tumor.bam
~~~~~~~~~~~~~~~~~~




