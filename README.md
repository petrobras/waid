[![Apache 2.0][apache-shield]][apache] 
[![CC BY 4.0][cc-by-shield]][cc-by]

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
- [Dataset](#dataset)
- [Jupyter Notebooks (Python)](#jupyter-notebooks-python)

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
All datasets comprise '*.csv* ' files whose values are expressed in Brazilian numeric format (i.e., the decimal symbol is a colon ',' and the separator is a semicolon ';').

## Acoustic amplitude image dataset

To load an acoustic amplitude image data from a given well (for example, Tatu-22), one can use the following Pandas command line:

```python 
bsc_data = pd.read_csv('tatu22_IMG.csv',
                        sep = ';',
                        decimal = ',',
                        ...)
```


## Basic logs dataset

To load a basic log data from a given well (for example, Tatu-22), one can use the following Pandas command line:

```python 
bsc_data = pd.read_csv('tatu22_BSC.csv',
                        sep = ';',
                        decimal = ',',
                        ...)
```

The chosen nomenclature is as follows:

* **for image data files:** <well_name>_AMP.csv (AMP stems from the amplitude of the acoustic signal acquired by the image-logging tool. The values inside the file express acoustic attenuation measures in *dB*)
* **for basic logging data files:** <well_name>_BSC.csv (BSC stems from the word *basic*). The basic curves present in all 8 wells are:
    * Caliper (CAL)
    * Gamma Ray (GR)
    * Bulk Density (DEN)
    * Neutron Porosity (NEU)
    * Sonic Compressional Slowness (DTC)
    * Sonic Shear Slowness (DTS)
    * Photoelectric Factor (PE)
    * NMR Total Porosity(nmrPhiT)
    * NMR Effective Porosity (nmrPhie)
    * NMR Permeability (nmrPerm)
    * NMR Free Fluid (nmrFF)
    * Shallow Formation Resistivity (RES10)
    * Deep Formation Resistivity (RES90)

This is the dataset ...

### Missing  values

Some isolated curve values, or even the entire DTS curve (Coala-21, Coala-88 and Coala-89), are missing in some of the wells. We encourage users to try Statistical and Machine Learning imputation techniques to imput missing values and missing curves.

# Jupyter Notebooks (Python) 

...
