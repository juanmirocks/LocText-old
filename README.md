# LocText

The end goal is to build a text mining pipeline to find and extract from biomedical papers (i.e. [PubMed](http://www.ncbi.nlm.nih.gov/pubmed)) the subcellular localization of proteins.

Project start: end of 2013
Project end: ...working...

## People involved

_rostlab_ group:

* Juan Miguel Cejuela (PhD student, expertise on text mining)
* Tanya Goldberg (PhD student, expertise on localization and biology)
* Shruthi Sakthi (Master student)
* Shrikant Vinchurkar (Master student)

_Group of Lars_:

* Lars Juhl Jensen (Professor, expertise on text mining and bioinformatics)


## Introduction

For the pipeline, three main text mining analyzers come in place:

1. the recognition (& normalization) of protein mentions in text,
2. the recognition (& normalization) of localization mentions in text, and
3. the correct identification of the relationship, `protein` --> `subcellular localization(s)`.

We start from the basis of available systems to do 1 & 2. However, we do not discard improving these two systems if necessary.
