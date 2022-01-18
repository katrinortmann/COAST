# COAST (Conceptual Orality Analysis and Scoring Tool)

Human language is used in two primary forms: written and spoken. Both forms place very different demands on the language user, thus leading to very different utterances. However, a high amount of variation also exists *within* written and spoken language (cf. Koch & Oesterreicher 2007, Halliday 1989, Biber & Conrad 2009). To account for this variation, Koch & Oesterreicher (1985) proposed to distinguish between *medial and conceptual orality and literacy*. That is, independently of their medial realization, language can show characteristics that are typical of the written or spoken mode, i.e. be conceptually oral/literal.

Koch & Oesterreicher (1985, 2007) list a number of universal characteristics that allow to judge the degree of orality, although in a rather vague and abstract way. Ágel & Hennig (2006) extended the approach of Koch & Oesterreicher and created a framework for objectively measuring the conceptual orality of a given text based on linguistic features. However, their method requires the manual inspection of every individual text and cannot be applied sensibly to a large amount of data.

In [Ortmann & Dipper (2019)](https://www.aclweb.org/anthology/W19-1407/) and [Ortmann & Dipper (2020)](https://www.aclweb.org/anthology/2020.lrec-1.162), we developed a set of simple linguistic features that can be determined automatically in texts of any length and indicate the degree of orality in modern and historical (German) texts. In Ortmann & Dipper (forthcoming), we combined our results to develop an automatic, objective score of orality that correlates with expert judgement.

COAST is a Python tool that automatically analyzes our developed features in a given set of texts, outputs the feature statistics and calculates an orality score for each text. The list of [features](#available-features) and their [weights](#weights) for the final score can be customized depending on the application.

## Requirements

- [Python 3](https://www.python.org/)
- [click package](https://pypi.org/project/click/) ([Documentation](https://click.palletsprojects.com/))

## Usage

### Input Format

### Available Processors

### Available Features

### Weights

### Reproduce Results

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
