# On the Robustness of Random Forest Against Data Poisoning: An Ensemble-Based Approach

[Marco Anisetti](https://homes.di.unimi.it/anisetti), [Claudio A. Ardagna](https://homes.di.unimi.it/ardagna), [Alessandro Balestrucci](https://sites.google.com/view/alessandrobalestrucci/scientific-activity), [Nicola Bena](https://homes.di.unimi.it/bena), [Ernesto Damiani](https://sesar.di.unimi.it/staff/ernesto-damiani/), [Chan Yeob Yeun](https://www.ku.ac.ae/academics/college-of-engineering/department/department-of-electrical-engineering-and-computer-science/people/dr-chan-yeob-yeun)

>  Machine learning is becoming ubiquitous. From financial to medicine, machine learning models are boosting decision-making processes and even outperforming humans in some tasks. This huge progress in terms of prediction quality does not however find a counterpart in the security of such models and corresponding predictions, where perturbations of fractions of the training set (poisoning) can seriously undermine the model accuracy. Research on poisoning attacks and defenses received increasing attention in the last decade, leading to several promising solutions aiming to increase the robustness of machine learning. Among them, ensemble-based defenses, where different models are trained on portions of the training set and their predictions are then aggregated, are getting significant attention, due to their relative simplicity and theoretical and practical guarantees. Surprisingly, ensemble-based defenses, which do not pose any restrictions on the base model, have not been applied to increase the robustness of random forest. The work in this paper aims to fill in this gap by designing and implementing a hash-based ensemble approach that protects random forest against untargeted, random poisoning attacks. An extensive experimental evaluation measures the performance of our approach against a variety of attacks, as well as its sustainability in terms of resource consumption and performance, and compares it with a traditional monolithic model based on random forest. A final discussion presents our main findings and compares our approach with existing poisoning defenses targeting random forests.

This repository contains the four datasets used in the experimental evaluation: **Musk2 (M2)**, **Android malware (AM)**, **Spambase (SB)**, and **Diabetic Retinopaty Debrecen (DR)**. The datasets significantly differ in terms of cardinality, number of features, and sparsity.

| Name | Cardinality | N features | Sparsity (%) | Cardinality after preprocessing | File name |
| - | - | - | - | - | - |
| **Musk2 (M2)** | 6598 | 166 | 0.28 | 2034 | [m2.csv](m2.csv) |
| **Android malware (AM)** | 18733 | 1000 | 92.37 | 14508 | [am.csv](am.csv) |
| **Spambase (SB)** | 4061 | 57 | 77.44 | 3626 | [sb.csv](sb.csv) |
| **Diabetic Retinopathy Debrecen (DR)** | 1151 | 19 | 10.41 | 1080 | [dr.csv](dr.csv) |

Each csv file in this repository contains the corresponding dataset. CSV files have `N features` + 1 columns, where the last column (`Class`) contains the class label.

## Dataset: M2

M2 is an open dataset for the identification of musk molecules [[https://archive.ics.uci.edu/ml/datasets/Musk+%28Version+2%29](https://archive.ics.uci.edu/ml/datasets/Musk+%28Version+2%29)], divided in two classes *musk* and *non\-/musk*. The dataset is collected by including different conformations (shapes) of musk and non-musk molecules. In particular, all the low-energy conformations of 141 initial molecules have been generated and manually annotated.

The dataset consists of 6,598 data points (1,017 musk and 5,581 non musk), organized in 166 features with low sparsity 0.28%. We then built a balanced dataset of 2,034 points by randomly subsampling data points in class non mask. We finally split the dataset in a training set of 1,628 data points (810 musks and 818 non musks) and in a test set of 406 data points (207 musks and 199 non musks).

Below we show an excerpt of the dataset.

| 'f1' | 'f2' | 'f3 | 'f4' | ... | Class |
| - | - | - | - | - | - |
| 38 | 68 | 28| -65 | ... | 0 |
| 49 | -194 | -145 | 28 | ... | 1 |

## Dataset: AM

AM is a dataset collected at [Khalifa University](ku.ac.ae) for the detection of malware on Android devices. The dataset is collected on Android devices with benign and malign apps installed, by capturing the system calls performed by the apps. Any sequence of three consecutive system calls is a feature, whose value is the number of times such sequence has been called.

The dataset consists of 18,733 data points (7,254 malware and 11,479 non malware), organized in 25,802 features with high sparsity (92.37%).  We then built a balanced dataset of 14,508 points, by randomly subsampling data points in class non malware. We further split the dataset in a training set of 11,607 data points (5,731 malware and 5,776 non malware) and in a test set of 2,901 data points (1,423 malware and 1,478 non malware). Finally, being a dataset with high dimensionality and more features than data points, to avoid overfitting, we reduced the number of features according to *InfoGain* [[https://link.springer.com/article/10.1007/BF00116251](https://link.springer.com/article/10.1007/BF00116251)], a feature ranking method selecting those features that reduce the *entropy* in the dataset (i.e., the most informative features with regards to the dataset). With this method, we reduced the number of features to 1,000.

Below we show an excerpt of the dataset.

| 'ppoll ppoll ppoll' | 'futex ppoll ppoll' | 'ppoll ppoll futex' | 'ppoll futex ppoll' | ... | Class |
| - | - | - | - | - | - |
| 0 | 0 | 0| 0 | ... | 0 |
| 49 | 11 | 9 | 5 | ... | 1 |

**Note**: the dataset included here is an excerpt (20% at random) of the original dataset. For access to the complete dataset please contact

- [Nicola Bena (Università degli Studi di Milano)](mailto:nicola.bena@unimi.it)
- [Sangyoung Yoon (Khalifa University)](mailto:sangyoung.yoon@ku.ac.ae)

## Dataset: SB

SB is an open and well-know dataset for spam detection in email body messages [[https://doi.org/10.1007/s10994-007-5004-z](https://doi.org/10.1007/s10994-007-5004-z)], [[https://researchcommons.waikato.ac.nz/handle/10289/2131](https://researchcommons.waikato.ac.nz/handle/10289/2131)], [[https://infoscience.epfl.ch/record/83272](https://infoscience.epfl.ch/record/83272)], [[https://archive.ics.uci.edu/ml/datasets/Spambase](https://archive.ics.uci.edu/ml/datasets/Spambase)]. It contains features counting the occurrence of particular words and the length of sequences of consecutive capital letters.

The dataset consists of 4,061 data points (2,788 spam and 1,813 non spam), organized in 57 features with medium-high sparsity but lower than AM (77.44%). We then built a balanced dataset of 3,626 points, by randomly subsampling data points in class spam. We finally split the dataset in a training set of 2,901 data points (1,458 spam and 1,433 non spam) and in a test set of 725 instances (355 spam and 370 non spam).

Below we show an excerpt of the dataset.

| 'word_freq_make' | 'word_freq_address' | 'word_freq_all' | 'word_freq_3d' | ... | Class |
| - | - | - | - | - | - |
| 0 | 0 | 0 | 0 | ... | 0 |
| 0.54 | 0 | 1.08 | 0 | ... | 1 |

## Dataset: DR

DR is an open dataset for the detection of symptoms of diabetic retinopathy [[https://doi.org/10.1016/j.knosys.2013.12.023](https://doi.org/10.1016/j.knosys.2013.12.023)], [[https://archive.ics.uci.edu/ml/datasets/Diabetic+Retinopathy+Debrecen+Data+Set](https://archive.ics.uci.edu/ml/datasets/Diabetic+Retinopathy+Debrecen+Data+Set)]. It contains features extracted from the Messidor image set [[https://doi.org/10.5566/ias.1155](10.5566/ias.1155)]. All features are numeric and represent either a detected lesion, a descriptive feature of a anatomical part, or an image-level descriptor. The class feature states if an image contains signs of diabetic retinopathy or not.

The dataset consists of 1,151 data points (611 signs of disease and 540 no signs of disease), organized in 19 features with low sparsity but higher than M2 (10.41%). We then built a balanced dataset of 1,080 points, by randomly subsampling data points in class signs of disease. We finally split the dataset in a training set of 864 data points (431 signs of disease and 433 no signs of disease) and in a test set of 216 data points (109 signs of disease and 107 no signs of disease).

Below we show an excerpt of the dataset.

| 0 | 1 | 2 | 3 | ... | Class |
| - | - | - | - | - | - |
| 1 | 1 | 1 | 1 | ... | 0 |
| 1 | 1 | 49 | 47 | ... | 1 |

For additional details, please check our paper.

## Acknowledgements

  Research supported, in parts, by Technology Innovation Institute (TII) under Grant 8434000394, by the project MUSA - Multilayered Urban Sustainability Action - project, funded by the European Union - NextGenerationEU, under the National Recovery and Resilience Plan (NRRP) Mission 4 Component 2 Investment Line 1.5: Strenghtening of research structures and creation of R\&D "innovation ecosystems", set up of "territorial leaders in R\&D" (CUP  G43C22001370007, Code ECS00000037).
  Research partially supported also by the project SERICS (PE00000014) under the NRRP MUR program funded by the EU - NextGenerationEU.