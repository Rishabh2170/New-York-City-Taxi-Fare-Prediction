# 🚕 New York City Taxi Fare Prediction

> *Can you predict a rider's taxi fare?*

Predicting taxi fares in New York City from pickup/dropoff coordinates, pickup time and passenger count. This is my submission for the Kaggle competition **[New York City Taxi Fare Prediction](https://www.kaggle.com/competitions/new-york-city-taxi-fare-prediction/overview)**.

## 🏆 Result

| Metric | Value |
|---|---|
| **Public/Private Score (RMSE)** | **3.25688** |
| **Leaderboard Rank** | **~480 / ~1,500 participants** (top ~32%) |

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
   Trains and validates the regression model, then generates the predictions for `test.csv` and saves the file to `submission_file/`.

---

## 🛠️ Tech Stack

- **Language:** Python
- **Environment:** Jupyter Notebook
- **Libraries:** pandas, NumPy, Matplotlib / Seaborn, scikit-learn *(plus any boosting library you used, e.g. XGBoost / LightGBM)*

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
- Try gradient boosting models or ensembles / stacking
- Add features such as rush-hour flags, weekends and holidays

---

## 👤 Author

**Rishabh**
GitHub: [@Rishabh2170](https://github.com/Rishabh2170)

---

⭐ If you found this project useful, consider giving it a star!
