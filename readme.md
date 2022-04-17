ldig (Language Detection with Infinity Gram)
======================

This is a prototype of language detection for short message service (twitter) with 99.1% accuracy for 17 languages.

__ldig can also be used with success on longer documents.__
This version was initiated in the context of research conducted at the University of Corsica, for the automatic processing of less resourced languages, and in particular of Corsican. The results recorded in Kevers (2022) showed an average accuracy between 99.10% and 99.71% for 18 languages (17 official EU languages + Corsican).

ldig-python3 fork
------

The motivations for this fork are :
- adaptation of ldig to __python3__
- add alphabets (greek an cyrilic) not supported in the original version.


Usage
------

You can use ldig with the provided model or you can retrain a new model from your own data.

__Standard use with provided models :__

1. Extract model directory

        tar xf models/[select model archive]

2. Detect

        ldig.py -m [model directory] [text data file]

__Train new models__

1. Compile maxsubst executable (if not already done)

        cd maxsubst
        g++ -Icybozulib/include maxsubst.cpp -o maxsubst

2. Prepare your data

    Learning data must be placed in a file formated as follow :

        CorrectLabel [TAB] Metadata [TAB] Text.

3. Initialisation

        python3 ldig.py -m [ModelDir] -x [MaxSubStBin] --init [LearnCorpusFile]

    Several options are available :

        --ff=[LowerLimitOfFrequency] : threshold of feature frequency
        -n [NgramUpperBound] : n-gram upper bound

4. Learning

        python3 ldig.py -m [ModelDir] --learn [TxtCorpusFile] -e [LearningRate]

    Several options are available :

        -r [RegularizationConstant] : regularization constant
        --wr [NumWholeRegularizations] : number of whole regularizations

5. Optimisation (optional)

        python3 ldig.py -m [ModeliDir] --shrink


Data format
------

As input data, Each "document" (tweet or other) is one line in text file as the below format.

    [label]\t[some metadata separated '\t']\t[text without '\t']

[label] is a language name like en, de, fr and so on.
Metadata is optional, but the tabulation symbol has to be present.
(ldig doesn't use metadata and label for detection, of course :D)

The output data of lidg is as the below.

    [correct label]\t[detected label]\t[original metadata and text]


Estimation Tool
----

ldig has a estimation tool.

    ./server.py -m [model directory]

Open http://localhost:48000 and input target text into textarea.
Then ldig outputs language probabilities and feature parameters in the text.


Supported Languages (with provided models)
------

- cs	Czech
- da	Dannish
- de	German
- en	English
- es	Spanish
- fi	Finnish
- fr	French
- id	Indonesian
- it	Italian
- nl	Dutch
- no	Norwegian
- pl	Polish
- pt	Portuguese
- ro	Romanian
- sv	Swedish
- tr	Turkish
- vi	Vietnamese

Supported Languages (with Laurent Kevers models, data available at https://github.com/lkevers/ldig-models-TAL62-3)
------

The models have to be generated from the data following the documented procedure.

These models are designed to support 17 official languages of the European Union, plus Corsican.

- bg / bul - Bulgarian
- co / cos - Corsican
- cs / ces - Czech
- da / dan - Danish
- de / deu - German
- el / ell - Greek
- en / eng - English
- fi / fin - Finnish
- fr / fra - French
- hu / hun - Hungarian
- it / ita - Italian
- lt / lit - Lithuanian
- nl / nld - Dutch
- pl / pol - Polish
- pt / por - Portuguese
- ro / ron - Romanian
- sp / spa - Spanish
- sv / swe - Swedish


Documents
------

- [Presentation in English](http://www.slideshare.net/shuyo/short-text-language-detection-with-infinitygram-12949447)
- [Presentation in Japanese](http://www.slideshare.net/shuyo/gram-10286133)

- Blog Articles about ldig
  - [Language Detection for twitter with 99.1% Accuracy](http://shuyo.wordpress.com/2012/02/21/language-detection-for-twitter-with-99-1-accuracy/)
  - [Precision and Recall of ldig (twitter language detection)](http://shuyo.wordpress.com/2012/03/02/precision-and-recall-of-ldig-twitter-language-detection/)
  - [Estimation of ldig (twitter Language Detection) for LIGA dataset](http://shuyo.wordpress.com/2012/03/02/estimation-of-ldig-twitter-language-detection-for-liga-dataset/)
  - [Why is Norwegian and Danish identification difficult?](http://shuyo.wordpress.com/2012/03/07/why-is-norwegian-and-danish-identification-difficult/)

- __Laurent Kevers publications using ldig-python3__ :
  - KEVERS, L. (2022). L’identification de langue, un outil au service du corse et de l’évaluation
des ressources linguistiques. _Traitement Automatique des Langues_, 62(3). Numéro spécial
" Diversité linguistique".https://www.atala.org/content/tal_62_3_-0 .
  - KEVERS, L. & RETALI -MEDORI , S. (2020). Towards a Corsican Basic Language Resource Kit.
In _Proceedings of the 12th Language Resources and Evaluation Conference_ (p. 2726-
2735). Marseille, France : European Language Resources Association. https://www.aclweb.org/anthology/2020.lrec-1.332

- For more information about NLP and Corsican : https://bdlc.univ-corse.fr/tal/

Copyright & License
-----
- (c) 2011-2012 Nakatani Shuyo / Cybozu Labs Inc. All rights reserved.
- (c) 2021 Laurent Kevers / University of Corsica (changes made for ldig-python3)
- All codes and resources are available under the MIT License.
