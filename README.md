## ped sort and renumber
ped_sort_and_renumber is a fast and highly efficient utility for pedigree sorting and renumbering. It is optimized for speed and designed to handle large pedigree files with complex ancestor–descendant relationships.

### Description:

ped_sort_and_renumber performs several key functions:
1. Checks the pedigree, including adding any parents not listed as animals to the animal column.
2. Performs pedigree loop checks to detect cycles.
3. Identifies animals that appear as sires and dams.
4. Applies topological sorting to ensure that ancestors (sires and dams) appear before their descendants.
5. Renumbers all IDs (animals, sires, and dams) into a consistent integer-based format, while retaining the original IDs for traceability.

Pedigree checking is crucial for all genetic analyses. Additionally, some software packages require pedigrees to be sorted and possibly renumbered such that offspring IDs are always greater than those of their parents.

### Usage:
```
./ped_sort_and_renumber <pedigree_file>
```

### Input pedigree file format:

    -CSV (comma-delimited)
    -No header row
    -Columns are: Animal, Sire, Dam
    -IDs of missing parents can be: 0 or blank (i.e., ",,")
    -Animal ID can not be 0
    -If animal ID is blank, the animal and its parents are ignored

#### Example input pedigree file:
```
50,4,19
1,A,0
2,1,B
3,,2
10,5,0
k,1,B
R,,0
6,4,11
60,1,2
```

### Output files for this example pedigree:

1. <pedigree_file>.sorted:
   
This file includes pedigree sorted topologically so that ancestors precede descendants. IDs of missing parents are 0.

<pedigree_file>.sorted for this example:

```
A,0,0
1,A,0
B,0,0
2,1,B
4,0,0
19,0,0
5,0,0
11,0,0
50,4,19
3,0,2
10,5,0
k,1,B
R,0,0
6,4,11
60,1,2
```

2. <pedigree_file>.sorted_renumbered
   
All unique IDs (animals, sires, dams) are renumbered with consistent integer identifiers. The fourth column retains the original ID for reference

Output <pedigree_file>.sorted_renumbered for this example:
```
1,0,0,A
2,1,0,1
3,0,0,B
4,2,3,2
5,0,0,4
6,0,0,19
7,0,0,5
8,0,0,11
9,5,6,50
10,0,4,3
11,7,0,10
12,2,3,k
13,0,0,R
14,5,8,6
15,2,4,60
```
3. sire_dam_not_appear_as_animal_and_added.csv
   
Sires and dams that do not appear in the animal column are added and listed in this file. 

Output <sire_dam_not_appear_as_animal_and_added.csv> for this example:
```
4,sire
19,dam
A,sire
B,dam
5,sire
11,dam
```


