
Readme · MD
# Heart Disease Prediction
 
A machine learning project to predict the likelihood of heart disease in patients using clinical and demographic data collected from multiple hospitals.
 
## Problem Statement
 
Cardiovascular diseases are the leading cause of death globally. Early identification of at-risk patients can help prevent premature deaths. This project builds a KNN classification model to predict whether a patient is likely to have heart disease based on their medical profile.
 
## Dataset

 
918 patient records with 11 features and 1 target variable.
 
| Feature | Description |
|---|---|
| Age | Age of patient in years |
| Sex | M or F |
| ChestPainType | TA, ATA, NAP, ASY |
| RestingBP | Resting blood pressure (mm Hg) |
| Cholesterol | Serum cholesterol (mm/dl) |
| FastingBS | Fasting blood sugar > 120 mg/dl (1/0) |
| RestingECG | Normal, ST, LVH |
| MaxHR | Maximum heart rate achieved |
| ExerciseAngina | Exercise induced angina (Y/N) |
| Oldpeak | ST depression value |
| ST_Slope | Up, Flat, Down |
| HeartDisease | Target variable (1 = disease, 0 = normal) |
 
## Project Structure
 
```
heart-disease-prediction/
├── notebook.ipynb
├── dataset.csv
└── README.md
```
 
## How to Run
 
1. Clone the repository
```bash
git clone https://github.com/your-username/heart-disease-prediction.git
cd heart-disease-prediction
```
 
2. Install dependencies
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```
 
3. Open the notebook
```bash
jupyter notebook notebook.ipynb
```
 
## Exploratory Data Analysis
 
Key observations from the data:
 
- Average patient age is 53 years
- Cholesterol and RestingBP both contain zero values which are physiologically unlikely and were treated as outliers
- Cholesterol distribution is left skewed with the median roughly 25 mm/dl higher than the mean
- FastingBS and HeartDisease are integer columns but treated as categorical variables (binary 0/1)
- Dataset is predominantly male: 724 male vs 193 female patients
Sex distribution is consistent across all splits:
 
| Split | Male | Female |
|---|---|---|
| Full dataset | 724 | 193 |
| Training set | 615 | 164 |
| Test set | 109 | 29 |
 
## Approach
 
- Conducted univariate KNN classification on individual features to identify which features carry the most predictive signal
- Used cross validation to tune hyperparameters and find the optimal configuration
- Evaluated the final model on a held out test set
## Single Feature KNN Results
 
| Feature | Accuracy |
|---|---|
| MaxHR | 55.07% |
| Oldpeak | 58.70% |
| Sex_M | 61.59% |
| ExerciseAngina_Y | 73.19% |
| ST_Slope_Flat | 81.88% |
| ST_Slope_Up | 55.07% |
 
ST_Slope_Flat was the strongest single predictor with 81.88% accuracy.
 
## Final Model
 
- Algorithm: KNN Classifier
- Best parameters: metric = manhattan, n_neighbors = 19
- Cross validation accuracy: 82.67%
- Test set accuracy: 82.61%
## Key Findings
 
- ST slope (flat) is the most predictive single feature
- Exercise induced angina is also a strong predictor
- The model generalises well with cross validation and test accuracy closely aligned at 82.6%
- The dataset is predominantly male which may limit how well the model generalises to female patients
## Future Improvements
 
- Experiment with different distance metrics beyond manhattan such as euclidean or minkowski and compare their effect on accuracy
- Experiment with different values of n_neighbors beyond 19 over a wider search range
- Try other classification algorithms such as Random Forest or XGBoost to compare against KNN

## Tech Stack
 
- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook
