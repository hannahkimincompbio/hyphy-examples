# Computing GC content and CpG deficiency

Given a **nucleotide** sequence alignment, the goal is to compute and report.

1. The fraction of nucleotides that are `C` or `G` (GC) content, `f(C) + f(G)`, where `f(X)` denotes the frequency of `X` in the alignment.
2. The relative abundance of `CpG`, which simply `f(CG)/ [f(C)f(G)`

There are several HyPhy scripts in this directory, arranged from the simplest to the most advanced in numerical order, so that `CG-01.md` (`.md` is used so that GitHub renders the annotated source files) is the simplest, `CG-02.md` is the second simplest, etc. The scripts include inline comments that you could use to follow the logic. You can also open them in a markdown editor to view formatted text.

There is a test dataset, `ncov.fas` which contains a few partial sequences from SARS-CoV-2. They are **not** aligned.

To run an example, execute

```
hyphy CG-01.md
```

or (for the scripts that expect positional arguments)

```
hyphy CG-0X.hbl arg1 arg2 ... argN
```
or (for the scripts that expect keyword arguments)

```
hyphy CG-0X.hbl --key1 arg1 --key2 arg2 ...
```
