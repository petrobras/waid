[![Apache 2.0][apache-shield]][apache] 
[![CC BY 4.0][cc-by-shield]][cc-by]

[apache]: https://opensource.org/licenses/Apache-2.0
[apache-shield]: https://img.shields.io/badge/License-Apache_2.0-blue.svg
[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

# Welcome to the WAID (Well Acoustic Image Dataset) project contributing guide

:+1: Thank you for taking the time to contribute to the WAID project! :+1:

We expect to receive various types of contributions from individuals, research institutions, startups, companies and oil operators partners.

In this guide we present how each of the expected contributions might be proposed.

# Table of Content

- [Welcome to the WAID (Well Acoustic Image Dataset) project contributing guide](#welcome-to-the-waid-well-acoustic-image-dataset-project-contributing-guide)
- [Table of Content](#table-of-content)
- [Getting started](#getting-started)
- [Asking questions](#asking-questions)
- [Before contributing](#before-contributing)
  - [Contribution levels](#contribution-levels)
  - [WAID repository structure](#waid-repository-structure)
  - [Using the notebooks](#using-the-notebooks)
- [Proposing contributions](#proposing-contributions)
  - [Citation](#citation)
  - [Bugs](#bugs)
  - [Documentation improvements](#documentation-improvements)
  - [Cosmetic improvements](#cosmetic-improvements)
  - [Other improvements](#other-improvements)
- [Backlog](#backlog)

# Getting started

The recommended first step is to read the project's [README](README.md) for an overview of what this repository contains.

# Asking questions

Please do not open issues to ask questions. Please use the Discussions section accessed through the link that appears in the top menu.

# Before contributing

Before you can contribute to this project, we require you read and agree to the following documents:

* [CODE OF CONDUCT](CODE_OF_CONDUCT.md);
* [CONTRIBUTOR LICENSE AGREEMENT](CONTRIBUTOR_LICENSE_AGREEMENT.md);
* This contributing guide.

It is also very important to know, participate and follow the discussions. Click on the Discussions link that appears in the top menu.

## Contribution levels

We expect to receive contributions at different levels, as shown in the figure below. Some examples for each level are:

* Basic: 
    * Identify and report any issues in the dataset.
* Intermediary:
    * Identify, report and fix bugs;
    * Suggest documentation improvements;
    * Suggest improvements in data exploratory stage: visualization, outliers and missing data handling etc.
* Advanced:
    * Improve existing models already proposed to solve known applications based on the dataset;
    * Suggest or develop new approaches for known applciations based on the dataset;
    * Suggest new applications or new models to improve data understanding and further explore the information potential stored in the dataset.

## WAID repository structure

The WAID repository contains three different parts:

* A set of matched CSV files containing acoustic amplitude log data and basic well logs for eight wells. The WAID Dataset is available inside the [dataset](dataset) folder, split in two subfolders: [image](dataset\img) and [basic](dataset\bsc).
* A set of Jupyter Notebooks to provide basic handling on the dataset, including a toy experiment using Deep Learnning models (based on Keras Tensorflow), is available inside the [notebooks](notebooks) folder.

## Using the notebooks

Before using any of the code or Jupyter notebooks available in this repository, we recommend you set up a Python Virtual Environment with the packages versions listed in the [requirements.txt](requirements.txt).

# Proposing contributions

For each type of expected contribution, there is a subsection below with specific instructions. The last subsection specifies additional requirements for contributions to be incorporated into this project.

## Citation

If you use any resource published in this repository, we ask that it be properly cited in your work. Click on the ***Cite this repository*** link on this repository landing page to access different citation formats supported by the GitHub citation feature.

## Bugs

Please open an **issue** to report any bug. If you've implemented a fix, please create a **pull request** on a branch called `bugs`.

## Documentation improvements

We believe that any part of the documentation for this project can be improved, including this guide. You can work on that and then create a **pull requests** on a branch called `documentation_improvements` directly.

## Cosmetic improvements

Changes that are cosmetic in nature and do not add anything substantial to the stability, functionality, or testability of the WAID project are also welcome. In this case, please create a **pull requests** on a branch called `cosmetic_improvements` directly.

## Other improvements

If you intend to work and propose a more significant improvement, please consult our [backlog](BACKLOG.md) first. If you have any questions about the best strategy for the WAID project, please contact us or start  new **discussions**. When your proposed improvement is ready, please create a **pull request** on a branch called `other_improvements`.

It is important to keep in mind that all source code is implemented according to the style guide established by [PEP 8](https://peps.python.org/pep-0008/). This is guaranteed with the use of the [Black formatter](https://github.com/psf/black) with default options. Therefore, while codes have lines up to 88 characters (Black formatter's default option), each line with docstring or comment must be up to 72 characters long as established in PEP 8.

# Backlog

The list of priority improvements for the WAID project that we intend to develop collaboratively with the community is detailed in the file [BACKLOG.md](BACKLOG.md).