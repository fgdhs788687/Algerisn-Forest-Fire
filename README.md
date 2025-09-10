# Algerian Forest Fires FWI Prediction Project
This project focuses on predicting the Fire Weather Index (FWI) for Algerian forest fires. It includes data preprocessing, exploratory data analysis (EDA), 
and machine learning model training. The final model is deployed via a Flask web application that allows users to input data and receive FWI predictions.

# 📂 File Structure
- Algerian_Forest_Fires_eda_and_fe.ipynb: Jupyter notebook for data cleaning, EDA, and feature engineering.
- model_training.ipynb: Jupyter notebook for model selection, training, and saving the final model and scaler.
- ridge_regression.pkl: A serialized file containing the trained Ridge Regression model.
- scaler.pkl: A serialized file containing the fitted StandardScaler object for data preprocessing.
- applicationn.py: The main Flask application that serves the prediction model.
- application_prototype.py: An alternative Flask application prototype for the model.
- index.html: The home page template for the Flask application.
- advance_home.html: The prediction page template for the main Flask application.
- indexproto.html: A placeholder HTML file used by the prototype application.
- home.html: A basic prediction page template.

# 📈 Data Preprocessing and EDA
The initial dataset, 
Algerian_forest_fires_dataset_UPDATE.csv , contained 246 entries and 14 columns. The data was divided into two regions: "Bejaia Region Dataset" and 
"Sidi-Bel Abbes Region Dataset".
The following steps were taken to clean and prepare the data:
- A new column, Region, was created to distinguish between the two datasets.
- Missing values were removed from the dataset.
- A problematic header row was dropped to ensure consistent data.
- Spaces in column names were removed.
- The day, month, year, Temperature, RH, and Ws columns were converted to integer data types.
- Columns from Rain to FWI were converted to float data types, excluding Classes.
- The Classes column was cleaned to have only two unique values: 'fire' and 'not fire'.
- The Classes column was encoded numerically, with 'not fire' as 0 and 'fire' as 1.
Exploratory data analysis revealed that August (Month 8) was the hotspot for fires in both the Bejaia and Sidi-Bel Abbes regions.

# 🤖 Model Training
This project utilizes several linear regression models to predict the FWI. The key steps in model training were:
1. Feature Selection: Highly correlated independent features (BUI and DC) were identified and removed to prevent multicollinearity.
2. Data Scaling: The remaining features were standardized using StandardScaler to ensure they had a mean of 0 and a standard deviation of 1.
3. Model Selection: The following models were trained and evaluated:
  - Linear Regression
  - Lasso Regression and LassoCV
  - Ridge Regression and RidgeCV
  - ElasticNet Regression and ElasticNetCV
4. Performance: The Ridge Regression model, which was cross-validated, achieved a high R² score of 0.9843 with a low Mean Absolute Error (MAE) of 0.5642, making it the most suitable model for this application.

The trained Ridge model and StandardScaler were saved as pickle files (ridge_regression.pkl and scaler.pkl) for future use.

# 🌐 Web Application
The Flask application (applicationn.py) serves as the front end for the machine learning model. It includes:
  - An entry point (/) to render a welcome page (index.html).
  - A prediction page (/fwi_prediction) to render a form (advance_home.html) for user input.
  - A prediction endpoint (/predictdata) that receives user data, preprocesses it using the StandardScaler, and then uses the Ridge model to make a Fire Weather Index (FWI) prediction.
    
# 🔧 Installation and Usage
To set up and run this project, you will need the following dependencies. You can install them using the following command:
pip install -r requirements.txt
The requirements.txt file should contain:
  - pandas
  - numpy
  - scikit-learn
  - flask
  - matplotlib
  - seaborn


To start the web application, run applicationn.py from your terminal:
python applicationn.py
The application will be hosted on your local machine. Open a web browser and navigate to the provided address to access the user interface. On the FWI prediction page,
enter the required meteorological data and click "Predict" to see the model's output.
