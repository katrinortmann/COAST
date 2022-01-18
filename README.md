# COAST (Conceptual Orality Analysis and Scoring Tool)

Natural human language is used in two primary forms: written and spoken. Both forms place very different demands on the language user, thus leading to very different utterances. However, a high amount of variation also exists *within* written and spoken language (cf. Koch & Oesterreicher, 2007; Halliday, 1989; Biber & Conrad, 2009). To account for this variation, Koch & Oesterreicher (1985) proposed to distinguish between *medial and conceptual orality and literacy*. That is, independently of their medial realization, language can show characteristics that are typical of the written or spoken mode, i.e. be conceptually oral/literal.

Koch & Oesterreicher (1985, 2007) list a number of universal characteristics that allow to judge the degree of orality, although in a rather vague and abstract way. Ágel & Hennig (2006) extended the approach of Koch & Oesterreicher and created a framework for objectively measuring the conceptual orality of a given text based on linguistic features. However, their method requires the manual inspection of every individual text and cannot be applied sensibly to a large amount of data.

In Ortmann & Dipper (2019) and Ortmann & Dipper (2020) we developed a set of simple linguistic features that can be determined automatically in texts of any length and indicate the degree of orality in modern and historical (German) texts. In Ortmann & Dipper (forthcoming), we combined our results to develop an automatic, objective score of orality that correlates with expert judgement.

COAST is a Python tool that automatically analyzes our developed features in a given set of texts and outputs the feature statistics and calculates an orality score for each text. The list of features and their weights for the final score can be customized depending on the application.

## Requirements

- [Python 3](https://www.python.org/)
- [click package](https://pypi.org/project/click/)([Documentation](https://click.palletsprojects.com/))

## Usage


### Input Format

### Available Processors

### Available Features

### Weights

### Reproduce Results

## References

Ágel & Hennig (2006)

Biber & Conrad (2009)

Halliday (1989)

Koch & Oesterreicher (1985)

Koch & Oesterreicher (2007)

Ortmann & Dipper (2019)

Ortmann & Dipper (2020)

Ortmann & Dipper (forthcoming)

Anne Schiller, Simone Teufel, Christine Stöckert, and Christine Thielen. 1999. *Guidelines für das Tagging deutscher Textcorpora mit STTS (Kleines und großes Tagset)*. [PDF](http://www.sfs.uni-tuebingen.de/resources/stts-1999.pdf).
