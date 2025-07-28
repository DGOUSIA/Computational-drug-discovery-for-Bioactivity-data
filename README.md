# Computational-drug-discovery-for-Bioactivity-data
# Aim of the Project:
To classify drug-like compounds based on their bioactivity (IC₅₀) against a viral protein target (e.g., SARS coronavirus 3C-like protease), by:

Labeling compounds as active or inactive

Computing Lipinski’s drug-likeness descriptors

Performing exploratory data analysis (EDA) and statistical testing

Enabling further use in QSAR modeling or lead optimization




# 📊 Dataset Used:
ChEMBL database (accessed via chembl_webresource_client)

Bioactivity data (specifically IC₅₀ values) against the SARS coronavirus 3C-like proteinase (CHEMBL3927)



#Output includes:

Compound identifiers (molecule_chembl_id)

Molecular structure in SMILES format (canonical_smiles)

IC₅₀ values (nM)



# Process Workflow Summary:

1. Retrieve Bioactivity Data
Queried the ChEMBL target for “coronavirus”

Selected target ID: CHEMBL613837 for SARS-CoV

Extracted IC₅₀ values and stored as a DataFrame



2. Preprocessing and Labeling
Dropped compounds with missing standard_value

Created a new column bioactivity_class:

Active: IC₅₀ < 1000 nM

Inactive: IC₅₀ > 10000 nM

Intermediate: 1000–10000 nM (later removed)



3. Lipinski’s Rule-of-Five Descriptor Calculation
Installed and used RDKit to compute:

MW (Molecular Weight)

LogP (Partition Coefficient)

NumHDonors (Hydrogen Bond Donors)

NumHAcceptors (Hydrogen Bond Acceptors)

Combined descriptors with activity data



4. Data Normalization & pIC₅₀ Calculation
Converted IC₅₀ values to pIC₅₀ using:

𝑝𝐼𝐶50= −log10 (𝐼𝐶50 𝑖𝑛 𝑀)
pIC50=−log 10
​
 (IC50 in M)
Filtered out intermediate class for binary classification



5. Exploratory Data Analysis (EDA)
Plotted:

Frequency count of active vs inactive

Scatterplot of MW vs LogP (color-coded by activity)

Boxplots for pIC₅₀, MW, LogP, NumHDonors, NumHAcceptors


# 6. Statistical Analysis
Applied Mann-Whitney U Test to assess whether the distribution of each descriptor differs between actives and inactives:

Significant difference found for:

pIC₅₀, MW, NumHDonors, NumHAcceptors

No significant difference for LogP


# 🛠 Functions Used and Their Purpose:
Function	Purpose
target.search()	Search proteins in ChEMBL
activity.filter()	Retrieve IC₅₀ bioactivity data
lipinski()	Calculate drug-likeness descriptors using RDKit
pIC50()	Convert IC₅₀ to pIC₅₀ (log scale for regression)
mannwhitney()	Perform non-parametric test between actives and inactives
sns.* (Seaborn)	Generate EDA plots (scatter, box, count)


# ✅ Results:
Preprocessed dataset of ~133 compounds with descriptors and pIC₅₀ values.

Clear classification of active vs. inactive compounds.

Visual and statistical evidence showing which chemical properties (descriptors) differ between active and inactive compounds.

Cleaned and labeled dataset saved for future ML modeling (e.g., QSAR or deep learning).



# 🚀 Future Scope / Extensions:
Train a classification model (e.g., SVM, Random Forest) to predict bioactivity from descriptors.

Apply QSAR modeling using the combined dataset.

Incorporate additional molecular descriptors or 3D features.

Expand to multiple targets for broader drug screening.

Use this approach in lead optimization pipelines or virtual screening.
