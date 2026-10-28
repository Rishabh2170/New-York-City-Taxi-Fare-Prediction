# 🚕 New York City Taxi Fare Prediction

> *Can you predict a rider's taxi fare?*

Predicting taxi fares in New York City from pickup/dropoff coordinates, pickup time and passenger count. This is my submission for the Kaggle competition **[New York City Taxi Fare Prediction](https://www.kaggle.com/competitions/new-york-city-taxi-fare-prediction/overview)**.

## 🏆 Result

| Metric | Value |
|---|---|
| **Best Score (RMSE)** | **3.25688** (XGBoost) |
| **Leaderboard Position** | **~480 / ~1,500 participants** (top ~32%) |

> Submissions were made after the competition deadline (late submissions), so the rank reflects where this score would fall on the leaderboard.

---

---

## 📌 Problem Statement

Given the details of a taxi ride in NYC, predict the **`fare_amount`** for the trip. The competition is evaluated using **Root Mean Squared Error (RMSE)** (lower is better).

### Dataset

| File | Description |
|---|---|
| `train.csv` | Very large training set (~55M rows) with the target `fare_amount` |
| `test.csv` | ~10K rides for which fares must be predicted |
| `sample_submission.csv` | Format of the submission file |

**Features**

- `key`: unique identifier for each ride
- `pickup_datetime`: timestamp of the pickup
- `pickup_longitude`, `pickup_latitude`: pickup coordinates
- `dropoff_longitude`, `dropoff_latitude`: dropoff coordinates
- `passenger_count`: number of passengers
- `fare_amount`: **target** (train only)

> The dataset is not included in this repo because of its size. Download it from the [competition page](https://www.kaggle.com/competitions/new-york-city-taxi-fare-prediction/data) and place it in `raw_data/`.

---

## 🗂️ Repository Structure

```
New-York-City-Taxi-Fare-Prediction/
│
├── raw_data/                         # Original Kaggle data files
├── processed_data/                   # Cleaned data and engineered features
├── model_training_data/              # Train/validation splits used for modelling
├── submission_file/                  # Final submission CSV(s) for Kaggle
│
├── data_loading.ipynb                # Efficiently loading the large dataset
├── EDA.ipynb                         # Exploratory data analysis
├── data_preparation.ipynb            # Cleaning + feature engineering
├── model_training_&_submission.ipynb # Model training, evaluation, submission
│
└── .gitignore
```

---

## 🔄 Workflow

The project is split into four notebooks that are meant to be run in order:

1. **Data Loading** (`data_loading.ipynb`)
   Loads the large training file efficiently and saves it for the later steps.

2. **Exploratory Data Analysis** (`EDA.ipynb`)
   Looks at the distribution of fares, locations, passenger counts and time patterns, and identifies outliers and invalid records.

3. **Data Preparation** (`data_preparation.ipynb`)
   Cleans the data (e.g. invalid coordinates, negative or extreme fares, unrealistic passenger counts) and creates features such as:
   - Date/time features (hour, day of week, month, year)
   - Trip distance between pickup and dropoff (e.g. Haversine distance)
   - Other location-based features

4. **Model Training & Submission** (`model_training_&_submission.ipynb`)
   Trains XGBoost, Random Forest and Ridge models, validates them with a train/validation split using RMSE, tunes hyperparameters, then generates predictions for `test.csv` and saves the files to `submission_file/`.

---

## 🤖 Models & Results

Three models were trained and compared. Each was validated with a train/validation split using **RMSE**, and its hyperparameters were tuned before submission.

| Model | Kaggle Score (RMSE) |
|---|---|
| **XGBoost Regressor** | **3.25688** ✅ |
| Random Forest Regressor | 3.36260 |
| Ridge Regression | 5.15766 |

**Final XGBoost configuration**

```python
XGBRegressor(
    objective='reg:squarederror',
    n_estimators=250,
    max_depth=7,
    learning_rate=0.1,
    subsample=0.9,
    colsample_bytree=0.7,
    min_child_weight=7,
    gamma=1,
    random_state=42,
    n_jobs=-1
)
```

**Random Forest configuration**

```python
RandomForestRegressor(
    n_estimators=500,
    max_depth=10,
    max_samples=0.8,
    bootstrap=True,
    min_samples_leaf=2,
    min_samples_split=7,
    random_state=42,
    n_jobs=-1
)
```

**Takeaways**
- Tree-based models clearly beat the linear baseline: Ridge's RMSE (5.16) is far higher than XGBoost's (3.26), which shows that fares depend non-linearly on distance, location and time.
- XGBoost edged out Random Forest, improving RMSE by about 0.11.

---

## 🛠️ Tech Stack

- **Language:** Python
- **Environment:** Jupyter Notebook
- **Libraries:** pandas, NumPy, Matplotlib / Seaborn, scikit-learn, XGBoost

---

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone https://github.com/Rishabh2170/New-York-City-Taxi-Fare-Prediction.git
cd New-York-City-Taxi-Fare-Prediction

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn jupyter

# 3. Download the data from Kaggle into raw_data/
kaggle competitions download -c new-york-city-taxi-fare-prediction -p raw_data/

# 4. Run the notebooks in order
#    data_loading -> EDA -> data_preparation -> model_training_&_submission
jupyter notebook
```

The final predictions are written to `submission_file/` and can be uploaded directly to the Kaggle competition page.

---

## 📈 Possible Improvements

- Add more location features (distance to airports, landmarks, boroughs, neighbourhood clusters)
- Use more training data and further tune hyperparameters
- Try LightGBM / CatBoost, and ensembling or stacking the best models
- Use k-fold cross-validation and more systematic tuning (e.g. Optuna)
- Add features such as rush-hour flags, weekends and holidays

---

## 👤 Author

**Rishabh**
GitHub: [@Rishabh2170](https://github.com/Rishabh2170)

---

⭐ If you found this project useful, consider giving it a star!
