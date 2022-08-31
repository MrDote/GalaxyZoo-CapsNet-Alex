# GalaxyZoo_CapsNet

## Table of contents
* [Project Overview](#general-info)
* [Required Packages and Technologies](#technologies)
* [Data](#setup)
* [Files](#files)
* [Acknowledgments](#acknowledgments)

## Project Overview
This project investigated the relative abilities of a capsule network and residual network to reproduce the human classifications of galaxy images. This repository provides code that can process the required image data into the necessary data frame, train both models, evaluate their classification accuracies and test their abilities to reproduce well known physical results related to galaxy evolution.
	
## Required Packages and Technologies
The required packages for this project are:
* Pytorch
* CUDA
* Torchvision
* Sys
* SKimage
* SKlearn
* PIL
* Scipy
* Matplotlib
* Seaborn
* Numpy
* Pandas

This project also used 4 CPUs and 1 Tesla V100 GPU on the Lancaster University [High End Computing (HEC) Cluster](https://answers.lancaster.ac.uk/display/ISS/High+End+Computing+%28HEC%29+help).
	
## Data
All datasets used in this project can be downloaded from the following locations:

* The SDSS galaxy images and their corresponding labels used can be found on [Kaggle](https://www.kaggle.com/competitions/galaxy-zoo-the-galaxy-challenge/data) which provided 61578 RGB images in total. For access to the complete labelled dataset of SDSS galaxy images refer to the [Galaxy Zoo](https://data.galaxyzoo.org/).

* The higher resolution DECaLS galaxy images and their corresponding labels can be found on [Zenodo](https://zenodo.org/record/4196267#.YqiMJqHMLIU).

* The sample dataset of galaxy colours and total stellar mass was taken from [Schawinski et al. 2010b](https://cdsarc.cds.unistra.fr/viz-bin/cat/J/ApJ/711/284#/browse). For the complete dataset of galaxy colours refer to [MPA-JHU](https://www.sdss.org/dr12/spectro/galaxy_mpajhu/) and [NYU VAGC](http://sdss.physics.nyu.edu/vagc/) for the complete dataset of galaxy stellar masses.

* The galaxy Sersic indicies were downloaded from [Simard et al. 2011](https://cdsarc.cds.unistra.fr/viz-bin/cat/J/ApJS/196/11#/browse).



## Files
Describe files
```abc```

### CapsNet
The CapsNet folder contains 3 versions of the capsule network code: ```CapsNetReconstructor.py```, ```CapsNetRegressor.py``` and ```CapsNetPredictor.py```

```CapsNetRegressor.py``` is used to train the capsule network to predict the Galaxy Zoo vote fractions corresponding to an image. It accepts input date in the form of [Number of images, Number of colour channels, Image width, Image height] and matches each image in the tensor, by index, to the image label tensor [Number of images, Number of vote fractions]. The network uses an adam optimizer to minimize the mean squared error between the actual vote fractions and the network predicted fractions. The network will output the average value of the mean squared error across all image at each epoch as well as saving the trained set of weights to the EPOCH.NPY file.

The ```CapsNetPredictor.py``` allows you to load in the pre-trained weights from the EPCOH.NPY file to predict the vote fractions corresponding to a set of input images to the network. 

Note that ```CapsNetPredictor.py``` code failed to work when classifying 1 image with it outputting a 16-dimensional vector rather than the predicted array of vote fractions. However, it works fine when classifying more than one image.

```CapsNetReconstructor.py``` trains a capsule network to classify a galaxy image as either smooth and rounded, featured or an artefact using binary labels rather than vote fractions. Then using the trained weights reconstructs the images giving a visualisation of the features that the capsule network is able to detect and use to classify images. 

Note: if training or classifying RGB images change ‘in_channels = 3’, if using greyscale images set ‘in_channels =1’.


### DataAnalysis


### Dataloader
```Segmenter_Dataloader.py``` ```Dataloader.py```

### Miscellaneous


### ResNet
```ResNetRGB.py``` ```ResNetRGBPredict.py``` ```ResNetGrey.py``` ```ResNetGreyPredict.py``` 

## Acknowledgments
Project Acknowledgments
