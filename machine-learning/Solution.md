# Project Setup Guide

This guide will help you set up a Python virtual environment, install dependencies from `requirements.txt`, and configure it as the kernel for a Jupyter notebook.

## Prerequisites

- Python installed (preferably Python 3.6+)
- pip installed
- Jupyter Notebook installed

## Steps

### 1. Setting Up the Python Virtual Environment

1. Open Command Prompt.
2. Navigate to your project directory:
    ```sh
    cd /c:/.../Numida/machine-learning
    ```
3. Create a virtual environment:
    ```sh
    python -m venv venv
    ```
4. Activate the virtual environment:
    ```sh
    .\venv\Scripts\activate
    ```

### 2. Installing Dependencies

1. Ensure the virtual environment is activated.
2. Install the dependencies from `requirements.txt`:
    ```sh
    pip install -r requirements.txt
    ```

### 3. Setting Up the Jupyter Notebook Kernel

1. Ensure the virtual environment is activated.
2. Add the virtual environment as a Jupyter kernel:
    ```sh
    python -m ipykernel install --user --name=venv --display-name "Python (venv)"
    ```

### 4. Launching Jupyter Notebook

1. Ensure the virtual environment is activated.
2. Start Jupyter Notebook:
    ```sh
    jupyter notebook
    ```
3. In Jupyter Notebook, select the kernel named "Python (venv)" for your notebooks.

## Conclusion

You have successfully set up your Python virtual environment, installed the necessary dependencies, and configured it as the kernel for Jupyter Notebook. Happy coding!

## Project Overview

### Objective

The objective of this project is to develop a machine learning model to predict loan efficiency scores and normalized loan scores for a given dataset of loans.

### Critical Logic and Assumptions

1. **Target Variables**: 
    - `loan_performance_score`: This metric captures the relationship between the loan yield and the repayment duration. Loans that yield higher returns and are repaid sooner receive better scores. It essentially measures the efficiency of loan repayments.
    - `loan_efficiency_score`: This metric captures the relationship between loan scores and customer leverage. Customers with higher leverage on better-scoring loans are considered more valuable than those with lower leverage or poor loan scores. It measures the ability to maximize returns from trustworthy customers.

2. **Data Preprocessing**:
    - Handling missing values.
    - Encoding categorical variables using `pd.get_dummies`.
    - Normalizing numerical features.

3. **Model Training**:
    - Using `GradientBoostingRegressor` for training the models.
    - Splitting the data into training and testing sets.
    - Evaluating the models using metrics such as MAE, MSE, and R^2.

### Steps Applied

1. **Data Loading**: Load the dataset into a pandas DataFrame.
2. **Data Cleaning**: Handle missing values and outliers.
3. **Feature Engineering**: Create new features and encode categorical variables.
4. **Model Training**: Train the `GradientBoostingRegressor` models on the training data.
5. **Model Evaluation**: Evaluate the models using appropriate metrics.
6. **Prediction**: Make predictions on the test data and store the results.

### Feature Importance Analysis - Key Points and Intuition

#### Loan Efficiency Score Model - Feature Importances

- **payment_duration (0.676)**: The most critical feature. Shorter repayment periods significantly enhance loan efficiency. **!!NB: This will require weight optimization to find the appropriate balance for the business.**
- **yield_rate (0.117)**: Higher yield rates contribute positively to loan efficiency.
- **cash_yield_15_dpd (0.106)**: Reflects immediate returns from the loan.
- **customer_leverage (0.096)**: Measures the ratio of total recovered amounts to the total principal, indicating the trustworthiness of the customer.

#### Normalized Loan Score Model - Feature Importances

- **payment_duration (0.729)**: The most critical feature. Shorter repayment periods significantly enhance loan performance.
- **yield_rate (0.138)**: Higher yield rates contribute positively to loan performance.
- **cash_yield_15_dpd (0.125)**: Reflects immediate returns from the loan.

#### Intuition

- **Repayment Duration**: Shorter repayment periods are crucial for both models, indicating that loans repaid quickly are more efficient and perform better. **To be expected before weight adjustment**
- **Yield Rate**: Higher yield rates are beneficial, showing that loans with better returns are more efficient and perform better.
- **Immediate Returns**: The cash yield within 15 days past due is important, highlighting the significance of early returns on loan performance and efficiency.
- **Customer Leverage**: For the Loan Efficiency Score model, customer leverage is important, indicating that customers who repay more relative to their principal are more valuable.

These key features help in understanding the factors that drive loan efficiency and performance, aiding in better decision-making for loan approvals and management.

### Next Steps

As we move forward, there are several key areas where we can enhance our models and overall project. Here’s a breakdown of the next steps:

- **Hyperparameter Tuning**: While our initial models show promise, there’s room for improvement through hyperparameter tuning. This involves systematically adjusting the parameters of our models to find the optimal settings that yield the best performance. You can use techniques like Grid Search or Random Search, and libraries such as scikit-learn provide convenient tools for this purpose. By fine-tuning parameters like learning rate, number of estimators, and max depth, we can potentially achieve better accuracy and efficiency.

- **Additional Feature Engineering**: Our current feature set is a good start, but exploring additional features could further enhance model performance. Non-linear relationship may prove fruitful. 

- **Model Validation**: With additional data we can apply several different validation schemes to ensure the models perforamnce is generalizable. 

- **Documentation**: Comprehensive documentation is essential for the next engineer who takes over this project. As the model growws, a living document capturing the essence of the logic, and the architecture decicion log will be essential. LLM's can be leveraged to rapidly geenrate this code, with Human-in-the-loop optimization to ensure the validty of the documentation. 

