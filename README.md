# ped_sort_and_renumber
ped_sort_and_renumber — A fast pedigree sorting and renumbering tool. It is optimized for speed and efficiently handling large pedigree files with complex ancestor-descendant relationships.

## Description:

ped_sort_and_renumber is a highly efficient Python utility designed to process large pedigree files quickly. It performs two main functions:

1. Topological Sorting of pedigree records to ensure ancestors (sire/dam) appear before their descendants.
2. Renumbering of all unique IDs (animals, sires, and dams) into a consistent integer-based format, while retaining the original ID for traceability.

This is particularly useful for preparing input files for genetic analysis software or simulation tools that require pedigrees in a specific order or numeric ID format as well as sorted pedigree.

## Usage:
python ped_sort_and_renumber <pedigree_file>

## Input file format:

    CSV (comma-delimited)
    No header row
    Columns: Animal, Sire, Dam
    Missing parent values can be: 0, ., or -

    Example input:
    50,4,19
    1,A,0
    2,1,B
    3,1,2
    10,5,6
    k,1,B
    R,A,19
    6,4,11
    60,1,2

## Output files:

    1. <pedigree_file>.SORTED

    Pedigree sorted topologically so that ancestors precede descendants
    Missing parents are retained as-is (e.g., 0, ., etc.)

    Example output file <pedigree_file>.SORTED:
    A,0,0
    1,A,0
    4,0,0
    B,0,0
    11,0,0
    2,1,B
    6,4,11
    19,0,0
    5,0,0
    50,4,19
    3,1,2
    10,5,6
    k,1,B
    R,A,19
    60,1,2


    2. <pedigree_file>.SORTED_RENUM

    All unique IDs (animals, sires, dams) are renumbered with consistent integer identifiers. The fourth column retains the original ID for reference

    Example output file <pedigree_file>.SORTED_RENUM:
    1,0,0,A
    2,1,0,1
    3,0,0,4
    4,0,0,B
    5,0,0,11
    6,2,4,2
    7,3,5,6
    8,0,0,19
    9,0,0,5
    10,3,8,50
    11,2,6,3
    12,9,7,10
    13,2,4,k
    14,1,8,R
    15,2,6,60

