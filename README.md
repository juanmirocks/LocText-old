# LocText

The goal is to build a text mining pipeline to extract the subcellular localization of proteins from biomedical papers.

Project start: end of 2013
Project end: ...working...

## People involved

_rostlab_ group:

* Juan Miguel Cejuela (PhD student, expertise on text mining)
* Tanya Goldberg (PhD student, expertise on localization and biology)
* Shrikant Vinchurkar (Master student, doing with us a student job)
* Kujtim Rrahmani (Mater student, doing with us his IDP and thesis)

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

...TODO @Shruthi

### 2. Compare Juanmi's gene tagger vs Lars's

Juanmi's gene tagger was evaluated on Biocreative corpus test data and following are the results of evaluation:

* P: 0.8580 (precision)
* R: 0.8215 (recall)
* F: 0.8394 (F-score)

Lars's gene tagger was evaluated as well but obtained poor results. We believe the poor results are due the fact that Lars's method used a dictionary with only human gene names included. Therefore, we could not obtain a fair evaluation of Lars' and consequently **Juanmi's vs Lars' could not be compared**.

### 3. Annotate a corpus for relationship extraction

We want to annotate some corpus, possibly mostly abstracts to obtain a higher diversity of information, and around 600-800 abstracts or the equivalent in full-text articles. Annotating:

* Protein names, normalized to: `UniProt` & `STRING`
* Localization mentions, normalized to: `GO` terms

### Collecting the papers

We will focus on papers treating the organisms: `{human, arabidopsis, drosophilace, c.elegans, s.pombe, s.cerevis}`. For instance, `rat` and `mouse` were discarded by suggestion of Lars, since mammals typically have very similar gene names and similar localizations.

#### Method followed for collection of papers:

@Shrikant: In the `sprot` data files from `/mnt/project/rost_db/data/trembl/taxonomic_divisions/uniprot_sprot_*.dat`, we scanned every protein entry in these files to generate statistics for Eukaryota, Bacteria and Archaea. For each taxonomy class, following statistics were generated:

1. Summary of all proteins whose subcellular localization is mentioned, along with supplementary information such as: AC, Protein ID, Organism, # of experimental localization, # of non-experimental localization and localization itself.
2. Mapping of proteins with experimental localization to the PubMed Id's where the localization is actually mentioned.
3. Summary of taxonomy class listing collective statistics for each organism (# of proteins with only experimental localization, # of proteins with only non experimental localization, # of proteins with exp as well as non-exp localizations, # of proteins having no localizations, total # of proteins in sprot)

We scanned the summary of taxonomic class to choose organisms with most localization entries. For these organisms, we collected PubMed papers using the mapping proteinID --> PubMed Id (PMID) that was present in the `sprot` files. The summary results of taxonomic classes {Eukaryota, Bacteria, and Archaea}  at the level of organisms are in: [metadata/Summary/SummaryAnnotation.xlsx](https://rostlab.org/gitlab/juanmi/loctext/blob/master/metadata/Summary/SummaryAnnotation.xlsx). The files containing mapping protein --> PubMedID (PMID) as well as summary results at the level of proteins are in [metadata/Summary](https://rostlab.org/gitlab/juanmi/loctext/tree/master/metadata/Summary).

* **What is the % of papers that contain within the _abstract_ support information for the localization?**.

@Shrikant: We started processing abstracts for Eukaryota and scanned 45 abstracts (15 each for the organisms Human, Yeast and Arabidopsis). Details about scanning abstracts are mentioned in next section. Since the papers were collected with the help of PubMed Id summary that we had, we could find localization information in 37 out of 45 abstracts (i.e. ~ 82 %). Although we could find out localization keywords in large number of abstracts, not all such abstracts were useful to derive rules.

#### Scanning the abstracts

@Shrikant:

1. 45 abstracts were randomly chosen (15 each from Human, Yeast and Arabidopsis)
2. The rules derived from reading 45 abstracts can be found in folder `metadata` (`Rules_Human.txt`, `Rules_Scerevisae.ods` , `Rules_Athaliana.ods`)
3. Legend used for manual marking of keywords in abstracts: `Yellow:Subcellular` location, `Green:Protein/Gene Id`, `Pink:Verbs`.
4. Estimated time to read and mark 15 abstracts - 6 hours

**Results**: some statistics about the annotations can be found here: [metadata/Summary](https://rostlab.org/gitlab/juanmi/loctext/tree/master/metadata/Summary)


## Resources

Some links & resources of interest:

* [Biocreative 2 GM corpus](http://www.biocreative.org/resources/corpora/biocreative-ii-corpus/)
* [Lars' COMPONENTS](http://compartments.jensenlab.org/Downloads)
* [CRAFT corpus](http://bionlp-corpora.sourceforge.net/CRAFT/)

## Other

### Draft Roadmap

* Feb: extra time for unfinished tasks
* Jan: writing the thesis
* Dec: method development
* Nov: method development
* Oct: method development
* Sept: playing with ML
* Aug: statistics 1 & 2. Also, we get GO ids for localizations and UniProt and .. for proteins. Finally, we need to set the rules for our ML method here. From here on we will also annotate one full text article every week.
* July: 100 abstracts

### Ongoing Discussions & Meetings

#### Meeting on 17.07.14

* 100 abstracts supposed to take not more than 60 hours of work (2 weeks)
** first Shrikant annotates the abstracts and sends Tanya daily th eids of the abstracts to checks
** after Tanya is done with checking of these abstracts, she sends the ids to Juanmi
** Juanmi annotates these abstracts from scratch (Juanmi will be slower than us. Therefore, we expect him to finishe ~20 abstracts by the time we have 100). 
* once we have those we compare ourselves (Shrikant & Tanya) with the annotations of Juanmi. We would expect an overlap in annotations of at least 80%. This would be our statistics 1
* afterwards we'll compare our consensus annotations (the three of us) with the annotations of UniProt. This would be our statistics 2