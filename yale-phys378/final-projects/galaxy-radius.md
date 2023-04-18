# Predicting Galaxy Radius with ML

## Objective
Develop a machine learning framework that can predict how large a galaxy is from its image.

## Background 
The radius of a galaxy is an important intrinsic physical property of a galaxy. Astronomers have mostly used light-profile fitting techniques (fitting a 2D model to the image of a galaxy) to determine the radius of galaxies in the past. However, these techniques cannot be scaled to the data-volumes expected in astronomy over the next decade. Therefore, it’s important to develop ML-based frameworks that can determine the radius of galaxies.

## Data
The data for this problem consists of galaxies simulated to match galaxies imaged using the [Hyper Suprime-Cam Survey](https://hsc.mtk.nao.ac.jp/ssp/). We will be using simulated galaxies for this problem as we know the robust ground truth for these, and thus we can verify the efficacy of the models that you develope effectively. 

The data consists of 40,000 images; and the ground truth parameters for every image.

* `/images/` (obtained by expanding images.tar.gz)--> This folder contains all the 40,000 images. The images are in the [FITS](https://en.wikipedia.org/wiki/FITS) format -- an extermely popular format for astronomical images. 
* `gal_morph_train_val.csv` --> Ground Truth parameters for images in the training and validation sets. Its upto you what fraction to use for training/validation
* `gal_morph_test.csv` --> Ground Truth parameters for images in the test set. No part of this dataset may be used in any way before the final testing phase. 

In both the csv files above, the following columns will be of interest to you:-
* `file_name` --> Filename in /images/ for the correspinding image
* `bt` --> Bulge-to-Total Light Ratio for the Galaxy
* `R_e `--> Radius of the Galaxy (in arcseconds)
* `total_flux` --> Flux of the galaxy (in ADUs) 

### Prediction Variable
The goal of this problem is to develop an ML framework that can predict the radius of galaxies. 

### How to Get the Data
Using Linux/MacOS Command Line, first navigate to the location where you want to download the data. Then type in the following commands
```bash
ftp ftp.astro.yale.edu
cd pub/aghosh/phys_378_projects/gal_morph/
get *.csv
get *.tar.gz
```

If you are using Windows, or if the above method fails, use your browser to navigate to 
```
ftp://ftp.astro.yale.edu/pub/aghosh/phys_378_projects/gal_morph/
```
Connect as guest if a prompt appears. Now download all the files 

*After downloading the files, expand the `images.tar.gz` tarball to obtain the images folder with all the images.* To expand the tarball, use the following command on unix
```
tar –xvzf images.tar.gz
```
## Suggestions
0. If you are doing this on a personal laptop or a desktop, the first thing to do is to install [Anaconda](https://www.anaconda.com/) to create an isolated coding environment for your project. Once you have installed anaconda you can create a new environment for your project and install some dependencies using
```bash
conda create -n phys378_project python=3.7
```
This will create a conda environment called `phys378_project` on your computer and isolate it from other work you might be doing on it. 
Then activate this environment using 
```bash
conda activate phys378_project
```
To install dependecies in this environment, use 
```bash
pip install fitsdataset
pip install tqdm
```
Once you are finish coding, do
```
conda deactivate phys378_project
```
Note that the next time you want to work on your project, you have to activate this environment again. 

1. **Use [this demo notebook](https://github.com/aritraghsh09/class-materials/blob/main/yale-phys378/final-projects/experiments/fits_data_loading.ipynb) to see an example of how to load fits images as a PyTorch dataset**

2. To read in individual fits files, use the [astropy.io.fits](https://docs.astropy.org/en/stable/io/fits/index.html) module.
```python
from astropy.io import fits
data = fits.getdata("/path/to/image/1.fits")
```
  data will be an Numpy array. 

3. The images are 239 pixels X 239 pixels. However, in order to make it easier for your models to train on them (reduce training time,space etc.), you can crop all the images to 143 pixels X 143 pixels

4. While discussing your results, try to check if the accuracy of your radius prediction is dependant on some of the other galaxy parameters referred to above. 


