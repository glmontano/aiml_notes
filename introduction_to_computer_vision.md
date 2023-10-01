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

## Data Augmentation

Consider an image of a cat with ears in a fixed orientation. A CNN with a particular filter learning off this image may deduce that such ears in the said orientation is the feature. However, a cat may have different orientations depending on whether it is standing or laying down, passing the orientations to the ears. The CNN learning off a single orientation will overfit on the training data, and may perform poorly on a set of testing data with cats in different orientations.

Data augmentation works by augmenting the original data set with rotations of existing data. Taking the example of a cat in a speicif orientation - one would rotate the same image, therefore changing the orientation and feeding it into the training process.

The rotation example about is only one form of data augmentation. Other augmentation techniques include

1. Geometric transformations - Randomly flipping, cropping rotating or translating
2. Mixing images - Combining different images. Two methods are `pixel averaging` qand `crop overlaying`
3. Color space transormations - Changing brightness and contrast, chaning RGB color channels, intesify any color
4. Random erasing - Deletes parts of the initial iamges thereby forcing the model to focus on the entire image rather than a portion of it. Inspiring by Dropout method of the ANN.
5. Kernel filters - Used to sharpen or blur images using filters.

One advantages of data augmentation is that htey can all be all mentioned techniques may be done simultaneously.

## Batch Normalization

Batch normalziation is a technique originally learnt that can also be applied to CNNs. To recall - Batch Normalization scales or normalizes a layer's output to a specific scale, and one where the variance of the output is small (take 1 in the case of the standard normal distribution).

In the case of CNNs, it is also used to deal with `internal covariate shift`, where the distribution of inputs differs in different layers. This can create issues in training, including convergence delays.

A concrete example may include data that originally has white pixels, though after changes in the distribution, lead to figures with orange pixels.

As originally tauught - Batch Normalization standardizes the activations of each input variable per mini-batch, which means that during the weight update, the assumptions made by the subsequent layer regarding the spread and distribution of inputs will not alter drastically. Under similar distributions - training is more efficient and faster.

Furthermore, BN provides a weak form of regularization (reducing overfitting). Since BN is performed on mini-batches - it adds noise to the data, which results in regularization.

## Spatial Dropout

As with BN - the concept of Dropout was covered where neurons in a layer a dropped according a dropout-ratio. In CCNs - dropping out pixels would not be as effective due to the connectivity or correlations between pixels within a small neighborhood. As such - an altered version of dropout - `spatial dropout` is used instead.

In `spatial dropout` the pixels/cells/results from a filter map are effectively dropped out by making those results zero. For example, say 8 filter maps exist with a dropout-ratio of 0.25. Then, 2 filter maps will be randomly dropped by making the results of those filter maps zero.

# 2.2 Introduction to Transfer Learning

Ideally - we want CCNS with

- low bias
- low variance
- positive modelling performance in recall, precision and F1-score

To achieve this we required - a large, diverse and high-quality "labeled" image dataset. Furthermore, high computational power to train deep convolutional neural networks for complex images.

This is a lot easier to spell out, then executre.

## The first problem

Obtaining a large and diverse image dataset may be difficult due to cost, rareness, privacy and so on. Data augmentation cannot always be used as training images need to be diverse, meaningful and of high quality.

# The second problem - The computational cost of training deep CNNS

There are large computational costs associated with training CNNs. Training requires both performance and minimal latency. Requirements may include using high-quality GPUs, cloud computing resources, and other ideas from accelerated computing hardware.

However, all of this is expensive to acquire and may not always be feasible for individual deep learning practitioners or algorithmin researchers.

## The solution - Transfer Learning

Transfer Learning is a way of achieving a solution. It using the parameteres from a high-quality model, and apply them to your task at hand, and fine-tuning the model for your requirements. This has the benefit of *transferring the knowledge* from an high quality model to the task at hand.


















