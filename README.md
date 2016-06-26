# PreProcessor

TABLE OF CONTENTS
=========================

1. [Introduction](#1-introduction)
2. [Technical Information](#2-tech)
3. [Installation](#2-installation)
 	- 3.1. [External Libraries](#31-external-libraries)
    - 3.1.1 [NLP libraries](#32-nlp-libraries)
4. [Requirements](#4-requirements)
5. [License](#6-license)



1. INTRODUCTION
=========================
PreProcessor is a program that helps users to annotate raw textual data. Despite various Part of Speech taggers, Lemmatisers, Stemmers, Named Entities Recognisers, Stence Delimiters, Tokenisers and Stopword Checkers can be used for this purpose, they are independent programs built for only one specifically purpose (e.g. identify the word's stem). Thus, when users want to use more than one or import them in their own programs/ applications, their integration turns to be really complex and time-consuming. As an attempt to fulfil this gap, PreProcessor aims at offering the user with a simple, yet robust and agile variety of morphosyntatic options to annotate raw textual data by taking advantage of the best known open-source libraries on the market.



2. TECHNICAL INFORMATION
=========================

* This program provides several abstraction methods to several NLP tools, such as TreeTagger, Snowball and OpenNLP and several, such as:
	* POS Tagging (EN, ES, etc.)
		* @ SentenceAnalyser.getTaggedSentenceList(String rawSentence): receives a *sentence* to be tagged and returns a *list with tags*.
	* Lemmatisation (EN, ES, etc.)
		* @ SentenceAnalyser.getLemmatizedSentenceList(String rawSentence): receives a *sentence* to be lemmatised and returns a *list with lemmas*. *Please make sure that you called the @ SentenceAnalyser.getTaggedSentenceList(String rawSentence) method first*.
	* Stemming (EN, ES, etc.)
		* @ SentenceAnalyser.getStemmedTokensList(List<String> rawTokensList): receives a *list of tokens/words* to be stemmed and returns a *stemmed list of tokens*.
	* Check for Stopword (EN and ES)
		* @ SentenceAnalyser.getStopwordCheckerList(List<String> rawTokensList): receives a *list of tokens/words* and returns a *boolean list with true's and false's* (true means that the token/word is a stopword).
	* Check for Common Categories (EN and ES)
		* @ SentenceAnalyser.getCommonCategories(String[] tokanizedSentence1, String[] tokanizedSentence2): receives *two tokenized sentences in the same language* and returns a *HashMap<String, Boolean>* (String - category; Boolean - true if the category was found in both sentences), i.e. returns the intersection of the common named entities categories extracted from the two sentences.
			* Categories available for Spanish English: see section 2.1.1 NLP libraries.

* How to create the object:
	* SentenceAnalyser for English?
		* SentenceAnalyser sa = new SentenceAnalyser(Constants.EN);			
	* SentenceAnalyser for Spanish?
		* SentenceAnalyser sa = new SentenceAnalyser(Constants.ES);


3. INSTALATION
=========================

1. Import the code to your Java editor.

2. Copy the folder 'config' and 'internalResources' to the root of your project (it should be at the same level as the src folder).
	* the folder 'internalResources' contains models for the:
		* TreeTagger
		* OpenNLP
		* Stanford NLP
		* and Stopword Lists

	* the folder 'config' contains configuration files for the TreeTagger. You need to configure the treetagger.properties file.


## 3.1 External Libraries 
This section is important to let you know what libraries are used in this project, as weel as to know how to update the resources or models.

#### 3.1.1 NLP libraries
	* TreeTagger
		* provides a POS Tagger for EN, SP, PT, FR, DE, IT and RU
			* due to the github limitations, we need to download the RU model from the following address: http://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/data/russian-par-linux-3.2-utf8.bin.gz
		* The following java library allows to use TreeTagger in Java.
			* org.annolab.tt4j-1.0.15

	* Stemmer 
		* provides a Stemmer for EN, SP, PT, FR, DE, IT and RU
		* the following java library allows to use Stemmer in Java]
			* org.tartarus.snowball

	* OpenNLP
		* provides a **sentence splitter** and **tokenization** in EN, but can be used for at least EN, PT and SP
		* also provides **NER** for EN and SP, see models available through http://opennlp.sourceforge.net/models-1.5/
		* the following java library allows to use OpenNLP in Java
			* opennlp-maxent-3.0.3;
			* opennlp-tools-1.5.3; 
			* opennlp-uima-1.5.3
	
		* you can find these models inside the project folder, more specificaly in the "/resources/opennlpmodels/..." folder.
			* contains the following models for English:
				* Date name finder model.			
				* Location name finder model.		
				* Money name finder model.		
				* Organization name finder model.	
				* Percentage name finder model.	
				* Person name finder model.		
				* Time name finder model.
			* and the following models for Spanish:
				* Location name finder model, trained on conll02 shared task data.
				* Organization name finder model, trained on conll02 shared task data.	
				* Person name finder model, trained on conll02 shared task data.	
				* Misc name finder model, trained on conll02 shared task data.
			* the English and Spanish models are loaded by the 'NEREnModelsLoader' and 'NEREsModelsLoader' classes, respectivly.

	* Stanford NLP
		* provides a **parser** in EN and ES




4. REQUIREMENTS
=========================

- Java 6 (JRE 1.6) or higher
- Several models and libraries (already included either in the 'internalResources' or in the 'libs' folder)




5. LICENSE
=========================

Copyright (c) 2013-2016 University of Malaga, Spain. 
All rights reserved.

For more information please contact:

> hercos (at) uma (dot) es



### Follow me on
<!-- Please don't remove this: Grab your social icons from https://github.com/carlsednaoui/gitsocial -->

<!-- display the social media buttons in your README -->

[![alt text][1.1]][1]
[![alt text][2.1]][2]
[![alt text][3.1]][3]
[![alt text][4.1]][4]



<!-- links to social media icons -->
<!-- no need to change these -->

<!-- icons with padding -->

[1.1]: http://i.imgur.com/tXSoThF.png (twitter icon with padding)
[2.1]: http://i.imgur.com/P3YfQoD.png (facebook icon with padding)
[3.1]: http://i.imgur.com/yCsTjba.png (google plus icon with padding)
[4.1]: http://i.imgur.com/0o48UoR.png (github icon with padding)


<!-- links to your social media accounts -->
<!-- update these accordingly -->

[1]: https://twitter.com/#!/hernanimax
[2]: https://www.facebook.com/hernani.costa.161
[3]: https://plus.google.com/+HernaniCosta
[4]: https://github.com/hpcosta
