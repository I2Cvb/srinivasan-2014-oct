Fully automated detection of diabetic macular edema and dry age-related macular degeneration from optical coherence tomography images
=====================================================================================================================================

[![DOI](https://zenodo.org/badge/16195/I2Cvb/srinivasan-2014-oct.svg)](https://zenodo.org/badge/latestdoi/16195/I2Cvb/srinivasan-2014-oct)

```
@article{srinivasan2014fully,
  title={Fully automated detection of diabetic macular edema and dry age-related macular degeneration from optical coherence tomography images},
  author={Srinivasan, Pratul P and Kim, Leo A and Mettu, Priyatham S and Cousins, Scott W and Comer, Grant M and Izatt, Joseph A and Farsiu, Sina},
  journal={Biomedical optics express},
  volume={5},
  number={10},
  pages={3568--3577},
  year={2014},
  publisher={Optical Society of America}
}
```

How to use the pipeline?
-------

### Pre-processing pipeline

The following pre-processing routines were applied:

- BM3D denoising,
- Flattening,
- Cropping.

#### Data variables

In the file `pipeline/feature-preprocessing/pipeline_preprocessing.m`, you need to set the following variables:

- `data_directory`: this directory contains the orignal SD-OCT volume. The format used was `.img`.
- `store_directory`: this directory corresponds to the place where the resulting data will be stored. The format used was `.mat`.

#### Algorithm variables

The variables which are not indicated in the inital publication and that can be changed are:

- `x_size`, `y_size`, `z_size`: the original size of the SD-OCT volume. It is needed to open `.img` file.
- `sigma`: the estimate of the standard deviation for the BM3D denoising.
- `h_over_rpe`, `h_under_rpe`, `width_crop`: the different variables driving the cropping. 

#### Run the pipeline

From the root directory, launch MATLAB and run:

```
>> run pipeline/feature-preprocessing/pipeline_preprocessing.m
```

### Extraction pipeline

The following features were extracted:

- HOG.

#### Data variables

In the file `pipeline/feature-extraction/pipeline_extraction.m`, you need to set the following variables:

- `data_directory`: this directory contains the pre-processed SD-OCT volume. The format used was `.mat`.
- `store_directory`: this directory corresponds to the place where the resulting data will be stored. The format used was `.mat`.

#### Run the pipeline

From the root directory, launch MATLAB and run:

```
>> run pipeline/feature-extraction/pipeline_extraction.m
```

### Classification pipeline

The method for classification used was:

- Linear SVM.

#### Data variables

In the file `pipeline/feature-classification/pipeline_classifier.m`, you need to set the following variables:

- `data_directory`: this directory contains the feature extracted from the SD-OCT volumes. The format used was `.mat`.
- `store_directory`: this directory corresponds to the place where the resulting data will be stored. The format used was `.mat`.
- `gt_file`: this is the file containing the label for each volume. You will have to make your own strategy.

#### Run the pipeline

From the root directory, launch MATLAB and run:

```
>> run pipeline/feature-classification/pipeline_classifier.m
```

### Validation pipeline

#### Data variables

In the file `pipeline/feature-validation/pipeline_validation.m`, you need to set the following variables:

- `data_directory`: this directory contains the classification results. The format used was `.mat`.
- `gt_file`: this is the file containing the label for each volume. You will have to make your own strategy.

#### Run the pipeline

From the root directory, launch MATLAB and run:

```
>> run pipeline/feature-validation/pipeline_validation.m
```
