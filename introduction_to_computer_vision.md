# 1.1 ANNs vs CNNs

We are looking at all of this in the context of 'Image Classification'. Images are converted to data via a `Picture Elemenet` (`PixEl`) repreentation. Each pixel is a smallest point on the image that'd appear on one's screen, that represents a degree of a single color and stored in memory. 

Since most images are colored or  `RGB` - there are further PixEl-sets of data for each R, G and B - thereby increasing the size of data.

To begin - let's look at images in the absence of color or `greyscale`. In this case, every PixEl takes a value between an including 0 and 255, where 0 repreents black, 1 is white and the values inbetween are shades of grey.

All images are naturally represented by a matrix of PixEls, but for the process of machine learning, are row-stacked together into a single column or vector, before inputting the model. Following a simple 2-output classifical model leads the neural network to be called an Artificial Neural Network, that has it's problems.

 Some challenges with ANNs include
 - Inability for translational invariance
 - Inability for spatial invariance

ANNs treat every PixEl independently, without relation. This creates issues when say identifying a complex image where its features depends on the location of others. Think of a cat and its ears, hose and eyes.

ANNs also lack in detecting which features of an image are important. Think of a picture of a cat, with a branch in the background.

ANNs are very computationally expensive. A 28x28 PixEl image, with 32 neurons in the first hidden layers, means having to train 50,000 weights.

The answer to these problems are Convolutional Neural Networs or CNNs

## CNNs

CNNs are
- Spatial invariant
- Translation invariant
 
This works through two additional layers prior to a hidde layer. These are the `convolutional` and `pooling` layers. The convolutional layer utilizes a kernal, which is constant matrix that multiplies through (have to define the multiplication) or slides throught the entire pixel set, thereby enhancing or ensuring the extraction of features (have to better understand this).

The pooling layer looking at subsets of the data to extract features, and looks at minimums, maximums and averages of a feature.

CNNs also have a computational advantage. For an RGB 50x50 image, and ANN would rely on 50x50x3=7500 trainable parameters. CNNs however may use 10 sets of 3x3 kernels (the 10 is called a filter in this case). Each kernel is responsible for identifiying a feature. Further one will exist for each R, G and B though the number of inputs in this case is (3x3x3+1)x10 = 280 trainable parameters. Kernels therefore reduce dimensionality.

# 1.2 CNN Architecture

A CNN can be viewed as two stages.

(1) Feature Extraction Satge
(2) Prediction Stage

### Prediction Stage

For simplicity - the Prediction Stage is a simple ANN, and is all that we've learn so far about neural networks. The input here is a flattened repreesntation of the iamge from the Feature Extraction Stage. Thereafter, fully connected layers lead to the classification of the image. In the case of identifying whether an image is a cat - it is True or False (perhaps a dog).

### Feature Extraction Stage

This is the new stage for the CNN, containing the Convolution and Pooling layers.

Convolution layers identify features of the image, and pooling to simplify outputs and less sensitive to locations. There may be multiple convolution and pooling layers. Once the features are deemed to be well extracted - they may enter the Prediction Stage or the ANN.

## The Convolutional Layer

Here, we revisit how the convulational layer works. It can be seen as a process where
- a filter or kernel is established. This has a dimension less then that of the image
- it is applied multiple times across the image, before a multiplicative process is applied
- The result of the multiplicaiton process, at each filter application, makes an output

The values of the filter are weights or trainable parameters, that are optimized using gradient descent.

The output then enters a ReLu activation function. This is deemed the best function as it makes negative numbers 0, and this is useful as negative numbers don't exist in PixEls.

## Pooling

The next step in Feature Extraction is Pooling. The pooling layer helps removing unwanted features from the image, thereby reducing the size of the image and the computational cost.

Pooling works by scanning through subsets of the feature map, and taking either the maximum, minimum or average. Of course, this means loss in information. However, for the purpose of feature extraction - we are OK in loosing immaterial pieces of information such as, multiple pixels of fur and so on. Perhaps, there're redundant pieces of information in classifying an image.

Pooling also helps with Spatial Invariance. It looks for cats in various sections of the image. Lastly, taking only pieces of information improve computational power, but also overfitting.

## Flatten Layer

All the columns of the output matrices are flattend into a single column, before entering the ANN.

# 2.1 Regularization in CNN's

Recall that overfitting is the result of a model incorporating both a training dataset's information and noise, therefore resulting in poor performance in out-of-sample or testing data sets. This is also described as the model overgeneralizing on the training dataset or `overfitting`. This fault also appears in the calibration of parameters in a CNN.

As previously learnt - `regularization` is the processs of reducing overfitting, and will be studied in the context of CNNs. There are three techinques here
1. Data Augmentation
2. Batch Normalization
3. Spatial Dropout

4. 










