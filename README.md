# Automated Data Creation
This repo is regarding Natural Language Processing project Automated Data Creation.

# Process

  - We will take some base images/ reference images from refcoco database. COCO database has referential images which will help us to further generate synthetic data.
  - We will also utilise [cocoapi](https://github.com/cocodataset/cocoapi) provided by refcoco org which will help us download data.
  - Once we have related data and api, we will start transformations on images as follows :
    - Exposure - These transformations will change exposure of images to light. This will mainly increase individual, non-color dependant dataset. There will be three main types of transformations :
        1. Contrast Stretching : Contrast Stretching takes the approach of analyzing the distribution of pixel densities in an image and then “rescales the image to include all intensities that fall within the 2nd and 98th percentiles.”
        2. Histogram Equalisation : Histogram Equalization increases contrast in images by detecting the distribution of pixel densities in an image and plotting these pixel densities on a histogram.
        3. Adaptive Equalisation : Adaptive Equalization differs from regular histogram equalization in that several different histograms are computed, each corresponding to a different section of the image; however, it has a tendency to over-amplify noise in otherwise uninteresting sections
    - Transpose -- These transformation doesn't change any inherit properties of images but changes their orientation. This kind of data help us understand context between objects and their properties.
        1. Horizonatal and Vertical Flip
        2. rotation by 45, 90, 135, 180 degrees
 - Once data is generated, we will focus on captions. As captions were already provided by refcoco data set, we will simply randomly select three captions and provide them to each image. 
 - Finally we will have a set of Synthetic image, masked objects in that image and it's captions.

### Installation
1. Step 1 would be to clone the repo.
2. Once you clone the repo, we suggest to create a python3 virtual env and install required prequisites.

```sh
$ python -m venv ./env
$ pip install -r requirements.txt
```
3. Move to cocoapi/PythonAPI folder and run make.
```
$ cd cocoapi/PythonAPI
$ make
```
4. PythonAPI folder has **Data_Creation.ipynb** file which will generate synthetic data. But before we do that, we need to do some changes :
        - **We need to make sure all paths are correctly marked**
        - **Cell 2 and cell7** has annotation path, pleas emake sure it's pointed correctly and **cell5, cell6, cell8, cell12** has dataCreate folder path.
5. Download necessary data files, you only need to download the [**annotations_trainval2014.zip**](http://images.cocodataset.org/annotations/annotations_trainval2014.zip) from refcoco database. We don't need image files as they will automatically be downloaded by cocoapi. To work properly place downloaded files in annotation folder.
6. Once everything set, you can run **Data_Creation.ipynb** file to generate desired dataset. Initially two sets of 100 images are taken, which will approximately create 2500+ images, but you can change values accordingly.

### Sample Data

Sample data on almost 200 images(synthetic images over 2500) can be downloded from [here](https://drive.google.com/drive/folders/1TNpqHUaYB024nfzxF_SlmG3dMGD_uCTU?usp=sharing). Data is divided by each image id folder which further contains multiple synthetically created images.

### Contribution/Tasks
I was assigned to generate synthetic data in a way that no mechanical or manual effort is used. To train a model that can detect not only objects but context as well, we need a very diverse and varied dataset. After discussing with TA, I decided to go with synthetic data creation from already existing data. This way there is already an established accuracy and correctness among dataset and a large amount of synthetic data could be generated with high confidence.
Other than that, limiting captions to 3 rather than all 5 helps to create cross validation and establishing relations between different class objects.

