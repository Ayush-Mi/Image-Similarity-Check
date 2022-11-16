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

Model Architecture
![](https://github.com/Ayush-Mi/Image_Similarity_Scoring/blob/main/image/outer-model.png)

Model was trained for ten epochs with contrastive loss function and Adam optimizer
![](https://github.com/Ayush-Mi/Image_Similarity_Scoring/blob/main/image/Model_performance.png)

#### VGG16 Network

After passing the image through pretrained VGG16 network the feature vector of dimension (4096,) was taken from 'fc2' layers. The PCA analysis with 100 components was done on the generated featuresand later 2D T-SNE plot was used to see the distribution of images in dataset.

2D TSNE plot of 100 samples taken randomly from dataset
![](https://github.com/Ayush-Mi/Image_Similarity_Scoring/blob/main/image/Feature_Map.png)

Test Image | Pred 1 (0.693) | Pred 2 (0.656) | Pred 3 (0.652) | Pred 4 (0.649)
:---: | :---: | :---: | :---: | :---:
![](https://github.com/Ayush-Mi/Image_Similarity_Scoring/blob/main/image/test_image.png) | ![](https://github.com/Ayush-Mi/Image_Similarity_Scoring/blob/main/image/pred_1.png) | ![](https://github.com/Ayush-Mi/Image_Similarity_Scoring/blob/main/image/pred_2.png) | ![](https://github.com/Ayush-Mi/Image_Similarity_Scoring/blob/main/image/pred_3.png) | ![](https://github.com/Ayush-Mi/Image_Similarity_Scoring/blob/main/image/pred_4.png) 

As observed in the above results, the model is seems to be looking at the colour and shapes of objects in given image as feature, hence some fintuning on the data is required to generate better scores.

## Conclusion
For big data the solution can be implemented using PySpark which reduce the amount of time required to compare the fearure vector of given image.
