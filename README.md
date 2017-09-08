# Semantic Segmentation
## Udacity Self-Driving Car Nanodegree. Term 3. Project 2

### Introduction
In this project, I've labeled the pixels of a road in images using a Fully Convolutional Network (FCN).

### Setup
##### Frameworks and Packages
Make sure you have the following is installed:
 - [Python 3](https://www.python.org/)
 - [TensorFlow](https://www.tensorflow.org/)
 - [NumPy](http://www.numpy.org/)
 - [SciPy](https://www.scipy.org/)
##### Dataset
Download the [Kitti Road dataset](http://www.cvlibs.net/datasets/kitti/eval_road.php) from [here](http://www.cvlibs.net/download.php?file=data_road.zip).  Extract the dataset in the `data` folder.  This will create the folder `data_road` with all the training a test images.
  
### Reflections  
This project solves one of the tasks from the perception subsystem of the Self-Driving Car - road semantic segmentation.  
Getting the images from the frontal camera, algorithm classify each pixel on the image as road or non-road.  
For this project I've used pretrained VGG-16 model, extended it to the fully convolutional model and Kitti Road Dataset.  
  
#### Model architecture
The model has the following high level architecture (Padding=same):  
Input: Image H W 3  
Block 1 out: H/2 W/2 64  
Block 2 out: H/4 W/4 128  
Block 3 out: H/8 W/8 256  
Block 4 out: H/16 W/16 512  
Block 5 out: H/32 W/32 512  
Block 6 conv1x1(k:1, s:1), out: H/32 W/32 4096  
Block 7 conv1x1(k:1, s:1), out: H/32 W/32 4096  
Block 8 conv1x1(k:1, s:1), out: H/32 W/32 2  
Block 9 deconv(k:4, s:2), out: H/16 W/16 2  
Block 10 input: Block 4, conv1x1(k:1, s:1), out: H/16 W/16 2  
Block 11 add(Block 9, Block 10), out: H/16 W/16 2  
Block 12 input: Block 3, conv1x1(k:1, s:1), out: H/8 W/8 2  
Block 13 add(Block 11, Block 12), out: H/8 W/8 2  
Block 14 deconv(k:16, s:8), out: H W 2  
  
#### Sample output
<p>
  <img src="/data/img.png">
</p>

#### Next steps
*  Implement Intersection over Union Metric (IOU)  
*  Apply different model optimization technique (fusion, optimizing for reference, precision reduction), keeping the appropriate quality   
*  Apply TensorBoard for visualization  
*  Consider data augmentation to improve the model accuracy  
*  Consider other datasets and Multiclass Classification  
*  Testing on the embedded device  