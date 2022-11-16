# Image Similarity Check

## Description
This repo is about detecting diplicates or similar image in a database of images given a test image. It also touches upon the traditional Siamese network used for detecting similar images.

## Method
Here the similarity scoring method has been divided into two different approches. In the first approach I have built a siamese network with resnet architecture having 4 residual blocks. It uses Euclidean distance as distance metrics to compare two images given. In the second approach I have used a VGG16 model pretrained on imagenet data from keras API to generate feature vector for images. These feature vectors are stored as pickle file and is used to calculate cosine distance between the given test images and all the other images stored in database.

The first approach is ideal if we are working on small set of data but it will take a lot of time to compare with each image if number of images are large. This problem is solved by using the second approach where the feature vector of known images are already extracted and stored as pickle file. The new image only has perform the distance calculation between the stored features and the test image feature.

The inference time for second method can be further reduced by performing PCA in the generated feature and using that for distance calculation. The backend NN model can also be finetuned/retrained to increase the accuracy.

## Dataset
A subset from the [CVPR Indoor Scene Classification](https://web.mit.edu/torralba/www/indoor.html) was used which had images only from Grocery, Gym, Bookstore and Kitchen classes. 

For the Siamese network, the augmented image using Keras Imagedatagen API was used as similar image pair whereas the shuffled image were used for dissimlar image pairs. 

## Dependencies
All the required dependencies can be installed using requirement.txt

## Results

#### Siamese Network

#### VGG16 Network

## Conclusion
For big data the solution can be implemented using PySpark which reduce the amount of time required to compare the fearure vector of given image.
