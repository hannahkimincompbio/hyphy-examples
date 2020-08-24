# Computing Gene Stoichiometry content and outputting a summary table

Given a **nucleotide** sequence alignment, the goal is to count atoms and report.

1. The counts of nucleotides within a sequence that are 'A', 'T', C', 'G', corresponding to the canonical nuclotides.
2. The total number of Carbon, Hydrogen, Oxygen, and Nitrogen atoms per sequence, computed with information from the known chemical structures

There are several HyPhy scripts in this directory, arranged from the simplest to the most advanced in numerical order, so that `GS-01.md` (`.md` is used so that GitHub renders the annotated source files) is the simplest, `GS-02.md` will be the second simplest, etc. The scripts include inline comments that you could use to follow the logic. You can also open them in a markdown editor to view formatted text.

There is a test dataset, `ncov.fas` which contains a few partial sequences from SARS-CoV-2. They are **not** aligned.

To run an example, execute

```
hyphy GS-01.md
```

or (for the scripts that expect positional arguments)

```
hyphy GS-0X.md arg1 arg2 ... argN
```
or (for the scripts that expect keyword arguments)

```
hyphy GS-0X.md --key1 arg1 --key2 arg2 ...
```
