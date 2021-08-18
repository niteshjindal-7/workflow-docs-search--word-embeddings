# workflow-docs-search-[word-embeddings]

The dataset can be found at the below link:
https://drive.google.com/drive/folders/1qIueRHoH06Lux1Kd0pmoiBQxx33ECOK-?usp=sharing

Feel free to change the directory name while running the script.

## **Background:-**

Our aim is to aid a hospital personnel in finding a suitable workflow document to carry out a medical procedure smoothly as per the provided information in the workflows. 
That is to say, if a nurse is promptly handed with a childbirth workflow when she intends to look for it by typing related keywords in searchbox, it is convenient for her to follow the medication administration guidelines as per the document while treating a patient thereby reducing the human errors and making the entire process efficient.

To address this concern, we collected the sample workflow documents in portable document format(pdf), which include illustrations and text data. We can call these documents as training documents. Then, we built a corpus of words from the documents (i.e. vocabulary of unique words from all the training documents) and then trained a word2vec embedding model to get a vector representation of each significant word followed by an averaging of all the word-level embeddings in a document to obtain document-level embeddings. Once we had the document embeddings, we find the similarity score between each document embedding with an embedding obtained from the user seach inquiry. Higher the similarity score implies that a given document is more relevant to user’s query.documents with high similarity score are displayed to the user as a result. 

Word2Vec is a three layer neural network  (input, 1-hidden, output) that learns the weights of hidden layer  creates vector representation of words of D dimension ( i.e. embedding size) based on the context they have been used for. Therefore, words with similar contexts tend to have similar embeddings. Although there is a basic approach to create such embeddings, such as bag-of-words model, but it fails to capture the context of the words. 

This approach requires a format of list of list for training (i.e. as an input) where every document is contained in a list and every list contains list of tokens of that documents. To get such an input, we transformed raw pdf documents to text data and then performed text cleaning to remove whitespaces, most frequent words, numbers, distracting quotes, alphanumeric values from the text and developed a corpus having a list of documents with each document containing a list of tokens.That is, each document contained meaningful tokens, which describes that document.

Before passing this input to Word2Vec model function from gensim module, we set some of the model parameters:

  •	size=100. It refers to the embedding size or size of neurons in the hidden layer and is set to 100 because we did not have vast corpus size.
  
  •	window=5. Model will capture information for the two words after and two words before the input vocab word during learning phase. 
  
  •	sg=1. It implies that skip-gram model would be used whereas sg=0 implies that continuous bag-of-words model would be used.
  
  •	alpha=learning rate which helps in minimising the loss function in each iteration.
  
Once the model is trained and loaded, we capture the similarity scores of documents with user search query and the documents with high similarity score tends to me more closer to user query and displayed as a result.


## **Scope of Improvement:-**

  •	Existing document embedding approach can be replaced by using the advanced word embedding algorithms, such as BERT and ELMo which are capable enough to understand negation words and are computationally efficient.
  
  •	Documents embeddings are likely to be similar for a particular topic or context. We can form a community of such embeddings in the form of various clusters.This could be achieved by using graph based community algorithm where each document embedding becomes a node and closer nodes form a cluster.Instead of parsing each document embedding , we could just measure which cluster of nodes(doc embeddings) is closer to user search query.
  
  
## **References:-**

Word2Vec:

  https://rare-technologies.com/word2vec-tutorial/
  
  https://radimrehurek.com/gensim/auto_examples/tutorials/run_word2vec.html
  
  https://israelg99.github.io/2017-03-23-Word2Vec-Explained/
  
  http://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/
  
  https://medium.com/analytics-vidhya/combining-word-embeddings-to-form-document-embeddings-9135a66ae0f
  
  https://medium.com/@zafaralibagh6/a-simple-word2vec-tutorial-61e64e38a6a1

Text clustering as graph community detection:

 https://www.python-course.eu/networkx.php
 
 http://snap.stanford.edu/class/cs224w-2016/projects/cs224w-58-final.pdf
 
 https://link.springer.com/article/10.1007/s10994-020-05882-8
 
 https://arxiv.org/pdf/2104.09439.pdf
 
 https://arxiv.org/abs/0803.0476   
 
 https://www.sciencedirect.com/topics/computer-science/community-detection
 
 https://arxiv.org/ftp/arxiv/papers/1512/1512.07827.pdf
 
 https://python-louvain.readthedocs.io/en/latest/api.html
 
 https://readthedocs.org/projects/python-louvain/downloads/pdf/latest/
