# Geo Classifier
# Results classification for solar observations database

## Install the project

To use this notebooks you will need to setup the notebook environment using a terminal and run:
`$ conda env create -f solarobs.yml`

then in you notebook you must start the kernel within this environment, it's located at top right, by default you should Have Python [env:default], when the correct environment is selected you should have Python [env:solarobs]

You can change the kernel in the menu Kernel > Change Kernel ...

If the environment is not shown, try to reload the jupiterlab web page.

## Run the project

All the implemented solutions can be found in the sources and run for the geocatalog webserver:
Each file can be run cell by cell

1. Supervised classification based on keywords

A first approach to classification is to get the most relevant keywords in the corpus and use them as
labels for supervised classification.
The first step is to build a keyword list that can be used for text classification. In order to do this, we
get the list of keywords from the metadata records and select the ones that are the similar to the
search keyword (above a predefined threshold).
For each metadata record, we are looking at the keywords that are attached and, if they are also
contained in the list of the best keywords, then the preprocessed metadata record is written in the
training file, together with its corresponding best keywords, as labels. The same text will be written
also in the test file, so the classifier will be able to find the best category for each metadata record.
If the metadata record doesn't have any keyword in the list, it is written to the test file to be labeled
through a machine learning algorithm.
In order to determine the best label for each metadata record, we used **fastText** classifier trained on
the labeled file

Main file that should be run:
 	Keyword_Clustering.ipynb
External libraries:
	It requires *fastText* installation and the path to it in the __imports__ file


2. K-Means classification

K-means clustering is one of the basic and generic unsupervised classification algorithms of
elements in a vectorial-space. Its objective is to group similar data points together (clusters), by
following patterns. 
The first step is to define a number k, which represents the number of clusters that will be formed. The center of each cluster is called
centroid.
The algorithm builds a corpus of the entries in the database and, using it and word2vec algorithm, it creates conenctions betweem words
to compute similarities. Then, it identifies k centroids and allocates each data point to the nearest cluster.
The algorithm starts with a first group of random centroids, then it performs repetitive calculations to optimize their positions. It stops whether the pre-set number of iterations has been reached or if there is no change in the positions of the centers.
In case of natural language, processing , word2vec embeddings are used in order to determine the position of each word in the multidimensional space. 

Main file that should be run:
	K-Means Classification.ipynb


3. Latent Semantic Analysis clustering

One of the most common techniques for automatically obtaining topics is Latent semantic analysis (LSA). It  builds relationships between a set of documents and the terms they contain by producing a set of concepts related to the documents and terms. 

As input, it received a corpus of documents and returns a number of different topics from it, together with the most prominent words of each. 
It uses bag of word(BoW) model, which results in a term-document matrix(occurrence of terms in a document). It builds a term frequency-inverse document frequency (tf-idf) where each position in the vector corresponds to a different word and a document is represented by the number of times each word appears. So, the most important words will be the ones that appear the most often in the documents. The LSA algorithms improve the process by also considering synonymy between words. It learns latent topics by performing a matrix decomposition on the document-term matrix using Singular value decomposition (SVD). This is a matrix factorization method that represents a matrix in the product of two matrices.
	
Main file that should be run:
	LDA_clustering.ipynb


4. Supervised classifier - Thematic Words

In case of short texts, as metadata records, the best approach is to build up a hierarchy of pre-defined words related to the topic and assign each text to those categories.

The approach in this case is the following:
	- run an unsupervised classifier for short texts to obtain several topics
	- build a similarity matrix between each set of expert labels and the obtained topics
	- add the similarities between each text and its topic to the matrix
	- for each topic, arrange the results in descending order, based on the similarity

Main file that should be run:
	Supervised Classifier-Thematic Words.ipynb

#Documentation

More information can be found in the documentation from the *doc* folder
