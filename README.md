# PreProcessor

CONTENTS
=========================

1. [Introduction](#1-introduction)
2. [Technical Information](#2-tech)
3. [Installation](#2-installation)
 	- 3.1. [External Libraries](#31-external-libraries)
    - 3.1.1 [NLP libraries](#32-nlp-libraries)
4. [Requirements](#4-requirements)
5. [Quick start](#5-quick-start)
    - 5.1. [Input formats](#51-input-formats)
6. [License](#6-license)



1. INTRODUCTION
=========================
PreProcessor is a program that helps users to preprocess textual data. Despite various Part of Speech taggers, Lemmatisers, Stemmers, Named Entities Recognisers and Stopword Checkers can be used for this purpose, they are independent programs built for only one specifically purpose (e.g. identify the word's stem). Thus, when users want to use more than one or import them in their own programs/ applications, their integration turns to be really complex and time-consuming. Accordingly, PreProcessor aims at offering the user with a simple, yet robust and agile variety of morphosyntatic options to annotate raw text by taking advantage of the best known open-source libraries on the market.



2. TECHNICAL INFORMATION
=========================

* This program provides several abstraction methods to several NLP tools, such as TreeTagger, Snowball and OpenNLP and several similarity Measures, which permits to do:
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


2. INSTALATION
=========================

1. Import the code to your Java editor.

2. Copy the folder 'config' and 'resources' to the root of your project (it should be at the same level as the src folder).
	* the folder 'resources' contains models for the:
		* TreeTagger
		* OpenNLP
		* Stanford NLP
		* and Stopword Lists

	* the folder 'config' contains configuration files for the Semantic Similarity Measures. You need to configure the folowing files and parameters, see step 3 first:
		* adw.properties 
			* wn30g.ppv.path= path to: /externalResources/adwResources/ppvs.30g.5k/
			* offset.map.file= path to: /externalResources/adwResources/offset2ID.map.tsv
			
		* jlt.properties
			* wordnet.wordnetData3.0= path to: /externalResources/adwResources/WordNet-3.0/dict
			* stopwords.FilePrefix = path to: /externalResources/adwResources/jlt/stopwords/stopwords
			* stanford.pos.model= path to: /externalResources/adwResources/jlt/stanford/left3words-wsj-0-18.tagger

3. Copy the folder 'externalResources' to your workspace (it should be at the same level as your project is).
	* this folder contains semantic signatures for the Semantic Similarity Measures

	* please check if the Semantic signatures are up-to-date through http://lcl.uniroma1.it/adw/ppvs.30g.5k.tar.bz2, if yes go to step 4.

		* if an update is required: Extract the downloaded file into a directory of your choice, I sugest you to use: 
			* /resources/adwResources/ (it should be at the same level as your project is)

		* then, update the 'wn30g.ppv.path' entry in the 'config/adw.properties' file, with the directory containing semantic signatures.






## 2.1 External Libraries 

This section is important to let you know what libraries are used in this project, as weel as to know how to update the resources or models.


#### 2.1.1 NLP libraries
	* TreeTagger
		* provides a POS Tagger for EN, SP, PT, FR, DE, IT and RU
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
		* provides a **sparser** in EN and ES




#### 2.1.2 Semantic Similarity Libraries
	* ADW
		* Semantic Similarity Library provides ....

		* adw.v1.0, read: ADW-README.txt
		* This package provides an implementation of Align, Disambiguate, and Walk (ADW). ADW is a WordNet-based approach for measuring semantic similarity of arbitrary pairs of lexical items, from word senses to full texts. The approach leverages random walks on semantic networks for modeling lexical items.

#### 2.1.3 Translation Libraries
	* Yandex (http://api.yandex.com/translate/doc/dg/yandex-translate-dg.pdf)
		* get API Key: http://api.yandex.com/key/form.xml?service=trnsl
		* requires:
			* json_simple-1.1.jar

	* in the future take a look at webservicex (http://www.webservicex.net/ws/WSDetails.aspx?CATID=12&WSID=63)
		* example
			* http://www.webservicex.net/TranslateService.asmx/Translate?LanguageMode=SpanishTOEnglish&Text=Hola
			* http://www.webservicex.net/TranslateService.asmx?WSDL

#### 2.1.4 Dictionaires
	* BabelNet WebService
		* requires:
			* commons-io-2.4.jar
			* jsoup-1.8.1.jar


#### 2.1.5 Wordnet Libraries
	* JWI
		* requires:
			* edu.mit.jwi_2.3.3

#### 2.1.6 Database Connectors
	* Mysql
		* when mysql does not want to start: sudo /Applications/XAMPP/xamppfiles/bin/mysql.server start
		* mysql-connector-java-5.1.29-bin.jar

#### 2.1.7 Others
	* CSV
		* To read and write CSV files
		* opencsv-3.3.jar
		* http://opencsv.sourceforge.net/#how-to-read

3. REQUIREMENTS
=========================

- Java 6 (JRE 1.6) or higher

- Semantic signatures (see [Installation](#2-installation))
- WordNet 3.0 dictionary files (already included in the resources directory)
- Several models (already included either in the 'internalResources' or in the 'externalResources' folder)




4. QUICK START
=========================

The following is a usage example to do POS tagging, Lemmatisations, Stemming,  and measure the semantic similarity.
In detail, this jar allows you to do:

* POS Tagging (EN and ES) 
	* @ SentenceAnalyser.getTaggedSentenceList: receives a sentence to be tagged and returns a list with tags.

* Lemmatisation (EN and ES)
	* @ SentenceAnalyser.getLemmatizedSentenceList: receives a sentence to be lemmatised. Please make sure that you called the @ getTaggedSentenceList(String rawSentence) method first.

* Stemming (EN and ES)
	* @ SentenceAnalyser.getStemmedTokensList: receives a list of tokens/words to be stemmed and returns a stemmed list of tokens.

* Stopword Checker (EN and ES)
	* @ SentenceAnalyser.getStopwordCheckerList: receives a list of tokens/words and returns a boolean list with true's and false's (true means that the token/word is a stopword).

* Common Categories Checker (EN and ES)
	* @ SentenceAnalyser.getCommonCategories: receives two tokanized sentences in the same language and returns the intersection of the common named entities categories extracted from the two sentences.

* Semantic Similarity Measures (EN)
	* @ SentenceAnalyser. 
		* Cosine



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
