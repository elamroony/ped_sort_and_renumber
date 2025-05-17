# ped_sort_and_renumber
ped_sort_and_renumber — A fast pedigree sorting and renumbering tool. It is optimized for speed and efficiently handling large pedigree files with complex ancestor-descendant relationships.

Description:

ped_sort_and_renumber is a highly efficient Python utility designed to process large pedigree files quickly. It performs two main functions:

1. Topological Sorting of pedigree records to ensure ancestors (sire/dam) appear before their descendants.
2. Renumbering of all unique IDs (animals, sires, and dams) into a consistent integer-based format, while retaining the original ID for traceability.

This is particularly useful for preparing input files for genetic analysis software or simulation tools that require pedigrees in a specific order or numeric ID format as well as sorted pedigree.

Usage:
python ped_sort_and_renumber <pedigree_file>

    Input file format:

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

Output files:

    <input_file>.SORTED

        Pedigree sorted topologically so that ancestors precede descendants
        Missing parents are retained as-is (e.g., 0, ., etc.)
        Example:

    A,0,0
    1,A,0
    4,0,0
    ...

<input_file>.SORTED_RENUM

    All unique IDs (animals, sires, dams) are renumbered with consistent integer identifiers
    The fourth column retains the original ID for reference

    Example:

        1,0,0,A
        2,1,0,1
        3,0,0,4
        ...

