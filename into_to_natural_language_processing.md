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


