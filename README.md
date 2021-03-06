# GPU-FV: Realtime Fisher Vector using GPUs

## Install 
1. Prerequesites:
-- a CUDA compatible GPU.
-- OpenCV installed.

2. Unzip armadillo. Then compile libpca and armadillo in local directories properly.

3. To compile GPU-FV code, first edit the following lines in Makefile according to  your own configuration.
Usually you do not have to modify ARMADILLO_ROOT and PCA_ROOT, since they are included in the package.

CUDA_ROOT = /usr/local/cuda
OPENCV_ROOT = ../opencv-2.4.9
ARMADILLO_ROOT = ./armadillo-4.650.2
PCA_ROOT = ./libpca-1.2.11

Then, just type 
$make

An executable file gpu_fv will be generated.

4. The main() function includes both training of GMM and encoding+classification for the Caltech256 dataset. 

The Caltech256 dataset can be downloaded from http://www.vision.caltech.edu/Image_Datasets/Caltech256/

To train a GMM, do

$./gpu_fv 0 $your_path_to_caltech256_dataset

, where $your_path_to_caltech256_dataset is the location of the 256 image sets in Caltech 256.

For example, if the dataset is in /home/tom, then this argument is specified as
"/home/tom/caltech256/256_ObjectCategories".

Then the projection parameters for pca after the dense sift process are stored in the file "center",
and the GMM components are stored in the file "cluster".

To encode and classify the images in Caltech256, do
$./gpu_fv 1 $your_path_to_caltech256_dataset

5. If you want to save the Fisher vectors of the images, you can define SAVE_CODE in main.cpp or in the Makefile.
Then make a directory called "C_output", the vectors will be saved there.


Fisher vectors of images in the training set have name R*, where * is the index in the training set.
Those in the testing set are named as E*, where * is the index in the testing set.

## References

GPU-FV: Realtime Fisher Vector and Its Applications in Video Monitoring   
Wenying Ma, Liangliang Cao, Lei Yu, Guoping Long, Yucheng Li  
ICMR 2016. [(arXiv)](http://arxiv.org/abs/1604.03498)
