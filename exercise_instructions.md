# Exercises - First steps with UNIX

*Note:* some exercises contain an **Additional Tasks** section, which you can
do if you have the time after having completed the main exercise. The
Additional Tasks sections will not be corrected in class.

<br>


## Exercise 1 - Navigating the filesystem in command line
**Objective:** get familiar with navigating the directory tree.

* Print your current working directory with the `pwd` command. This will
  show you where you currently are in the directory tree.
* If you are not already in the directory of the practicals, navigate to it
  using the `cd` command (if you are already in the practical's directory, then
  navigate to its parent with `cd ..` and then go back to it).
* List the content of the practical's directory with `ls`.
* Enter the `files` sub-directory.
* List of content of the `files` sub-directory with `ls -l` and `ls -lh`:
  * What does the `-l` and `-h` options do?
  * List the content of the directory in chronological order (oldest file
    first) and in reverse chronological order (newest file first).

<br>

**Additional Tasks:**
* Try the `cd ~` and `cd -` shortcuts.


<br>
<br>


## Exercise 2 - File globbing with wildcard characters
File **globbing** is the expansion of **wildcard characters** by the shell to
match existing file names.

Go to directory `practicals/sandbox` and perform the following tasks:
* List all files names *starting* with character `x`.
* List all files names *containing* the character `x`.
* List file names containing an `x` followed by one random character, followed
  by the character `r`.
* List file names containing an `x` and ending with any letter between `a` and
  `c` (example: `axona` or `exonic`).

<br>

**Additional Tasks:**
* Try to add quotes (single or double) around the pattern with the wildcard:
  what do you observe?
* Can you think of a use case for using quotes around a wildcard?


<br>
<br>


## Exercise 3 - Creating and moving directories and files
1. **Create the following directories Using the `mkdir` command:**
   * In the `files` directory, create the sub-directories `exercises` and `play`.
   * In `files/play`, create the sub-directories `micro-array` and `grep`.
   * In `files/exercises`, create directories `ex1-explore`, `ex2-merge` and
     `ex3-retrieval`.

2. **Copy files using the `cp` command:**
   * Make a copy of `files/uniprot-thioredoxin.fas` in directory `play/grep/`.

3. **Move files and directories with the `mv` command:**
   * Move the file `rat_virus.dat` to the directory `exercises/ex1-explore/`.
   * Move the files `seq1.fas`, `seq2.fas`, `seq3.fas` and `seq4.fas` to the
     directory `exercises/ex2-merge/`.
   * Move the file `uniprot-thioredoxin.fas` to the directory
     `exercises/ex3-retrieval/`.
   * Move the files `arrayDat-1.csv`, `arrayDat-2.csv` and `arrayDat-3.csv` to
     the directory `play/micro-array/`.

4. **Rename files and directories with the `mv` command:**
   * Rename the file `exercises/ex3-retrieval/uniprot-thioredoxin.fas` to
     `thioredoxin.fas` (leave the file at the same location).

<br>

**Additional Tasks:**


<br>
<br>


## Exercise 4 - Find and identify
Go to directory `practicals/sandbox/` and answer the following questions:
* What is the format of the file `create_million_line_file.sh` ?
* Find files with either extension `.jpeg` or `.png`.
* Find all `jpeg` files bigger than `10 ko`.

<br>

**Additional Tasks:**


<br>
<br>


## Exercise 5 - Display file content
Locate the file `uniprot-thioredoxin.fas`, navigate to it, then use the
following commands:

1. **Display the start/end of a file** using the **`head`** and **`tail`**
   commands.
   * Display the first 10 lines of the file.
   * Display the last 5 lines of the file.

2. **Count the number of lines** in a file using the **`wc`** command:
   * Count only the number of lines in the file.
   * Count only the number of words in the file.

3. **Display the content** of the file using the **`cat`** command:
   * Why is this not the most adapted program here?
   * Indicate another usage of cat?

4. **Display, navigate and search** a file with **`less`**.
   * Open the file using `less`.
   * Add the lines numbers to the display using the `-N` option.
   * Navigate the file using the space bar and arrows.
   * Search for the pattern `isoform` using the command `/<search term>`, then
     navigate through the matches with the keys `n` and `N`.
   * Close the file with `q`.

<br>

**Additional Tasks:**
* Display only the line 101 of the file by using a combination of `head` and
  `tail`. For this you will need to use the the `|` (pipe) operator, that
  allows to redirect the output of one command into another command.


<br>
<br>


## Exercise 6 - Merge data in columns
**Context:** in this exercise, we will be working with three files containing
replicates from a micro-array experiment. These files are the following:
* `/play/micro-array/arrayDat-1.csv`
  Input files:  to arrayDat-3.csv

**Our objective** is to merge these three files into a single tab-delimited
file with 4 columns: `ProbeID` (gene name), `Sample1`, `Sample2` and `Sample3`
(the gene expression levels recorded in each replicate of the experiment).

### Step 1: data exploration
Have a look at the 3 input files using `less` or `head`, to get familiar with
their structure and content.

### Step 2: conversion to tab-delimited
The original files contain tabulated data separated by the `;` (semi-column)
character.
* Convert the delimiters from `;` to `\t` (tab).
* Save the converted content into a new file with a `.tsv` extension. E.g. the
  converted version of `arrayDat-1.csv` should be named `arrayDat-1.tsv`.

### Step 3: sort the files
Before we can merge the content of the 3 `arrayDat-*.tsv` files, we have to
make sure that the order of rows in each file (i.e. the order of genes) are the
same. If you look at the files, you will see that this is not the case.
Therefore the files need to be sorted by their 1st column (`ProbeID`).

* Sort each `arrayDat-*.tsv` by its `ProbeID` column using the **`sort`**
  command.
* Make sure that the **header line** of the file remain at the top after the
  sorting operation.  
  **Hint:** the header line is the only one that starts with a letter, so we
  can maybe take advantage of *numerical sorting* that sorts letters before
  numbers. You can have a look at `man sort` to find the right option.
* Save the sorted output to files named `arrayDat-sorted-*.tsv`.

### Step 4: verify the file sorting
In this step, we will simply double-check that the sorted files we created
at the previous step (`arrayDat-sorted-*.tsv`) have the same number of lines
and that the genes on those lines are in the same order.

To verify this, the idea is to extract the first column (the gene names) from
the sorted files, and compare it across the 3 sorted files.

Proceed as follows:
* Use the **`cut`** command to extract the first column (`ProbeID`) of each
  `arrayDat-sorted-*.tsv` file. Save the output to temporary files named
  `tmp_1.tsv`, `tmp_2.tsv`, and `tmp_3.tsv` (these files should contain a
  single column).
* Using the **`diff`** command, compare the files `tmp_1.tsv` and `tmp_2.tsv`,
  as well as `tmp_1.tsv` and `tmp_3.tsv`.
* If all `tmp_*.tsv` files are the same (and they should), you can now delete
  these files. Their only purpose was to allow us to check that all files
  have their lines sorted in the same order.

### Step 5: Merge the sorted files
In this final step, we concatenate the content of the `sorted_*.tsv` files to
produce a final file (`final.tsv`) with 4 columns: `ProbeID`, `Sample1`,
`Sample2`, `Sample3`.

* Use **`paste`** to concatenate the content of the `sorted_*.tsv` files.
* Use **`cut`** to remove the duplicated `ProbeID` columns.
* These two steps can be performed in a single command line by using a pipe
  (`|`) to pass the output of `paste` to `cut`.

Your final output file should look like this:
[Insert image here]

<br>

**Additional Tasks:**
Try to re-write the entire process as a single command. For this you will
need the additional
* **Pipe operator**, to redirect the input of one command into the next.
* **Process substitution** `<( command )`, to treat the output of a command
  (or a series of commands) as a virtual file from which data is read.


<br>
<br>


## Exercise 7 - using `grep` to retrieve information from files

In this exercise, we will be using
[FASTA files](https://en.wikipedia.org/wiki/FASTA_format). FASTA is a
text-based format to represent nucleotide or protein sequences.
* FASTA files can contain one or more sequences.
* Each new sequence starts with a **sequence header** line, which starts with
  the character **`>`**. A sequence header is always on a single line.
* Each sequence header is followed by one or more lines that contain the
  nucleotide or amino acid sequence of the sequence.

Here is an example of a FASTA file:
```
>sp|P18823|ACCD_PEA Carboxyl transferase OS=Pisum sativum GN=accD PE=1 SV=3
MINEDPSSLTDMDNNIDSWKNNSENSSYSHADSLADVSNIDNLLSDKIFSIRDSNSNIYD
IYYAYDTNDTNITKYKWTNNINRCIESYLRSQICEDIDFNSDICDKVQRTIIILIRSTND
NDISDTNDISDTNDTNDTNAIYDPFDISDTNDTN
>sp|P09339|ACON_BACSU Aconitate hydratase OS=Bacillus subtilis GN=citB PE=1 SV=4
MANEQKTAAKDVFQARKTFTTNGKTYHYYSLKALEDSGIGKVSKLPYSIKVLLESVLRQV
DGFVIKKEHVENLAKWGTAELKDIDVPFKPSRVILQDFTGVPAVVDL
```

### Part A - basic `grep` usage
Have a look at file content of the file `play/grep/uniprot-thioredoxin.fas`
(e.g. using the `less` command). Then answer the following questions using the
**`grep`** command:
* How many sequences are there in the file? **Hint:** count the number of
  header lines. In the
* How many entries are from `Staphylococcus`?
* Display header lines that are *not* from `Staphylococcus`?

<br>

### Part B - extract the top 10 most-frequent genus
`/exercises/ex3-retrieval/thioredoxin.fas` is a FASTA file containing > 3000
sequences. Your task is to display the 10 most frequent genus in the sequences
of this file, and their frequency.

Here is a suggested way to perform this task:
1. Isolate the header lines.
2. Isolate the genus name from each line. To do this, you can take advantage
   of the *controlled vocabulary* in the file: the organisms name is always
   prefixed with `OS=`.
3. Sort the genus names, compute their frequency and keep only a single
   instance of each genus name.
4. Sort the genus by frequency and keep only the 10 most frequent.

**Hints:**
* The steps above are best done as part of a pipeline: use the `|` (pipe)
  operator to pipe the output of one command to the next.
* When building the pipeline and doing tests, you can end your pipeline with
  `| head` so that you avoid printing the whole file each time.
