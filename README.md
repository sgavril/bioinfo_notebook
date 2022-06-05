https://www.metagenomics.wiki/tools/short-read/ncbi-sra-file-format/prefetch
Download sra files using sratoolkit:

mkdir sra

cd sra

 ~/software/sratoolkit/sratoolkit.2.11.0-centos_linux64/bin/prefetch --option-file acc.txt
 
for var in sra/*.sra; do fastq-dump --outdir fastq --split-3 $var; done

Download metadata
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=sra&retmode=json&id=ERR1034587


How to mount windows network drives in wsl:
https://www.public-health.uiowa.edu/it/support/kb48568/


You first check out for the name of the package you want to remove:

dpkg --list

Then remove the given package

sudo apt-get remove package_name

Purge any related code

sudo apt-get purge package_name

Then Autoremove

sudo apt-get autoremove

Finally, do a clean so you check everything is correctly removed

sudo apt-get clean

https://docs.nvidia.com/cuda/wsl-user-guide/index.html


https://academic.oup.com/femsec/article/90/3/543/536864?login=true
http://mb3is.megx.net/gustame
