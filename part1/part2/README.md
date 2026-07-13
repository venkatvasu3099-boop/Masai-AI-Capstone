# Part 2: Supervised Machine Learning - Water pH Prediction

## Project Overview
This folder contains the Part 2 submission for the Applied AI & ML Essentials Capstone Project. The objective of this phase is to train a supervised machine learning model to predict the exact numeric pH level of a water sample based on its chemical attributes. 

## Dependencies
To run the modeling pipeline, you need Python and the following packages installed:
* pandas
* numpy
* scikit-learn
* joblib

You can install them via terminal:
`pip install pandas numpy scikit-learn joblib`

## Setup and Execution Instructions
1. Ensure the `processed_water_data.csv` file generated from Part 1 is in your working directory.
2. Run the machine learning script from your terminal:
`python part2_model.py`
3. Running the script will output the model training status, display evaluation metrics, and export a serialized model file named `water_ph_model.pkl`.

## Model Pipeline & Design Decisions
* **Feature Processing:** The engineered categorical feature `Hardness_Category` from Part 1 was converted into numerical format using One-Hot Encoding (`pd.get_dummies`) to make it readable for the algorithm. 
* **Data Splitting:** The dataset was split into an 80% training set and a 20% validation/testing set to properly evaluate generalisation performance.
* **Model Selection:** A **Random Forest Regressor** was selected for this task. Random Forests excel at capturing non-linear relationships and interactions between complex chemical features (like chloramines, sulfates, and organic carbon) without requiring intense feature scaling.
* **Evaluation Metrics:** Because predicting pH is a continuous regression task, the model was evaluated using:
  * **Mean Absolute Error (MAE):** Measures the average magnitude of absolute errors.
  * **Root Mean Squared Error (RMSE):** Punishes larger prediction errors more heavily.
