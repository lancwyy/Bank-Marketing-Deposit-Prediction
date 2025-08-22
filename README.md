# Bank Marketing Dataset - Term Deposit Prediction

## Project Overview
This project analyzes the Bank Marketing dataset to explore customer behavior and predict whether a client will subscribe to a term deposit. The main focus is on exploratory data analysis (EDA) to uncover patterns and insights that can inform predictive modeling. This project is the first one of the series.

## Dataset Description
- **Source:** [Kaggle Bank Marketing Dataset](https://www.kaggle.com/datasets/janiobachmann/bank-marketing-dataset/data)
- **File:** [data/raw/bank.csv](data/raw/bank.csv)
- **Description:** The dataset contains information about direct marketing campaigns (phone calls) of a Portuguese banking institution. Features include client attributes (age, job, marital status, etc.), campaign details, and the target variable (`y`), indicating if the client subscribed to a term deposit.
- For more details, see [data/raw/bank_description.md](data/raw/bank_description.md).

## EDA Notebook
- **Location:** [notebooks/Bank_Marketing_Pandas.ipynb](notebooks/Bank_Marketing_Pandas.ipynb)
- **Contents:**
  - Data loading and quality check
  - Exploratory visualizations
  - Feature analysis and summary statistics
  - Insights into factors affecting deposit subscription

## How to Run
1. **Requirements:**
    - Install Prerequisites: Make sure you have Visual Studio Code and Python installed.
    - Install VS Code Extension: Open VS Code and install the Jupyter extension from the Extensions Marketplace.
    - Clone the Repository: Clone this project to your local machine.
        - `git clone https://github.com/lancwyy/Bank-Marketing-Deposit-Prediction.git`
        - `cd 'your-project-folder'`
2. **Setup:**
	- Create the Environment: Open the VS Code terminal (Ctrl + ~) and run:<br>
    `conda env create -f environment.yml`
    - Activate the Environment:
    `conda activate <environment-name>`
    - Open the Notebook: In VS Code, open the notebook file (.ipynb).
    - Select the Kernel: In the top-right corner of the notebook window, click on the kernel selector and choose the environment you just created. 
    - The notebook is now ready to run.
## Directory Structure
```
├── data/
│   └── raw/
│       ├── bank.csv
│       └── bank_description.md   
├── notebooks/
│   └── Bank_Marketing_Pandas.ipynb
└── results/
    └── EDA Report.md
```

## Results
- EDA summary and key findings are documented in [results/EDA Report.md](results/EDA%20Report.md).

## License
- Project License: See [LICENSE](LICENSE)
