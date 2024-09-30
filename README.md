[![Apache 2.0][apache-shield]][apache] 
[![CC BY 4.0][cc-by-shield]][cc-by]

![logo_com_RD-3](https://github.com/user-attachments/assets/8e3bfead-a2a0-49a0-9fb2-e0243279dbcf)

[apache]: https://opensource.org/licenses/Apache-2.0
[apache-shield]: https://img.shields.io/badge/License-Apache_2.0-blue.svg
[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
  - [Motivation](#motivation)
  - [Strategy](#strategy)
  - [Ambition](#ambition)
  - [Contributions](#contributions)
  - [Licenses](#licenses)
- [Datasets](#datasets)
  - [Acoustic image logs dataset](#acoustic-image-logs-dataset)
  - [Basic logs dataset](#basic-logs-dataset)
- [Jupyter Notebooks (Python)](#jupyter-notebooks-python)
- [Published work using WAID data](#published-work-using-waid-data)

# Introduction

The “Wellbore Acoustic Image Database” (WAID) project is part of PETROBRAS' efforts to promote innovation worldwide in the Oil and Gas industry.

The WAID project belongs to the PETROBRAS' program called [Conexões para Inovação - Módulo Open Lab](https://tecnologia.petrobras.com.br/modulo-open-lab.html) and is available on the PETROBRAS' Reservoir GitLab repository.

## Motivation

The “Wellbore Acoustic Image Database” (WAID) aims to promote the development of applications based on Machine Learning, particularly Deep Learning, for automating tasks related to interpreting acoustic image logs representing the wellbore surface. Such solutions involve the segmentation of structures, filling of voids in the image, event detection and generation of new synthetic data, among others.

The WAID repository contains a [dataset](#dataset) composed of image data with associated conventional open-hole log data and a set of basic [jupyter notebooks](#jupyter-notebooks-python) for basic handling and early data exploration.

## Strategy

The “Wellbore Acoustic Image Database” project belongs to the PETROBRAS' program called [Conexões para Inovação - Módulo Open Lab](https://tecnologia.petrobras.com.br/modulo-open-lab.html). This is an ***open project*** composed of the following parts:
* A [dataset](#dataset) composed of acoustic image data from 7 wells with associated conventional open-hole logs;
* A set of scripts in [Jupyter Notebooks](#jupyter-notebooks-python) format in Python language for basic handling and visualization of this data.

Our strategy is to make these resources available to the global community and develop the WAID project collaboratively.

## Ambition

Acoustic image logs are a class of logging acquisition that allows the construction of wellbore images to bring rich and intuitive geological features for human experts to analyze. However, they are composed of very high-resolution measurements, bearing a considerably larger information content than conventional open-hole logs. For this reason, they demand a lot of time-consuming routines for petrophysicists to extract information from it.

This high information density feature of acoustic images makes them perfectly suitable to benefit from artificial intelligence-based techniques. Incorporating such techniques will allow petrophysical interpreters to speed up routine procedures, discover new applications, and extract more knowledge from this data source.

With this project, PETROBRAS intends to foster the incorporation of ML/IA techniques to speed up routine procedures but especially to foment:

* the development of new methods to improve classical applications such as identifying and discriminating geological structures (like fractures or vugs) from artifacts (like breakouts) and petrophysical parameter estimation;
* the development of new applications based on image logs;
* the discovery of new knowledge extracted from image logs.

## Contributions

We expect to receive various types of contributions from individuals, research institutions, startups, companies and partner oil operators.

Before you can contribute to this project, you need to read and agree to the following documents:

* [CODE OF CONDUCT](CODE_OF_CONDUCT.md);
* [CONTRIBUTOR LICENSE AGREEMENT](CONTRIBUTOR_LICENSE_AGREEMENT.md);
* [CONTRIBUTING GUIDE](CONTRIBUTING.md).

It is also very important to know, participate and follow the discussions. See the discussions section.

## Licenses

All the code of this project is licensed under the [Apache 2.0 License][apache] and all dataset data files (CSV files in the subdirectories of the [dataset](dataset) directory) are licensed under the [Creative Commons Attribution 4.0 International License][cc-by].

# Datasets

In its first release, WAID contains data from five wells in a Brazilian carbonate pre-salt reservoir. Their relative locations are shown below[^1]:

<img width="600" alt="waid_wells_location" src="https://github.com/user-attachments/assets/f44f3f87-2c27-44d1-af5e-90af4d923f69" title="Adapted from Frota et al., 2024.">

[^1]: Adapted from Frota et al., 2024 [Frota et al., 2024](https://doi.org/10.1109/IJCNN60899.2024.10650225) with permission of the authors.

The table below shows the wells identifiers and names:
Well ID|Well name  
:---:|:---:
A      |ANTILOPE-37
B      |TATU-22    
C      |BOTOROSA-47
D      |COALA-88   
E      |ANTILOPE-25

All datasets consist of '*.csv*' files whose values are expressed in Brazilian numeric format (i.e. the decimal symbol is a colon ',' and the separator is a semicolon ';').

## Acoustic image logs dataset

To load an acoustic amplitude image data from a given well (for example, TATU-22), one can use the following Pandas command line:

```python
import pandas as pd
 
bsc_data = pd.read_csv('tatu22_IMG.csv',
                        sep = ';',
                        decimal = ',',
                        ...)
```
Due to size restrictions in the image data files updated on GitHub, the original CSV files had to be split into many subfiles. We provide a Python function to solve this problem:

```python
import pandas as pd
import numpy as np
import os

def concat_IMG_data(well_id, data_path):
    # Due to file size limitations, the original AMP '.csv' file
    # has been split into several sub-files.
    # The concat_IMG_data() function aims to concatenate
    # them back into a single data object.
    #
    # concat_IMG_data() returns 'image_df', a Pandas dataframe
    # indexed by DEPTH information and whose columns are
    # the azimuthal coordinates of the AMP image log.
    
    # Name of the initial '00' file
    initial_file = well_id + "_AMP00.csv"

    # Read the the initial file to capture header information
    initial_file_path = os.path.join(data_path, initial_file)
    image_df = pd.read_csv(initial_file_path,sep = ';',
                           index_col=0,
                           na_values = -9999,na_filter = True,
                           decimal = ',',
                           skip_blank_lines = True).dropna()

    # Read and add data from the remaining files sequentially
    for file in os.listdir(data_path):
        if file.startswith(well_id) and file != initial_file:
            file_path = os.path.join(data_path, file)
            df_temp = pd.read_csv(file_path,sep = ';',
                                  header=None,index_col = 0,
                                  na_values = -9999, na_filter = True,
                                  decimal = ',', skip_blank_lines = True,
                                  dtype=np.float32
                                 ).dropna()
            
            # Adjust tem df's header to match image header
            df_temp.columns=image_df.columns
            
            # Concat dfs
            image_df = pd.concat([image_df, df_temp])
    return image_df
```

After defining ``img_data_path`` and ``well_identifier``, the above function returns the well image log data in a single Pandas dataframe, for example:

```python 
# Whole image data
img_data = concat_IMG_data(well_identifier,img_data_path)
```

## Basic logs dataset

To load a basic log data from a given well (for example, TATU-22), one can use the following Pandas command line:

```python
import pandas as pd

bsc_data = pd.read_csv('tatu22_BSC.csv',
                        sep = ';',
                        decimal = ',',
                        ...)
```

The chosen nomenclature is as follows:

* **for image data files:** <well_name>_AMP.csv (AMP comes from the amplitude of the acoustic signal captured by the imaging tool. The values in the file express acoustic attenuation measures in *dB*.)
* **for basic logging data files:** <well_name>_BSC.csv (BSC comes from the word *basic*). The basic curves present in the basic dataset are:
    * Caliper (CAL), unit: *in*.
    * Gamma Ray (GR), unit: *GAPI*.
    * Bulk Density (DEN), unit: *g/cc*.
    * Neutron Porosity (NEU), unit: *p.u.*.
    * Sonic Compressional Slowness (DTC), unit: *µs/ft*.
    * Sonic Shear Slowness (DTS), unit: *µs/ft*.
    * Photoelectric Factor (PE), unit: *barns/cc*
    * NMR Total Porosity(nmrPhiT), unit: *p.u.*.
    * NMR Effective Porosity (nmrPhie), unit: *p.u.*.
    * NMR Permeability (nmrPerm), unit: *mD*
    * NMR Free Fluid (nmrFF), unit: *p.u.*.
    * Shallow Formation Resistivity (RES10), unit: *Ω/m* (*Ohm/m*).
    * Deep Formation Resistivity (RES90), unit: *Ω/m* (*Ohm/m*).

It is important to highlight that the caliper log is often used as a data quality indicator.

### Missing  values

Some isolated curve values, or even the entire DTS curve (COALA-88), are missing in some of the wells. We encourage users to try Statistical and Machine Learning imputation techniques to imput missing values and missing curves.

# Jupyter Notebooks (Python) 

Two Jupyter notebooks, ``Plot_composite_logs.ipynb`` and ``Plot_segment_acoustic_image.ipynb``, are provided to illustrate the potential of the dataset:

* ``Plot_composite_logs.ipynb`` shows how to load the data and plot basic and image logs in a composite display at user defined depth intervals

<img width="500" alt="composite_logs" src="https://github.com/user-attachments/assets/748d63b7-7a6e-486f-8c34-2dd301b3180f">

* ``Plot_segment_acoustic_image.ipynb`` shows the basic handling of the image log data and an application for image segmentation based on amplitude value thresholds

<img width="500" alt="image_segmentation" src="https://github.com/user-attachments/assets/2a8f8144-8bb9-452d-9196-0f7e6c2ab28b">

# Published work using WAID data

In this section we aim to include an updated list of published papers (from journals or conferences) or other academic/technical works that have used data from this database

* Rewbenio A. Frota, Marley M. B. R. Vellasco, Guilherme A. Barreto and Candida M. de Jesus, "Heteroassociative Mapping with Self-Organizing Maps for Probabilistic Multi-output Prediction", 2024 International Joint Conference on Neural Networks (IJCNN), Yokohama, Japan, 2024, pp. 1-6, [DOI: 10.1109/IJCNN60899.2024.10650225](https://doi.org/10.1109/IJCNN60899.2024.10650225).
* Frota, Rewbenio A., Barreto, G.A., Vellasco, Marley M.B.R., de Jesus, Candida M. (2024). "New Cloth Unto an Old Garment: SOM for Regeneration Learning". In: Villmann, T., Kaden, M., Geweniger, T., Schleif, FM. (eds) Advances in Self-Organizing Maps, Learning Vector Quantization, Interpretable Machine Learning, and Beyond. WSOM+ 2024. Lecture Notes in Networks and Systems, vol 1087. Springer, Cham. [DOI: 10.1007/978-3-031-67159-3_1](https://doi.org/10.1007/978-3-031-67159-3_1)
