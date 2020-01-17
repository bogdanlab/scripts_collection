# To use PLINK

```bash
. /u/local/Modules/default/init/modules.sh
module load plink
```

# To merge a list of bfile
```bash
# this is a string, e.g., "bfile1 bfile2 bfile3"
bfile_list=a-list-of-bfile
# convert it to an array
bfile_list=($bfile_list)
# length of the list
len=${#bfile_list[@]}
# Generate the merge file list
for ((i=1; i<$len; i++ )); do
prefix=${bfile_list[$i]}
echo "${prefix}.bed ${prefix}.bim ${prefix}.fam" >> merge_file_list.txt
done
# do the merge
plink --bfile ${bfile_list[0]} --merge-list merge_file_list.txt --make-bed --out merged
```

# Extracting a subset of SNPs and individuals
```python
import pandas as pd
from os.path import join
# Extract the first `num_indv` individuals and first `num_snps` SNPs
def extract_plink_subset(bfile, num_indv, num_snps, out_dir='./'):
    famid = pd.read_csv(bfile + '.fam', delim_whitespace=True, header=None)[0]
    snpid = pd.read_csv(bfile + '.bim', delim_whitespace=True, header=None)[1]
    
    famid[0:num_indv].to_csv(join(out_dir, 'subset.indv'), index=False, header=None)
    snpid[0:num_snps].to_csv(join(out_dir, 'subset.snp'), index=False, header=None)
```
```bash
# use plink to get the genotype
plink --bfile ${bfile} --extract ./subset.snp --keep-fam ./subset.indv --make-bed --out ${out_bfile}
```
