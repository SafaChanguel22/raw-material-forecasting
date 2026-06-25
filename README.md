# raw-material-forecasting
🏭 Time Series Forecasting of Raw Material Stock Prediction
![image alt](https://github.com/SafaChanguel22/raw-material-forecasting/blob/6b56b4a345e8309e2a1a3ca0323ff2ab9d57577c/Capture%20d%E2%80%99%C3%A9cran%202026-06-22%20151028.png)

# The Companies
## Append Consilting 
- Started as student consultancy in 2022
- Specializing in AI, Data Science and systems development

## Hydro 
- Global leader in aluminium and renewable
- Hydro Recycling
  Operates recyclers across Europe and North America
  
### The recycling process 
- remelting aluminium scrap
- Sourcing aluminium scrap in a volatile scrap market; collect it, process it, and remelt

### The optimazation problem 
Stock prediction is a key part of the constraints in the huge
optimization problem being solved by the company
![image alt](https://github.com/SafaChanguel22/raw-material-forecasting/blob/58b08c3794f5e94ee7e3d0c8514e9d6dcd53c080/optimization%20problem.png)

# Stock prediction 

_Context_

The optimizer must recommend a plan that does not use more of each material than we have available.

We know what we have now, but it is uncertain what we will
receive and when we will receive it.

_Prediction goal_

Make **conservative** predictions of how many **kgs of each material** that will be delivered to Azuqueca **cumulatively** by the end of each day 

_Prediction loss function, P20_

Means we should predict a number that underestimates the cumulative delivery 20% of the times, and overestimates 80%

_Evaluation metric_
![image alt](https://github.com/SafaChanguel22/raw-material-forecasting/blob/ff85ad09117045e3abfa26375fb5ebac6880bd83/P20.png)

# Data 
_receivals.csv_: Primary dataset containing historical records of material receivals, with quantity, timestamp and raw material id (**rm_id**). It contains _122 590_ records.

_purchase_orders.csv_:  Information about ordered quantities and expected delivery dates. It contains _33 171_ records.

_materials.csv_: Data about each raw material. It contains _1 217_ records.

_transport.csv_: Transportation-related data that could affect delivery times and consistency. It contains _122 590_ records.

_prediction_mapping.csv_ & _sample_submission.csv_ : Submission files.

# Important hints & Strategy

These hints define the technical strategy followed throughout this project:

### 1. Understand the target
The target is **not** daily delivered quantity, but the **cumulative kg received per material (rm_id), by the end of each day**. This means the target is monotonically non-decreasing by nature.

### 2. The loss function is the pinball loss
P20 = pinball loss at quantile τ=0.2. This penalizes underestimation 4x more than overestimation, enforcing **conservative** predictions (better to predict low and be safe).
→ **Strategy:** train models with a native quantile objective (e.g. `objective='quantile', alpha=0.2` in LightGBM, `Quantile:alpha=0.2` in CatBoost) instead of training on MSE and adjusting after the fact.

### 3. Time-aware validation
Since this is time series data, train/validation splits must respect chronology: train on the past, validate on a later period.
→ **Strategy:** use `TimeSeriesSplit` or manual expanding/rolling windows on dates, never a random row split.

### 4. Random shuffling causes information leakage
Shuffling rows before splitting mixes future information into training (via lags, rolling averages, cumulative sums).
→ **Strategy:** always sort by date first, and double-check that no feature computed for a training row uses information from a date after the validation cutoff.

### 5. Blend level estimates
Combine multiple simple, robust signals as features or baseline estimators:
- last year's level at the same period (seasonality)
- recent trend (momentum)
- recent average (smoothing/noise reduction)
→ **Strategy:** use these as engineered features and/or as a baseline ensemble to stabilize predictions, especially for materials with short or noisy history.

### 6. Cumulative predictions must not decrease
A cumulative sum can never decrease over time.
→ **Strategy:** either (a) post-process predictions with `cummax`, or (b) model non-negative daily increments and cumulate them afterward.

## Focused skills
* Data preprocessing, manipulation and preparation
* Exploratory data analysis
* Feature engineering
* Model ensemble
* Model interpretation

In this projects, by solving a prediction problem with real-world data, we competed with other Virtual Teams and our classmates to have the best score :
Better score => More VTs defeated => higher grade.

The competition was hosted on Kaggle InClass, Kaggle is the largest platform for data science competitions
