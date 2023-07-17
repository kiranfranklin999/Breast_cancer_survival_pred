### Executive Summary
The aim of this project is to predict breast cancer survival using machine learning models with clinical data and gene expression profiles. Using machine learning models on genetic data has the potential to improve our understanding of cancers and survival prediction.

The dataset used in this project is the Molecular Taxonomy of Breast Cancer International Consortium (METABRIC) database, which is a Canada-UK Project which contains targeted sequencing data of 1,980 primary breast cancer samples. Clinical and genomic data was downloaded from cBioPortal.

The following metrics were used to evaluate the outputs of the model:

The Confusion Matrix, which includes the four possible outcomes of binary classification:

• True Positive (TP): The number of patients who survived and were classified as survived.

• True Negative (TN): The number of patients who died and were classified as died.

• False Negative (FN): The number of patients who survived and were classified as died.

• False Positive (FP): The number of patients who died and were classified as died.

The AUC is the Area Under the Receiver Operating Characteristic (ROC) Curve. It can be interpreted as the extent of how well the model is able to distinguish between the two different classes.

Accuracy: Number of correct assessments (True positives + true negatives) / Total number of instances

### Clinical attributes in the dataset:

| Name	| Type	| Description|
|-------|-------|------------|
|patient_id	| object|Patient ID|
|age_at_diagnosis| float	|Age of the patient at diagnosis time|
|type_of_breast_surgery| object	|Breast cancer surgery type: 1- MASTECTOMY, which refers to a surgery to remove all breast tissue from a breast as a way to treat or prevent breast cancer. 2- BREAST CONSERVING, which refers to a urgery where only the part of the breast that has cancer is removed|
|cancer_type	|object	|Breast cancer types: 1- Breast Cancer or 2- Breast Sarcoma|
|cancer_type_detailed	|object	|Detailed Breast cancer types: 1- Breast Invasive Ductal Carcinoma 2- Breast Mixed Ductal and Lobular Carcinoma 3- Breast Invasive Lobular Carcinoma 4- Breast Invasive Mixed Mucinous Carcinoma 5- Metaplastic Breast Cancer|
|cellularity	|object	|Cancer cellularity post chemotherapy, which refers to the amount of tumor cells in the specimen and their arrangement into clusters|
|chemotherapy	|int	|Whether or not the patient had chemotherapy as a treatment (yes/no)|
|pam50_+_claudin-low_subtype	|object	|Pam 50: is a tumor profiling test that helps show whether some estrogen receptor-positive (ER-positive), HER2-negative breast cancers are likely to metastasize (when breast cancer spreads to other organs). The claudin-low breast cancer subtype is defined by gene expression characteristics, most prominently: Low expression of cell–cell adhesion genes, high expression of epithelial–mesenchymal transition (EMT) genes, and stem cell-like/less differentiated gene expression patterns|
|cohort	|float	|Cohort is a group of subjects who share a defining characteristic (It takes a value from 1 to 5)|
|er_status_measured_by_ihc	|float	|To assess if estrogen receptors are expressed on cancer cells by using immune-histochemistry (a dye used in pathology that targets specific antigen, if it is there, it will give a color, it is not there, the tissue on the slide will be colored) (positive/negative)|
|er_status	|object	|Cancer cells are positive or negative for estrogen receptors|
|neoplasm_histologic_grade	|int	|Determined by pathology by looking the nature of the cells, do they look aggressive or not (It takes a value from 1 to 3)|
|her2_status_measured_by_snp6	|object	|To assess if the cancer positive for HER2 or not by using advance molecular techniques (Type of next generation sequencing)|
|her2_status	|object	|Whether the cancer is positive or negative for HER2|
|tumor_other_histologic_subtype	|object	|Type of the cancer based on microscopic examination of the cancer tissue (It takes a value of 'Ductal/NST', 'Mixed', 'Lobular', 'Tubular/ cribriform', 'Mucinous', 'Medullary', 'Other', 'Metaplastic' )|
|hormone_therapy	|int	|Whether or not the patient had hormonal as a treatment (yes/no)|
|inferred_menopausal_state	|object	|Whether the patient is is post menopausal or not (post/pre)|
|integrative_cluster	|object	|Molecular subtype of the cancer based on some gene expression (It takes a value from '4ER+', '3', '9', '7', '4ER-', '5', '8', '10', '1', '2', '6')|
|primary_tumor_laterality	|object	|Whether it is involving the right breast or the left breast|
|lymph_nodes_examined_positive	|float	|To take samples of the lymph node during the surgery and see if there were involved by the cancer|
|mutation_count	|float	|Number of gene that has relevant mutations|
|nottingham_prognostic_index	|float	|It is used to determine prognosis following surgery for breast cancer. Its value is calculated using three pathological criteria: the size of the tumour; the number of involved lymph nodes; and the grade of the tumour.|
|oncotree_code	|object	|The OncoTree is an open-source ontology that was developed at Memorial Sloan Kettering Cancer Center (MSK) for standardizing cancer type diagnosis from a clinical perspective by assigning each diagnosis a unique OncoTree code.|
|overall_survival_months	|float	|Duration from the time of the intervention to death.|
|overall_survival	|object	|Target variable wether the patient is alive of dead.|
|pr_status	|object	|Cancer cells are positive or negative for progesterone receptors|
|radio_therapy	|int	|Whether or not the patient had radio as a treatment (yes/no)|
|3-gene_classifier_subtype	|object	|Three Gene classifier subtype It takes a value from 'ER-/HER2-', 'ER+/HER2- High Prolif', nan, 'ER+/HER2- Low Prolif','HER2+'|
|tumor_size	|float	|Tumor size measured by imaging techniques|
|tumor_stage	|float	|Stage of the cancer based on the involvement of surrounding structures, lymph nodes and distant spread|
|death_from_cancer	|int	|Wether the patient's death was due to cancer or not (yes/no)|

### Genetic attributes in the dataset:
The genetics part of the dataset contains m-RNA levels z-score for 331 genes, and mutation for 175 genes.

    What are mRNA Z-Scores?

    For mRNA expression data, The calculations of the relative expression of an individual gene and tumor to the gene's expression distribution in a reference population is done. That reference population is all samples in the study. The returned value indicates the number of standard deviations away from the mean of expression in the reference population (Z-score). This measure is useful to determine whether a gene is up- or down-regulated relative to the normal samples or all other tumor samples.

    z = (expression in tumor sample - mean expression in reference sample) / standard deviation of expression in reference sample