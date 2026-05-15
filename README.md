# NLRP3 Inhibitor Prediction using Machine Learning

This repository contains a Python Jupyter Notebook implementing a machine
learning–based pipeline for predicting NLRP3 inhibitors using
RDKit-derived molecular descriptors.

\---

## 📌 Project Overview

* Molecular feature generation using **RDKit**
* Supervised machine learning models for activity prediction
* Focus on NLRP3 **inhibitor screening**

\---

## 🧪 Methodology

1. Descriptor Calculation  
**File:** `Script\_descriptor\_calcualation\_NLRP3.ipynb`

### Purpose

* Calculate **RDKit molecular descriptors** from SMILES strings
* Generate a descriptor matrix for NLRP3 datasets and external dataset
* Save descriptor names for **reproducibility**
* Prepare data for model training and prediction

### Key Steps

1. Load dataset containing SMILES
2. Generate RDKit descriptors
3. Handle invalid molecules
4. Save:

   * Descriptor DataFrame

### Output

* Descriptor matrix (`.csv`)
* Pickled descriptor names (`descriptor\_names.pkl`)
2. Model Training \& Feature Selection  
**File:** `Script\_training\_models\_NLRP3.ipynb`

### Purpose

* Perform **feature selection** using Boruta / RF
* Scale features using `StandardScaler`
* Train multiple ML classifiers
* Save trained models and preprocessing objects

### Machine Learning Models

* Random Forest (RF)
* K Neighbors Classifier(KNN)
* Support Vector Machine (SVM)
* Gradient Boosting (GB)
* AdaBoost (AB)

### Key Steps

1. Load descriptor dataset
2. Split data into train/test
3. Feature selection (Boruta)
4. Feature scaling
5. Model training \& evaluation
6. Save objects using `pickle` / `joblib`

### Output Files

* `selected\_features.pkl`
* `scaler.pkl`
* `model\_rf.pkl`
* `model\_svm.pkl`
* `model\_gb.pkl`
* (other trained models)

\---

3. External Compound Prediction  
**File:** `script\_external\_predictions\_NLRP3.ipynb`

### Purpose

* Predict NLRP3 activity for **external / novel compounds**
* Use **exact same descriptors, features, and scaling**
* Generate predictions from multiple models

\---

Prediction Workflow (Step-by-Step)

Step 1: Prepare External Dataset
Your input file must contain: SMILES

Step 2: Calculate Descriptors

* Use `Script\_descriptor\_calcualation\_NLRP3.ipynb`
* Ensure **same RDKit version** as training
* Output: descriptor DataFrame

Step 3: Load Saved Objects
import pickle
import joblib

with open("descriptor\_names.pkl", "rb") as f:
descriptor\_names = pickle.load(f)

with open("selected\_features.pkl", "rb") as f:
selected\_features = pickle.load(f)

scaler = joblib.load("scaler.pkl")
model\_rf = joblib.load("model\_rf.pkl")

Step 4: Preprocess External Data
X = df\_descriptors\[descriptor\_names]
X\_selected = X\[selected\_features]
X\_scaled = scaler.transform(X\_selected)

Step 5: Generate Predictions
df\_predictions = pd.DataFrame()

df\_predictions\["DT"] = dt\_model.predict(X\_scaled)
df\_predictions\["Dt\_prob"] = dt\_model.predict\_proba(X\_scaled)\[:,1]

Step 6: Save Prediction Results
df\_predictions.to\_csv("predictions\_external.csv", index=False)

\---

## 🛠️ Requirements

The notebook was developed using Python and requires the following libraries:

* Anaconda (24.11.0, 64-bit)
* Jupyter Notebook (6.4.6)
* Python ≥ 3.8
* RDKit  (2024.3.6)
* scikit-learn (1.5.2)
* pandas
* numpy
* Boruta (0.4.3)

### Install dependencies (recommended via conda):

```bash
conda install -c conda-forge rdkit scikit-learn pandas numpy matplotlib



