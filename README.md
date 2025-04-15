# Understanding Brain Health - International Challenge

## Information
This project focuses on brain health, using machine learning and data visualization to analyze psychological assessments as well as classify and interpret medical images for Alzheimer’s research. We work with an open-source brain scan dataset ADNI from our international partnership with NYU School of Medicine, gaining hands-on experience in image classification and explainable AI.

### Description of the disease
As we age, some cognitive decline is normal, but conditions like mild cognitive impairment (MCI) and Alzheimer’s disease (AD) cause more severe dysfunction. Alzheimer’s is the most common form of dementia, affecting over 55 million people worldwide and ranking among the leading causes of death. In its advanced stages, AD strips individuals of memory, independence, and the ability to interact, often requiring full-time care. In this project, we analyze brain scans, cognitive tests, and lab data from healthy individuals, MCI patients, and AD patients. Our goal is to explore how data science can help detect, predict, and monitor brain health to support early diagnosis and intervention.

### Dataset
The ADNI data set contains of two main "types" of data:
1) Tabular data that contains information about the patient (age, gender, profession, medical history etc.) and patients' responses to some tests that assess their cognitive abilities.
2) Imaging data from MRI or other medical scanners.

In 2010, ADNI contained a total of 819 subjects (229 normal control subjects, 398 subjects with mild cognitive impairment (MCI), and 192 subjects with mild Alzheimer's disease (AD). Since then, the database grew much larger, and these numbers grow as more institutions join the effort and upload their datasets into the collection.

### Tasks

#### Task 1: Discovering Relationships in Tabular Data
Create an interactive visualization and explore the six provided tables to understand their content — one holds demographic data, the others cover cognitive tests (PRDEMOG, CDR, GDSCALE, MMSE, MoCA, NEUROBAT). Use unsupervised machine learning (e.g., clustering) to explore patterns: do tests like MoCA, MMSE, CDR, and NEUROBAT agree? Examine correlations with demographics, diagnostic outcomes, and depression (GDSCALE), and test significance using t-tests and ANOVA.

#### Task 2: Making Sense of the Imaging Data
Review the available image scans and verify correct class and gender assignments using the overview sheet. Explore the dataset (subjects, groups, visits, age, gender, image formats) and extract relevant 2D slices for analysis. Build clean, balanced datasets and run several deep learning experiments (binary and optionally multi-class) to classify healthy vs. unhealthy brains, varying slices, models, and dataset balance. Use explainable AI (e.g., grad-CAM, SHAP, LRP) to visualize model decisions.

#### Task 3: Connecting the Findings from Imaging and Tabular Data
Filter the tabular data to match the imaging dataset and link both for exploratory, correlation-driven analysis. Identify measures that strongly relate to AD diagnosis and spot patterns or anomalies across patient groups. Discuss and document your findings with the international collaborator.

## Project Structure
```
├── application                     - holds the final application
├── data                            - contains raw, transformed and processed data
│   └── external               
│   └── interim
│   └── processed
│   └── raw
│     └── miniset                   - contains a small sample dataset for test purposes
├── models                          - contains serialized models
├── notebooks                       - contains jupyter notebooks 
│   ├── 0_eda
│   └── 1_preprocessing
│   └── 2_modelling
│   └── 3_evaluation
│   └── 4_visualizations
│   └── 5_miscellaneous
├── reports                         - contains figures and texts for the final report
│   └── figures
└── scripts                         - contains python scripts (including helper functions)
│   └── helpers
└── CONFIG.yml                      - config file to ajust parameters that are used over multiple scripts
└── README.md
└── requirements.txt

```

## Setup

### Flattening the data structure
The image data is extremely nested and thus inconvenient to handle. The information of the names of the subfolders
are contained in the filename itself, which renders the subfolders unnecessary.

We have written some functions to flatten the data structure:
1. Make sure the raw data is in the project folder `data/raw/data`
2. Run the notebook `notebooks/5_miscellaneous/data_extraction.ipynb`. Make sure to uncomment the line
`# copy_to_flat()` in the last cell. 

Note that this creates a copy of the data. Additional space on disk is required. After that one can theoretically disperse of the raw, nested data.

### Get train- and test set annotations
We provide functionality to split the data into a train and into testset by creating two CSV-files:
`test_labels.csv` and `train_labels.csv` in the `data/annotations`-folder. 
To create the split (always stratified) with the proportions you desire, run the `notebooks/1_preprocessing/Train_Test_Splitter.ipynb`-notebook.

You can adapt the split in the following way:
 - "proportion": This argument defines the proportion of data in the trainset (therefore has to be between 0 and 1)
 - "group_identifier": A column in the input dataframe. Allows us to split the data based on the values of a column
 - "save_files": If true, the above mentioned csv-files will be created. If false, the test- and trainset dataframe will be returned.
