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











