# Multilingual Extractive Reading Comprehension by Runtime Machine Translation
We introduce the first extractive RC systems for  non-English languages, without using language-specific RC training data, but instead by using an English RC model and an attention-based Neural Machine Translation (NMT) model [1].  

![The Overview](https://github.com/AkariAsai/extractive_rc_by_runtime_mt/blob/master/overview.png)

## Contents
1. [Code](#code)
2. [Datasets](#datasets)
3. [Benchmarks](#benchmarks)
4. [Reference](#reference)
5. [Contact](#contact)

## Code
We implemented our NMT and extractive RC models (BiDAF, BiDAF + Self Attention + ELMo) in [PyTorch](https://pytorch.org/).  
**Code will be released soon.**

## Datasets
We provide the two datasets, (1) multilingual SQuAD Datasets (Japanese, French) and (2) {Japanese, French}-to-English bilingual corpora to train our NMT models for the extractive RC system.

#### Multilingual SQuAD Datasets
The Japanese and French datasets are created by manually translating the original [SQuAD](https://rajpurkar.github.io/SQuAD-explorer/) (v1.1) development dataset into Japanese and French.  
These datasets contains 327 questions for each.  
More details can be found in Section 3.3 (SQuAD Test Data for Japanese and French) in [1].

| | Multilingual SQuAD Datasets       |
| ------------- |:-------------:|
| Japanese    | [japanese_squad.json](datasets/squad_japanese_test.json) |
| French | [french_squad.json](datasets/squad_french_test.json) |


#### {Japanese, French}-to-English bilingual Corpora
##### Wikipedia-based {Japanese, French}-to-English bilingual corpora
To train the NMT model for specific language directions, we take advantage of constantly growing web resources to automatically construct parallel corpora, rather than assuming the availability of high quality parallel corpora of the target domain.  
We constructed bilingual corpora from Wikipedia articles, using its inter-language links and [hunalign](https://github.com/danielvarga/hunalign), a sentence-level aligner.  
More details can be found in Supplementary Material Section A (Details of Wikipedia-based Bilingual CorpusCreation) in [1].  

To download preprocessed Wikipedia-based {Japanese, French}-to-English bilingual corpora, please run the commands below.  

```sh
cd datasets
wget http://www.hal.t.u-tokyo.ac.jp/~asai/datasets/extractive_rc_by_runtime_mt/wiki_corpus.tar.gz
tar -xvf wiki_corpus.tar.gz && rm -f wiki_corpus.tar.gz
cd ..
```

The downloaded wikipedia-based corpora will be placed under `datasets/wiki_corpus` folder.  
The training data includes 1,000,000 pairs, and
the development data includes 2,000 pairs.

##### Manually translated question sentences
In our experiment, we also found that adding a small number of manually translated question sentences could further improve the extractive RC performance.   
Here, we also provide the translated question sentences we actually used to train our NMT models.  
The details pf the creation of these small parallel questions datasets can be found in Supplementary Material Section C (Details of Manually Translated SQuAD DatasetQuestions Creation) in [1].

| | question sentences        |
| ------------- |:-------------:|
| Japanese     | [questions.ja](datasets/questions_jaen.ja), [questions.en](datasets/questions_jaen.en) |
| French  | [questions.fr](datasets/questions_fren.fr), [questions.en](datasets/questions_jaen.en) |


## Benchmarks
We provide the results of our proposed method on multilingual SQuAD datasets.
- Japanese

| methods|F1          | EM  |
| ------------- |:-------------:| :-----:|
| Our Method| **52.19** | **37.00** |
| back-translation baseline| 42.60|24.77|

- French

| methods |F1          | EM  |
| ------------- |:-------------:| :-----:|
| Our Method | **61.88** | **40.67** |
| back-translation baseline | 44.02 | 23.54|



## Reference
Please cite [1] if you found the resources in this repository useful.

[1] Akari Asai, Akiko Eriguchi, Kazuma Hashimoto, and Yoshimasa Tsuruoka. 2018. "[Multilingual Extractive Reading Comprehension by Runtime Machine Translation](https://arxiv.org/abs/1809.03275)".

## Contact
Please direct any questions to [Akari Asai](https://akariasai.github.io/) at akari-asai@g.ecc.u-tokyo.ac.jp.
