# LocText

The end goal is to build a text mining pipeline to find and extract from biomedical papers (i.e. [PubMed](http://www.ncbi.nlm.nih.gov/pubmed)) the subcellular localization of proteins.

Project start: end of 2013
Project end: ...working...

## People involved

_rostlab_ group:

* Juan Miguel Cejuela (PhD student, expertise on text mining)
* Tanya Goldberg (PhD student, expertise on localization and biology)
* Kujtim Rrahmani (Mater student, doing with us his IDP and thesis)
* Shruthi Sakthi (Master student, doing with us a Guided Research Lab)
* Shrikant Vinchurkar (Master student, doing with us a student job)

_Group of Lars_:

* Lars Juhl Jensen (Professor, expertise on text mining and bioinformatics)


## Introduction

For the pipeline, three main text mining analyzers come in place:

1. the recognition (& normalization) of protein mentions in text,
2. the recognition (& normalization) of localization mentions in text, and
3. the correct identification of the relationship, `protein` --> `subcellular localization(s)`.

We start from the basis of available systems to do 1 & 2. However, we do not discard improving these two systems if necessary.

## Undertakings

### 1. Write Java interface to Lars' method

...TODO

### 2. Compare Juanmi's gene tagger vs Lars's

Juanmi's gene tagger method 'TagTog' was evaluated on Biocreative corpus test data and following are the results of evaluation:

Precision: 0.8580
Recall: 0.8215
FScore: 0.8394

### 3. Motivation for undertaking

...TODO

Student: Shrikant Vinchurkar
1. Calculate the number of proteins for all organisms in SwissProt (ver Feb 2014) that are annotated experimentally and non-experimentally.
2. Summary for Eukaryotes, Bacteria and Archaea can be found in metadata/SummaryAnnotation.xlsx

### 4. Annotate a corpus for relationship extraction

We want to annotate some corpus, possibly mostly abstracts to obtain a higher diversity of information, and around 600-800 abstracts or the equivalent in full-text articles. Annotating:

* Protein names, normalized to: `UniProt` & `STRING`
* Localization mentions, normalized to: `GO` terms

#### Collecting the papers

We will focus on papers treating the organisms: `{human, yeast, arabidopsis, drosophilace, c.elegans, s.pombe, s.cerevis}`. For instance, `rat` and `mouse` were discarded by suggestion of Lars, since mammals typically have very similar gene names and similar localizations.

##### Method followed for collection of papers:
spv: We choose the sprot data files from /mnt/project/rost_db/data/trembl/taxonomic_divisions/uniprot_sprot_*.dat and scanned every protein entry in these files to generate statistics for Eukaryota, Bacteria and Archaea. For each taxonomy class, following statistics were generated:

1. Summary of all proteins whose subcellular localization is mentioned, along with supplementary information such as AC, Protein ID,  Organism, no of experimental localization, no of non-experimental localization and localization itself.
2. Mapping of proteins with experimental localization to the PubMed Id's where the localization is actually mentioned.
3. Summary of taxonomy class listing collective statistics for each organism (no of proteins with only experimental localization, no of proteins with only non experimental localization, no of proteins with exp as well as non-exp localizations, no of proteins having no localizations, total no of proteins in sprot)

We scanned the summary of taxonomic class to choose organisms with most localization entries. For those organisms, the papers were collected from PubMed with the help of proteinID to PubMed Id mapping that we had. The summary of taxonomic classes Eukaryota, Bacteria and Archaea is uploaded in folder metadata/SummaryAnnotation.xlsx.

* **How to sample papers**: read off from UniProt support papers for localization annotations and from these investigate with a few ~20 papers

* **what is the percentage of papers that contain in the _abstract_ support information for the localization?**. 
spv: We started scanning the abstracts for Eukaryota and scanned 45 abstracts (15 each from Human, Yeast and Arabidopsis). Details about scanning abstracts are mentioned in next section. Since the papers were collected with the help of PubMed Id summary that we had, we could find localization information in 37 out of 45 abstracts (i.e. ~ 82 %). Although we could find out localization keywords in large number of abstracts, not all such abstracts were useful to derive rules.

If it's a high amount, like ~90%, simply randomly sample from UniProt documents. Otherwise use Lars' pipeline to recognize protein and localization mentions to select abstracts that at least contain one mention for each category. -- Extra filter out High-throughput localization publications (assumption, the annotations are gonna appear in the full text).

#### Scanning the abstracts
sv:
1. 45 abstracts were randomly chosen (15 each from Human, Yeast and Arabidopsis)
2. The rules derived from reading 45 abstracts can be found in folder metadata (Rules_Human.txt, Rules_Scerevisae.ods , Rules_Athaliana.ods)
3. Legend used for manual marking of keywords in abstracts: Yellow-Subcellular location, Green-Protein/Gene Id, Pink-Verbs
4. Estimated time to read and mark 15 abstracts - 6 hours


## Resources

Some links & resources of interest:

* [Biocreative 2 GM corpus](http://www.biocreative.org/resources/corpora/biocreative-ii-corpus/)
* [Lars' COMPONENTS](http://compartments.jensenlab.org/Downloads)
* [CRAFT corpus](http://bionlp-corpora.sourceforge.net/CRAFT/)
