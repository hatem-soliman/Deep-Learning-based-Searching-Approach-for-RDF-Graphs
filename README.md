# Deep-Learning-based-Searching-Approach-for-RDF-Graphs
Search engines retrieve requested information based on the provided keywords. Consequently, it is difficult to accurately find the required information without understanding the syntax and semantics of the content. Multiple approaches are proposed to resolve this problem by employing the semantic web and linked data techniques. Such approaches serialize the content using the Resource Description Framework (RDF) and execute the queries using SPARQL to resolve the problem. However, an exact match between RDF content and query structure is required. Although, it improves the keyword-based search; however, it does not provide probabilistic reasoning to find the semantic relationship between the queries and their results. From this perspective, we propose a deep learning-based approach for searching RDF graphs. The proposed approach treats document requests as a classification problem. First, we preprocess the RDF graphs to convert them into N-Triples format. Second, bag-of-words (BOW) and word2vec feature modeling techniques are combined for a novel deep representation of RDF graphs. The attention mechanism enables the proposed approach to understand the semantic between RDF graphs. Third, we train a convolutional neural network for the accurate retrieval of RDF graphs using the deep representation. The results show that the proposed approach is accurate and surpasses the state-of-the-art. 

Overview

The proposed approach performs RDF graph retrieval prediction as follows:
1) We reuse the history-data of RDF graphs as training data.
2) We apply the W3C validation service to RDF graphs for preprocessing.
3) We concatenate BOW and word2vec feature modeling techniques for a novel deep representation of RDF graphs.
4) A convolutional neural network is trained to anticipate the retrieval of RDF graphs. We pass the deep representation to the classifier as input that predicts the retrieval of RDF graphs.

Preprocessing Steps

We preprocess each of the RDF graph using the W3C Validation Service. We load each collected RDF graph using Apache Jena API (http://jena.apache.org/) to validate its syntax. Then, the validated RDF graph is loaded into the model that transforms the RDFs from serialization format to N-Triples format.

Deep feature representation

A BOW representation of each RDF graph provides a boolean (0 or 1) array or a term frequency array using all repository terms and does not incorporate the semantic similarity among terms. Moreover, problems like high dimensionality and sparse data are observed in the bag-of-n-words feature representation. To this end, a neural network-based features representation model (word2vec) is proposed to learn and understand the semantic relationship between terms (predicates in our case). However, word2vec only considers semantics of individual terms rather than a sequence of words. Notably, a significant improvement is required to combine the sequence of terms, the syntax of terms, the semantic relationship among terms. In this perspective, a deep representation of RDF graphs is proposed. The long short term memory (LSTM) cells are exploited as a memory unit in the hidden layer that resolve the vanishing gradient problem. LSTM cells can memorize the sequence of terms in both forward direction and backward direction.

The hyper-settings of the proposed deep representation model as follows: 300 LSTM units, 0.2 dropout probability, 0.001 learning rate, and binary cross-entropy based loss function with Adam optimizer. We set 100 epochs for the training. Notably, the proposed model is implemented in Python Keras Library. To the best of our knowledge, we are the first to apply deep representation to learn the RDF graph representation. We use deep representation to train a convolutional neural network for the retrieval anticipation of RDF graphs.

Deep learning classifier

We leverage the convolutional neural network for retrieval prediction of RDF graphs. We select the convolutional neural network because of the following reasons: 1) its deep semantic relationship learning capabilities among words; 2) it avoids the gradient problem of recurrent neural network by applying different filter sizes. To train the convolutional neural network, the deep representation is forwarded to convolutional neural network that contains 3 layers of CNN, filter 128, kernel size 1, loss function
binary-crossentropy, and activation tanh. Then, the output of the convolutional neural network is passed to a flatten layer that returns a 1-dimensional vector. Finally, the dense layer connects the neurons between layers and the output layer returns the retrieval prediction of RDF graphs.

Dataset

We collect the DBpedia dataset (https://wiki.dbpedia.org/data-set-30). DBpedia 2016-10 release contains 13 billion pieces of information out of which 1.7 billion were extracted from the English edition of Wikipedia. We use only 1.7 billion RDF triples (English version) to evaluate the proposed approach; however, we ignore all syntactically invalid triples. Note that we divide the data into four different search categories: Triple-pattern requests with multiple responses; e.g., British actors and their birth regions, Extended triple-pattern requests with multiple responses; e.g., Movies having award-winning feminist actors, Triplepattern requests with zero responses; e.g., MIT graduates born in Steve Jobs???s death place, and Extended triple pattern requests with zero responses; e.g., People who influenced by Egyptian writers to evaluate the proposed approach.

