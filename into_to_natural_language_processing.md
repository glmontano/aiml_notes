In this section we learn how to use machine learning in nautral language (text) processing, and predictions

# 1.1 Word Representation

The first question is how to use text for machine learning pre-processing.

## One-Hot Encoding

This may be used in the context of the setting `the queen has entered the room`, which every word would be represented as an array, with a `1` or `0` appearing depending on the frequency of that word. Therefore we'd have `[1, 0, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0], [0, 0, 1, 0, 0, 0], [0, 0, 0, 1, 0, 0], [0, 0, 0, 0, 1, 0], [0, 0, 0, 0, 0, 1]`.

The issue with this methodology is the sparsness of the matrix in containing a majority of zeros, and the large amount of memory require for such a method. As such, an alternative is sought.

## Vectorization

Vectors may be used instead, which are similar to arrays. There are two `traditional-count-based approaches`.

1. Bad of Words (BoW)
2. Term Frequency - Inverse Document Frequency (TF-IDF)

### Vocabularly

A vocabularly is jargon in this vectorization representing the set of unique words after pre-processing a set of data. Each word is represented by a vector with as many elements as the vocabulary size. The vector will have a `1` in the index corresponding to the presence of the word in the vocabulary.

# 1.2 Vectorization Techniques

## Bag of Words (BoW)

BoW works by initializing a vector on a sentence by counting the occurence of each word. For example `I like cats do, do you like cats?` whas the vector `[i, like, cats, do, you] => [1, 2, 2, 1, 1]`. While this is a simple vectorization method, it doesn't capture the relationships between words. Limitations of BoW include

  - Volcabulary: Careful design is required to manage size
  - Sparse Data: Sparse data may exist, meaning computations from little information from a large representational sapce.
  - Meaning: Meaning of the sentence is lost if the order of the words is changed

## Term Frequency - Inverse Document Frequency

TF-IDF also works by counting, although, uses statistical measures to evaluate the importance of a word in a corpus or dictionary.

The value of the of a word in a vector follows a formula that can be understood through a number of steps. The formula is the product of 2 vectors, namely

`(Term Frequency) * (IDF)`,

where the multiplication is tuple-wise. Each have methods of calculation, which we will go through

### TF-IDF: Term Frequency Calculation

Consider `D` number of documents, each with a message of words. Pre-processing occurs, where each document's (`d`) message is sumarized into a fewer number of key words that maintain the message's meaning. It is on this pre-processes set of documents that under go the calculation, and for each document a vector is created.

`TF(Word in Doc-d) = (Num times word appears in d)/(Num of terms in d)`

This is performed for ever word `w` in `d`, and this is done for all `d`. As an example

1. Document 1: It is going to be sunny today
2. Document 1 Pre Processes: Go sunny today
3. Count `Go`: 1 times
4. Count `terms`: 3 times
5. `TF = 1/3`

This is repeated for every `w` in a `d`.

### TF-IDF: Inverse Document Frequency

The second vector counts the number of documents, before dividing it by the number of documents containing a word. Continuing with the example above

1. Documents 2 and 3 have preocesses messages of: `today not go office` and `go watch movie`
2. `go` appears in `D1`, `D2` and `D3`. Therefore
3. IDF(`go`) = log(3/3) = log(1) = 0

Indeed, the calculation takes the logarithm of the explained ratio.

### The multiplcation

At this stage, there will exist a matrix from TF and a vector from `IDF`. The multiplcation, which is tuple-wise, reuslts in a matrix of the same size as the TF` matrix.

## The Inner Workings on TF-IDF

TF-IDF's calculation seeks to reduce the importance of terms that are common across documents such as `about` or `but`. While they may be common, it does not mean the documents are about those prepositions.

Furthermore, words that appear a fewer number of doucments are deemed more relevant and have a higher weight. This way, TF-IDF attempt to give higher relevance scores to words that occur in fewer documents within the corpus.

# BoW vs TF-IDF

In conclusion - BoW is simple counting, and has no sematic information abou tthe document. Due to the simple counting method, it will give more relevant to words with higher frequency, such as `about` or `but`.

TF-IDF on the other hand has a weighted approach for importance. Those words that are less frequent are deemed more important. TF-IDF uses a normalized count, where each word is divided by the number of documentrs the word appears in.

# 1.3 Hands On

# 1.4 Text Classification

Text Classification is the process of processing meanings and labels on a given set of words. It is one of the fundamental tasks in natural language processing, with applications in sentiment analysis, topic labelings, spam detection and intent detection. There are two methods to perform TC

- (i) Manual: Using humans to annotate and provide context to the context, therefore time consuming and expensive.
- (ii) Automatic: Using machin learning, NLP and other AI techiques. This is significatnly faster and accurate.

Respectively, the methods of performing these are through `Rule Based Systems` and `Machine Learning Based`.

## Rules Based System

Here, human based rules are set for the classifcation. For example headlines or words containing "LeBron James" and "Lakers" will fall under the Sports classifcation.

These rules are human comprehensible and can be improved over time. However, these are time consuming since generating such rules for a complex system can be quite challenging and require lengthy analysis and testing. Furthermore, they are difficult to maintian and may not scale well. Finally, new rules may conflict with existing rules creating further complications. 

## Machine Learning Based

This method first requires historical data to be trained on. Classifcations are based on past observations and extracted features from the text and tags/labels of that text are used in training. With enough training ML models can make accurate predictions.

This method is usually more accurate than rule based systems, especially on complex NLP tasks.

Famous classification algorithms include Naive Bayes, Support Vector Machines (SVM) and deep learning algorithms.

# 1.5 Sentiment Analysis

Sentiment classifcation refers to the process of categorzing text as positive, negative, neutral or any other class depending on the the feelings that he user or consumner has expressed in the text. Some of the most important applications include in

1. Customer Product Reviews
2. Market Research and Analysis
3. Social Media Monitoring

Two methods for sentiment analysis are

1. TextBlob - NaiveBayesAnalyzer returns either positive, negative, and the probability of positivity/negativity
2. VADER - Rules based and used especially in social media. Uses dictionary that maps the lexical features (word frequency, word neighborhood count and word associations, etc) to the intensity of emotions known as sentiment scores. Uses `SentimentIntensityAnalyzer` class. The output is a dictionary with 4 keys: NEgative, neutral, positive and a compound representing the emotional intensity.

# 1.6 Sentiment Analysis - Hands On

# 1.7 Dense Encoding

First - we recall sparse vectors and matrices which are simply structures with a pertinent number of zeroes. Recall that these appear in the counting methods of vectorization in BoW and TF-IVF. When scaled with thousands of zeros and high dimensions, training may resuilt on poor model accuracy, and be computationally expensive to do so.

## Solving Sparseness with Dense Encodings

Dense encodings is a method that reduces the dimensionality of vectors, reducing the the vector size and therefore sparseness. Furthrermore, dense vectors also represent the semantics of the text.

Machine learning models are used to generate dense vectors including

1. Word2Vec -> CBOW and Skip-gram
2. GloVe
3. FastTExt

There are also neural network models such as BERT and CoVE which are fast, efficient to train and provide high performance.

# 1.8 Word2Vec

# 2.1 Introduction to Sequential Models

NLP using machine learning has 3 steps
- Proprocessing
- Feature extraction
- Modelling

So far, human designs in Bag of Words and TF-IDF led to feature extraction.

However, deep learning has progressed and may be a more powerful means of obtaining features.

One important point is that the embedding layer turns each word into a fixed-length vector of a specific size with 0s and 1s. This improves the processing of words and reduces dimensionality

Text data is known as sequential data, where the data has meaning through the given sequence of words. Other forms of sequential data include audio, video and time series. Change the sequence of the data will change the meanings and classifications.

Normal neural networks or ANN cannot be used for sequential data as they do not hold information of the sequence of data. As such, alternative are required. There are different neural netork models
  - RNN
  - LSTM

## Recurrent Neural Network (RNN)

RNNs activation fucntion has an additional connection pointing backwords, therefore transferring information backwords. This information is short-term memory. This allows the network to remember the neuron's previous value, and can pass it onto themselves in the future.

## Long Short-Term Memory

Similar to RNNs, though it has long term dependencies. It has a memory cell that can sotre information in memory for long periods.

This architecture allows LSTMs to converge faster while training and provides better performance compared to RNNs.

# 2.2










