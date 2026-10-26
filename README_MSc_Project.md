# COVID-19 Case Analysis and Regression Modelling (MSc Project)

## Project overview
This project uses COVID-19 surveillance data to explore reported case indicators and compare regression models for estimating **total confirmed cases** (`ConfirmedTotal`). The notebook includes data preparation, descriptive analysis, visualization, multicollinearity checks, and model evaluation.

The work is intended as an MSc research analysis. The notebook's outputs should be interpreted in the context of the data definitions, preprocessing decisions, and limitations described below.

## Research objective
To investigate how COVID-19 indicators—such as weekly confirmed cases, recoveries, deaths, testing activity, and active cases—relate to cumulative confirmed cases, and to compare the performance of:
- Linear Regression
- Ridge Regression
- Lasso Regression
- Elastic Net Regression

## Repository contents
Place the following files in the project directory:

```text
project-folder/
├── OEJ_External_Final_2_Commented.ipynb
├── COVID_19(JAN21_FEB23).xlsx
└── README.md
```

The Excel dataset is an input file and is not included in this README. Make sure you have permission to redistribute it before committing it to a public repository.

## Data
The notebook expects the source workbook named:

`COVID_19(JAN21_FEB23).xlsx`

The analysis references fields including:
- `DateReported` and `State` — observation identifiers
- `ConfirmedTotal` — target variable
- `ComfirmedLastWeek` — weekly confirmed cases (source spelling preserved)
- `RecoveriesTotal`, `RecoveriesLastWeek`
- `DeathTotal`, `DeathLastWeek`
- `ActiveCases`
- `TestingTotal`, `TestingLastWeek`

Confirm all field names and meanings against the original dataset documentation before using the results in a dissertation.

## Methods
1. **Data loading:** Read the Excel workbook into pandas.
2. **Normalization:** Apply Min-Max scaling to numeric columns while preserving the date/state identifiers.
3. **Missing-data handling:** Replace placeholder `?` values with missing values and impute selected fields with zero.
4. **Exploratory analysis:** Generate descriptive statistics, distribution plots, correlation matrices, and scatterplots.
5. **Multicollinearity assessment:** Calculate correlations and Variance Inflation Factor (VIF); also examine a reduced predictor set.
6. **Model development:** Split the observations into training and test subsets.
7. **Evaluation:** Compare in-sample and test-set Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and R-squared where included.

## Software requirements
Recommended Python environment: Python 3.10 or newer.

Install the principal packages with:

```bash
python -m pip install pandas numpy matplotlib seaborn scikit-learn statsmodels openpyxl jupyter
```

`openpyxl` is required by pandas to read `.xlsx` files.

## Running the notebook
1. Download or clone this project.
2. Place `COVID_19(JAN21_FEB23).xlsx` in the same directory as the notebook.
3. Create and activate a virtual environment if desired.
4. Install the dependencies listed above.
5. Start Jupyter:

   ```bash
   jupyter notebook
   ```

   Or open the `.ipynb` file in Visual Studio Code and select a Python kernel.
6. Run the notebook from top to bottom so that variables and data frames are created in the required order.

## Interpretation and research limitations
- **Association is not causation.** Regression coefficients and correlations do not establish causal relationships.
- **Potential target leakage / structural dependence:** cumulative case counts may be closely related to other cumulative or contemporaneous variables. Predictors should be justified for the stated research objective.
- **Normalization before splitting:** the notebook currently fits the scaler using the full dataset before the train/test split. This can introduce information from the test set into preprocessing. For a rigorous predictive workflow, fit preprocessing only on the training data (preferably using a scikit-learn `Pipeline`).
- **Zero imputation:** replacing missing values with zero assumes that missing or placeholder values represent zero. Validate this assumption using the data source's documentation; consider a more suitable imputation strategy where needed.
- **Random splitting:** if observations are time-ordered, a random train/test split may not evaluate future forecasting realistically. A chronological split is generally more appropriate for time-series forecasting.
- **Repeated analyses:** several notebook sections repeat model evaluation with different feature sets or metrics. Keep the experimental setup explicit when comparing results.
- **Data provenance:** cite the dataset provider and access date in the dissertation and repository once verified.

## Outputs
The notebook saves plots as image files (for example, distribution plots, correlation plots, and model comparison charts) in the current working directory. Some plots are displayed inline as well.

## Reproducibility
The notebook uses fixed `random_state` values in several model and split operations. Results can still vary with changes to package versions, source data, or notebook execution order.

## Author and citation
**Author:** [Your Name]  
**Degree/Programme:** MSc [Programme Name]  
**Institution:** [Institution Name]  
**Project title:** [Insert approved MSc project title]

If this work or its dataset is used in a publication or dissertation, cite the original data source and describe the preprocessing and evaluation choices.

## License
No license is specified. Add a license only if you have the right to distribute the code and any included data.
