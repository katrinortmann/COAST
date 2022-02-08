# COAST (Conceptual Orality Analysis and Scoring Tool)

Human language is used in two primary forms: written and spoken. Both forms place very different demands on the language user, thus leading to very different utterances. However, a high amount of variation also exists *within* written and spoken language (cf. Koch & Oesterreicher 2007, Halliday 1989, Biber & Conrad 2009). To account for this variation, Koch & Oesterreicher (1985) proposed to distinguish between *medial and conceptual orality and literacy*. That is, independently of their medial realization, language can show characteristics that are typical of the written or spoken mode, i.e., be conceptually oral/literal.

Koch & Oesterreicher (1985, 2007) list a number of universal characteristics that allow to judge the degree of orality, although in a rather vague and abstract way. Ágel & Hennig (2006) extended the approach of Koch & Oesterreicher and created a framework for objectively measuring the conceptual orality of a given text based on linguistic features. However, their method requires the manual inspection of every individual text and cannot be applied sensibly to a large amount of data.

In [Ortmann & Dipper (2019)](https://www.aclweb.org/anthology/W19-1407/) and [Ortmann & Dipper (2020)](https://www.aclweb.org/anthology/2020.lrec-1.162), we developed a set of simple linguistic features that can be determined automatically in texts of any length and indicate the degree of orality in modern and historical (German) texts. In Ortmann & Dipper (forthcoming), we combined our results to develop an automatic, objective score of orality that correlates with expert judgement.

COAST is a Python tool that automatically analyzes our developed features in a given set of texts, outputs the feature statistics and calculates an orality score for each text. The list of [features](#available-features) and their [weights](#weights) for the final score can be customized depending on the application.

## Requirements

- [Python 3](https://www.python.org/)
- [click package](https://pypi.org/project/click/) ([Documentation](https://click.palletsprojects.com/))

## Usage

From the command line, call COAST with

> py COAST.py analyze -i input_format -p "['processor_name', 'processor_name']" -f feature_file -w weight_file --reproduce-kajuk True input_dir_or_file output_dir

- `input_dir_or_file`: can be a single file or a folder
- `output_dir`: folder to save the results
- `input_format`: the following input formats are currently supported: `conlluplus`, `conllu`. For more input formats and documentation, see [below](#input-format).
- `processor_name`: processors are called in the given order; the following processors are currently supported: `ellipsisremover`, `bracketremover`, `pronounlemmatizer`. For more processors and documentation, see [below](#available-processors).
- `feature_file`: file containing the list of features to analyze (for more info and available features, see [below](#available-features))
- `weight_file`: file containing weights to calculate the orality score (for more info, see [below](#weights))
- `reproduce-kajuk`: default False; overwrites settings to reproduce the results of Ortmann & Dipper (forthcoming) (cf. [below](#reproduce-results))

The first three parameters (`input_dir_or_file`, `output_dir` and `input_format`) are required. The remaining parameters are optional.

### Input Format

The COAST tool provides importers for the [CoNLL-U](https://universaldependencies.org/format.html) and [CoNLL-U Plus](https://universaldependencies.org/ext-format.html) format. Both formats consist of tab-separated columns, which contain the annotated text. For `CoNLL-U` the columns are pre-defined:

```
ID (word index), FORM (word form), LEMMA (Lemma), UPOS (universal POS-tag), XPOS (language specific POS-tag), FEATS (Morphological features), HEAD (head), DEPREL (dependency relation to the head), DEPS (dependency graph), MISC (other annotation)
```

Files in the `CoNLL-U Plus` format can contain any desired columns. The order of columns is specified in the first line, e.g.,

```
# global.columns = ID FORM LEMMA UPOS XPOS FEATS HEAD DEPREL DEPS MISC line norm page type
```

Columns may be empty, except for the FORM column and also the XPOS column, which is required for most of the orality features.

To analyze texts in other formats with COAST, first convert them to one of the two formats. For conversion, you may consider using [C6C](https://github.com/rubcompling/C6C), a converter for a variety of different input and output formats.

### Available Processors

In order to analyze data with COAST, some additional pre-processing may be necessary. The tool comes with three processors that we used to pre-process the KaJuK corpus (Ágel & Hennig 2008) for our analysis in Ortmann & Dipper (forthcoming). For further processors, you may have a look at the [C6C pipeline](https://github.com/rubcompling/C6C).

When specifying processors in the command line, remember to list them in order of application. Also, COAST expects a Python list, so obey the format as stated [above](#usage) with double quotes surrounding the list and single quotes surrounding the processor names.

The available processor names are:

| Processor           |  Description                                    |
|---------------------|-------------------------------------------------|
| `ellipsisremover`   |  Removes ellipses from the input data to reflect the actual word count. Ellipsis is identified by the letter `E` in the `type` column. |
| `bracketremover`    |  Removes brackets from the word form (column `FORM`) to reflect the actual word length. In historical corpora, different types of brackets are often used to signal meta-linguistic attributes like initials, majuscules, hard-to-read or crossed-out words, etc. |
| `pronounlemmatizer` |  For personal pronouns (`XPOS` is `PPER`) and demonstratives (`XPOS` is `PDS`), the processor maps a range of word forms to a standardized lemma `ich/wir` and `dies(e)/die/der` that is used for the features `PRON1st` and `DEMshort`. This is only necessary if the input data is not lemmatized. |


### Available Features

The feature parameter can be used to specify, which features should be included in the analysis. The feature file should contain one feature name per line. An example can be found in the `/config` folder. If no feature file is given, all supported features are analyzed.

Currently, COAST supports the following features:

| Feature     | Description                               |
|-------------|-------------------------------------------|
| `mean_sent` | Mean sentence length                      |
| `med_sent`  | Median sentence length                      |
| `mean_word` | Mean word length                      |
| `med_word`  | Median word length                      |
| `subord`    | Ratio of subordinating conjunctions (`XPOS` is `KOUS` or `KOUI`) to full verbs (`XPOS` begins with `VV`)                      |
| `coordInit` | Proportion of sentences beginning with a coordinating conjunction (`XPOS` is `KON`)                      |
| `question`  | Proportion of interrogative sentences, based on the last punctuation mark of the sentence                      |
| `exclam`    | Proportion of exclamative sentences, based on the last punctuation mark of the sentence                      |
| `V:N`       | Ratio of full verbs (`XPOS` begins with `VV`) to nouns (`XPOS` is `NN`)                      |
| `lexDens`   | Ratio of lexical items (`XPOS` is `ADJ.*`, `ADV`, `N.*` or `VV.*`) to all words                      |
| `PRON1st`   | Ratio of 1st person pronouns with lemmas (column `LEMMA`) `ich` *‘I’* and `wir` *‘we’* to all words                      |
| `DEM`       | Ratio of demonstrative pronouns (`XPOS` is `PDS`) to all words                      |
| `DEMshort`  | Proportion of demonstrative pronouns (`XPOS` is `PDS`) with lemmas (column `LEMMA`) `diese` or `die` *‘this/these’* that are realized as the short form (`LEMMA` is `die`) |
| `PTC`       | Proportion of answer particles (`XPOS` is `PTKANT`) to all words; includes `ja` *‘yes’*, `gewiss` *‘certainly’*, `nein` *‘no’*, `bitte` *‘please’*, `danke` *‘thanks’* | 
| `INTERJ`    | Proportion of primary, i.e. one-word interjections (`XPOS` is `ITJ`) to all words; includes `ach, oh, o, bravo, halleluja, hmm, ...`                      |

POS tags are from the STTS tagset (Schiller et al. 1999). Words tagged as punctuation (`XPOS` is one of `$.`, `$,` or `$(`) are ignored except for sentence-type features `question` and `exclam`.

### Weights

The weight parameter can be used to calculate a custom orality score. The weight file should contain key-value pairs, separated by a colon, e.g.,

```
mean_word : -0.819 
PRON1st : 0.717 
V:N : 0.528
```

Positive values correspond to indicators of orality, negative values to indicators of literal language. The score is calculated by multiplying the [standardized](#standardization) value of each feature with the weight of that feature. Then, the total sum of those products is returned.

An example file is located in the `config` folder. If no weight file is specified, the default weights from Ortmann & Dipper (forthcoming) are used:

```
mean_word : -0.819 
PRON1st : 0.717 
V:N : 0.528
DEMshort : 0.365
subord : -0.314 
INTERJ : 0.276 
DEM : 0.06 
PTC : 0.104 
lexDens : -0
```

### Standardization

In order to compare values of different features like average word length (e.g., 5 letters) and the proportion of interjections (e.g., 0.1%), a linear transformation is applied before the calculation of the orality score. For each feature, the values are mapped to the standardized area between 0 and 1. As no sensible minimum and maximum value can be determined for most features, the lowest value (for a given feature) in the input data is mapped to 0 and the highest value to 1.

COAST will output one file with the original values for each feature and one file with the standardized values that also includes the orality score.

### Reproduce Results

The `reproduce-kajuk` parameter is inteded to reproduce the results from Ortmann & Dipper (forthcoming), based on the [data set](#kajuk-data-set) provided in the `/data` folder of this repository. Setting this parameter to `True` will automatically apply the options we used in our study, i.e.,

- `processors` are set to `ellipsisremover`, `bracketremover`, `pronounlemmatizer`
- `features` are set to `mean_sent, med_sent, mean_word, med_word, subord, coordInit, question, exclam, V:N, lexDens, PRON1st, DEM, DEMshort, PTC, INTERJ`
- `weights` are set to the default weights given [above](#weights)

This option also adds additional information to the output files, including the expert scores from the corpus and the categorization as oral or literal.

#### KaJuK data set

The `data` folder of this repository contains the KaJuK corpus (Ágel & Hennig 2008, licensed under [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/)), which we converted from a custom XML format to the CoNLL-U Plus format with the [C6C pipeline](https://github.com/rubcompling/C6C). The texts are split into 5 or 6 parts of about 2,000 words to enable cross-validation. For the feature analysis, we added POS tags according to the STTS tagset (Schiller et al. 1999), which are provided in the `XPOS` column. The tags are based on the annotation of different automatic taggers whose individual tags are given in the columns `someweta_web`, `spacy_dep_news`, `spacy_news_md`, `stanza_gsd` and `stanza_hdt`. The estimated overall tagging accuracy is about 88%. For more details on the tagging process, see Ortmann & Dipper (forthcoming). 

## License

The scripts in this repository are provided under the MIT license. The KaJuK corpus in the `/data` folder is licensed under [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/).

## References

Vilmos Ágel and Mathilde Hennig (Editors). 2006. *Grammatik aus Nähe und Distanz: Theorie und Praxis am Beispiel von Nähetexten 1650-2000*. Tübingen: Niemeyer.

Vilmos Ágel and Mathilde Hennig. 2008. *Kasseler Junktionskorpus.* Justus-Liebig-Universität Gießen. https://doi.org/10.34644/laudatio-dev-nCQsCnMB7CArCQ9CDmun. Accessed on July 12th 2021.

Douglas Biber and Susan Conrad. 2009. *Register, Genre, and Style*. Cambridge University Press.

Michael A. K. Halliday. 1989. *Spoken and written language*. Oxford University Press.

Peter Koch and Wulf Oesterreicher. 1985. Sprache der Nähe — Sprache der Distanz: Mündlichkeit und Schriftlichkeit im Spannungsfeld von Sprachtheorie und Sprachgeschichte. *Romanistisches Jahrbuch*, 36: 15–43.

Peter Koch and Wulf Oesterreicher. 2007. Schriftlichkeit und kommunikative Distanz. *Zeitschrift für germanistische Linguistik*, 35: 246–275.

Katrin Ortmann and Stefanie Dipper. 2019. Variation between Different Discourse Types: Literate vs. Oral. In *Proceedings of the NAACL-Workshop on NLP for Similar Languages, Varieties and Dialects (VarDial)*, pp. 64-79. Minneapolis, MN. [PDF](https://www.aclweb.org/anthology/W19-1407/)

Katrin Ortmann and Stefanie Dipper. 2020. Automatic Orality Identification in Historical Texts. In *Proceedings of The 12th Language Resources and Evaluation Conference (LREC)*, Marseille, France, pp. 1293-1302. [PDF](https://www.aclweb.org/anthology/2020.lrec-1.162)

Katrin Ortmann and Stefanie Dipper. Forthcoming. *Nähetexte automatisch erkennen: Entwicklung eines linguistischen Scores für konzeptionelle Mündlichkeit in historischen Texten.*

Anne Schiller, Simone Teufel, Christine Stöckert, and Christine Thielen. 1999. *Guidelines für das Tagging deutscher Textcorpora mit STTS (Kleines und großes Tagset)*. [PDF](http://www.sfs.uni-tuebingen.de/resources/stts-1999.pdf).
