# LocText

The end goal is to build a text mining pipeline to find and extract from biomedical papers (i.e. [PubMed](http://www.ncbi.nlm.nih.gov/pubmed)) the subcellular localization of proteins.

Project start: end of 2013
Project end: ...working...

## People involved

_rostlab_ group:

* Juan Miguel Cejuela (PhD student, expertise on text mining)
* Tanya Goldberg (PhD student, expertise on localization and biology)
* Kujtim Rrahmani (Mater student, doing with us his IDP and thesis)
* Shruthi Sakthi (Master student, doing with us a student job)
* Shrikant Vinchurkar (Master student, doing with us Guided Research Lab)

_Group of Lars_:

* Lars Juhl Jensen (Professor, expertise on text mining and bioinformatics)


## Introduction

For the pipeline, three main text mining analyzers come in place:

1. the recognition (& normalization) of protein mentions in text,
2. the recognition (& normalization) of localization mentions in text, and
3. the correct identification of the relationship, `protein` --> `subcellular localization(s)`.

We start from the basis of available systems to do 1 & 2. However, we do not discard improving these two systems if necessary.

## Undertakings

### Compare Juanmi's gene tagger vs Lars's tagger

...TODO tell story

### Annotate a corpus for relationship extraction

We want to annotate some corpus, possibly mostly abstracts to obtain a higher diversity of information, and around 600-800 abstracts or the equivalent in full-text articles. Annotating:

* Protein names, normalized to: `UniProt` & `STRING`
* Localization mentions, normalized to: `GO` terms

#### Collecting the papers

We will focus on papers treating the organisms: `{human, yeast, arabidopsis, drosophilace, c.elegans, s.pombe, s.cerevis}`. For instance, `rat` and `mouse` were discarded by suggestion of Lars, since mammals typically have very similar gene names and similar localizations.

* **How to sample papers**: read off from UniProt support papers for localization annotations and from these investigate with a few ~20 papers, **what is the percentage of papers that contain in the _abstract_ support information for the localization?**. If it's a high amount, like ~90%, simply randomly sample from UniProt documents. Otherwise use Lars' pipeline to recognize protein and localization mentions to select abstracts that at least contain one mention for each category. -- Extra filter out High-throughput localization publications (assumption, the annotations are gonna appear in the full text).


## Resources

Some links & resources of interest:

* [Biocreative 2 GM corpus](http://www.biocreative.org/resources/corpora/biocreative-ii-corpus/)
* [Lars' COMPONENTS](http://compartments.jensenlab.org/Downloads)
* [CRAFT corpus](http://bionlp-corpora.sourceforge.net/CRAFT/)
