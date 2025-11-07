# Manipulating sequences

### To unwrap FASTA seq liners
A lot of software outputs wrapped FASTA files, where sequence lines are truncated at a certain number of characters and continued on the following line.
To unwrap:
```
perl -pe '$. > 1 and /^>/ ? print "\n" : chomp' input.fasta > output.fasta
```

### Get sequence length
Delete header lines and gaps, then count how many characters each line has.
*NOTE: Before doing this, make sure the FASTA file is unwrapped.*
```
sed -e "/^>/d" -e "s/-//g" input.fasta | awk '{ print length }' > lengths.txt
We can count the number of each unique length:
sed -e "/^>/d" -e "s/-//g" input.fasta | awk '{ print length }' | sort | uniq -c | sort -hr
```

### Print FASTA headers
grep "^>" input.fasta | sed -e "s/>//" > headers.txt

### Generate random FASTA seq
Make 30 random sequences, each 300 bases long
```
paste -d '\n'     <(for i in {01..30}; do echo ">seq$i"; done)     <( cat /dev/urandom | tr -dc 'ATCG' | fold -w 300 | head -n 30 )     > output.fasta
```

### Replace bases
```
sed -e "/^[^>]/s/-//g" input.fasta > output.fasta
sed -e "/^[^>]/s/[YRWSKMDVHBX]/N/g" input.fasta > output.fasta
```

### Rename FASTQ files 
Rename FASTQ files from _1.trimmed.fastq.gz to _R1.trimmed.fastq.gz
```
for f in *_1.trimmed.fastq.gz; do mv -- "$f" "${f/_1.trimmed/_R1.trimmed}"; done
for f in *_2.trimmed.fastq.gz; do mv -- "$f" "${f/_2.trimmed/_R2.trimmed}"; done
```



