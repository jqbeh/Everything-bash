# General

Everyday codes for data wrangling.

### Print IDs in list A that do not match list B 
```
grep -v -f listB.txt listA.txt > newlist.txt
```
or
``` 
cat listA.txt listB.txt > combined.txt
sort combined.txt | uniq -d | grep -vFxf - combined.txt > diff.txt
```

### Extract metadata rows belong to IDs.txt
```
grep -Ff ids.txt allmetadata.txt > extracted_rows.txt
```




