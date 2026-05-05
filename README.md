# SB-Net

> **Implementation of the paper:** *"SB-Net: A Novel Spam Botnet Detection Scheme With Two-Stage Cascade Learner and Ensemble Feature Selection"* [DOI: 10.1109/OJCOMS.2025.3603425](https://doi.org/10.1109/OJCOMS.2025.3603425)
> 
> **SoftwareX paper:** *"SB-Net: Software for classifying botnet attacks to prevent comprehensive infection"* [DOI: 10.1016/j.softx.2026.102672](https://doi.org/10.1016/j.softx.2026.102672)

This repository is the **latest version** of the original [SB-Net project](https://github.com/IrsyadFikriansyah/SB-Net), featuring minor bug fixes, improved documentation, and enhanced code organization.

---

## 📋 Table of Contents

- [About](#-about)
- [Changes from Original](#-changes-from-original)
- [Prerequisites](#-prerequisites)
- [Environment Setup](#-environment-setup)
  - [Option 1: Using Conda (Recommended)](#option-1-using-conda-recommended)
  - [Option 2: Using pip/venv](#option-2-using-pipvenv)
- [Project Structure](#-project-structure)
- [Step-by-Step Guide](#-step-by-step-guide)
  - [Step 1: Prepare the Dataset](#step-1-prepare-the-dataset)
  - [Step 2: Data Sampling (Optional)](#step-2-data-sampling-optional)
  - [Step 3: Data Preprocessing](#step-3-data-preprocessing)
  - [Step 4: Data Splitting](#step-4-data-splitting)
  - [Step 5: Ensemble Feature Selection](#step-5-ensemble-feature-selection)
  - [Step 6: Cascade Learner Classification](#step-6-cascade-learner-classification)
  - [Step 7: Model Evaluation](#step-7-model-evaluation)
- [Quick Run](#-quick-run)
- [License](#-license)
- [Acknowledgements](#-acknowledgements)

---

## 📖 About

SB-Net is a spam botnet detection scheme that utilizes:
- **Two-Stage Cascade Learner**: A hierarchical classification approach for improved detection accuracy
- **Ensemble Feature Selection**: Combines multiple feature selection methods to identify the most relevant features for botnet detection

This implementation reproduces the methodology described in the original research paper and provides a framework for experimentation with botnet detection using network traffic data.

---

## 🔄 Changes from Original

This refactored version includes:
- Minor bug fixes and code improvements
- Enhanced documentation and clearer instructions
- Added Conda environment file (`environment.yml`) for easier setup
- Added data sampler scripts for optional dataset subsampling
- Improved code organization and comments

---

## 📦 Prerequisites

Before running this application, make sure you have the following installed:

- Python 3.8+ (Python 3.10 recommended)
- Jupyter Notebook or JupyterLab
- Conda (recommended) or pip

### Required Python Dependencies
- pandas
- numpy
- matplotlib
- scikit-learn (sklearn)
- imbalanced-learn (for SMOTE/RUS balancing)

---

## 🔧 Environment Setup

### Option 1: Using Conda (Recommended)

This project includes a Conda environment file for easy setup.

1. **Clone the repository:**
   ```bash
   git clone https://github.com/algof/SB-Net-refactor.git
   cd SB-Net-refactor
   ```

2. **Create the Conda environment:**
   ```bash
   conda env create -f environment.yml
   ```

3. **Activate the environment:**
   ```bash
   conda activate sbnet
   ```

4. **Verify the installation:**
   ```bash
   python -c "import pandas; import sklearn; print('All dependencies installed successfully!')"
   ```

### Option 2: Using pip/venv

If you prefer using pip with a virtual environment:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/SB-Net-refactor.git
   cd SB-Net-refactor
   ```

2. **Create a virtual environment:**
   ```bash
   # On Windows
   python -m venv venv
   venv\Scripts\activate

   # On Linux/macOS
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install pandas numpy matplotlib scikit-learn imbalanced-learn jupyter seaborn
   ```

4. **Verify the installation:**
   ```bash
   python -c "import pandas; import sklearn; print('All dependencies installed successfully!')"
   ```

---

## 📁 Project Structure

```
SB-Net-refactor/
├── Balancing/                         # Dataset balancing scripts
│   ├── SMOTE.ipynb                    # SMOTE oversampling
│   ├── RUS.ipynb                      # Random Under-Sampling
│   └── checking_depth_*.py            # Depth checking scripts
│
├── Datasets/
│   ├── CTU-13/                        # CTU-13 dataset folder
│   │   ├── 1/, 2/, 5/, 9/, 13/        # Scenario folders (raw data)
│   │   ├── data_maker_CTU_13.ipynb    # Preprocessing notebook
│   │   └── data_sampler_CTU_13.ipynb  # Optional data sampler
│   ├── NCC/                           # NCC dataset folder
│   │   ├── scenario_dataset_*/        # Scenario folders (raw data)
│   │   ├── data_maker_NCC.ipynb       # Preprocessing notebook
│   │   └── data_sampler_NCC.ipynb     # Optional data sampler
│   ├── NCC-2/                         # NCC-2 dataset folder
│   │   ├── sensor1/, sensor2/, sensor3/  # Sensor folders (raw data)
│   │   ├── data_maker_NCC_2.ipynb     # Preprocessing notebook
│   │   └── data_sampler_NCC_2.ipynb   # Optional data sampler
│   └── train_combiner.py              # Script to combine training files
│
├── graph/                             # Generated graphs and visualizations
│   └── *.py                           # Graph generation scripts
│
├── logs/                              # Output logs from experiments
│   ├── classification_results.log
│   ├── feature_n_results_*.log
│   └── final_classification_test_result_*.log
│
├── .gitignore                         # gitignore file
├── environment.yml                    # Conda environment file
├── borda_score.py                     # Borda score aggregation script
├── rank_aggregation.ipynb             # Ensemble feature selection notebook
├── train_train_test_maker.ipynb       # Train/test split notebook
├── looping_classification.py          # Cascade learner optimization
├── looping_features.py                # Feature count optimization
├── final_classification_test.py       # Final model evaluation
├── run_all.py                         # Script to run entire pipeline
├── co_run.sh                          # Shell script for Code Ocean
└── README.md                          # This file
```

---

## 🚀 Step-by-Step Guide

### Step 1: Prepare the Dataset

1. **Download the datasets:**
   - **CTU-13**: [CTU-13 Dataset: A Labeled Dataset with Botnet, Normal and Background traffic](https://www.stratosphereips.org/datasets-ctu13)
   - **NCC**: [NCC Dataset: Botnet Group Activity Dataset](https://doi.org/10.17632/4vftxh97m8.1)
   - **NCC-2**: [NCC-2 Dataset: Simultaneous Botnet Dataset](https://doi.org/10.17632/8dpt85jrhp.2)

2. **Place the datasets** into the `/Datasets/` folder following this structure:
   ```
   Datasets/
   ├── CTU-13/
   │   ├── 1/           # Scenario folders
   │   ├── 2/
   │   ├── 5/
   │   ├── 9/
   │   └── 13/
   ├── NCC/
   │   ├── scenario_dataset_1/
   │   ├── scenario_dataset_2/
   │   ├── scenario_dataset_5/
   │   ├── scenario_dataset_9/
   │   └── scenario_dataset_13/
   └── NCC-2/
       ├── sensor1/
       ├── sensor2/
       └── sensor3/
   ```

---

### Step 2: Data Sampling (Optional)

> **⚠️ Note:** This step is **optional**. Use data samplers only if you want to work with a subset of the data for faster experimentation or if you have limited computational resources.

> **💡 Info:** The sampled datasets are used in our [CodeOcean Capsule](https://codeocean.com/capsule/0040153) for reproducible experiments with reduced computation time.

If you want to use a sampled subset of the dataset:

1. **Run the sampler notebooks** for each dataset:
   ```bash
   # For CTU-13
   jupyter notebook Datasets/CTU-13/data_sampler_CTU_13.ipynb
   
   # For NCC
   jupyter notebook Datasets/NCC/data_sampler_NCC.ipynb
   
   # For NCC-2
   jupyter notebook Datasets/NCC-2/data_sampler_NCC_2.ipynb
   ```

2. **Configure the sampling parameters** within each notebook as needed (e.g., sample size, random seed)

3. **Execute the notebooks** to generate sampled datasets

> **💡 Tip:** If you skip this step and proceed with the full datasets, the processing will take longer but will use all available data for more comprehensive results.

---

### Step 3: Data Preprocessing

Run the Jupyter Notebook scripts to preprocess and generate train/test files for each dataset:

```bash
# For CTU-13
jupyter notebook Datasets/CTU-13/data_maker_CTU_13.ipynb

# For NCC
jupyter notebook Datasets/NCC/data_maker_NCC.ipynb

# For NCC-2
jupyter notebook Datasets/NCC-2/data_maker_NCC_2.ipynb
```

After running all three notebooks, combine all training files:

```bash
cd Datasets
python train_combiner.py
cd ..
```

---

### Step 4: Data Splitting

Execute the notebook to split `combined_train.csv` into training and testing datasets:

```bash
jupyter notebook train_train_test_maker.ipynb
```

This will create the final train and test splits ready for model training.

---

### Step 5: Ensemble Feature Selection

1. **Run the rank aggregation notebook** to perform ensemble feature selection using multiple methods:
   ```bash
   jupyter notebook rank_aggregation.ipynb
   ```

2. **Calculate Borda scores** to aggregate the feature rankings:
   ```bash
   python borda_score.py
   ```

The output will be a ranked list of features based on their importance across multiple selection methods.

---

### Step 6: Cascade Learner Classification

1. **Find the best algorithm combination** for the two-stage cascade classification:
   ```bash
   python looping_classification.py
   ```

2. **Determine the optimal number of features** based on classification performance:
   ```bash
   python looping_features.py
   ```

These scripts will output logs and results to the `/logs/` directory.

---

### Step 7: Model Evaluation

Run the final classification test to evaluate the model's performance on the prepared test data:

```bash
python final_classification_test.py
```

The results, including accuracy, precision, recall, F1-score, and confusion matrices, will be saved to the log files.

---

## ⚡ Quick Run

If you want to run the entire pipeline automatically (after setting up the datasets), you can use:

```bash
python run_all.py
```

This script will execute all steps in sequence, from data preprocessing to final evaluation.

---

## 📄 License

This project is for academic and research purposes. Please cite the original SB-Net paper if you use this implementation in your research.

---

## 🙏 Acknowledgements

- **Original SB-Net Implementation**: [IrsyadFikriansyah/SB-Net](https://github.com/IrsyadFikriansyah/SB-Net)
- **Research Paper**: *"SB-Net: A Novel Spam Botnet Detection Scheme With Two-Stage Cascade Learner and Ensemble Feature Selection"*
- All contributors to the original project and research

---

## 📧 Contact

For questions, issues, or contributions, please open an issue on this repository or contact the maintainers.
