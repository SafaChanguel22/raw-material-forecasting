# raw-material-forecasting
🏭 Time Series Forecasting of Raw Material Stock Prediction
![image alt](https://github.com/SafaChanguel22/raw-material-forecasting/blob/6b56b4a345e8309e2a1a3ca0323ff2ab9d57577c/Capture%20d%E2%80%99%C3%A9cran%202026-06-22%20151028.png)


## Focused skills
* Data preprocessing, manipulation and preparation
* Exploratory data analysis
* Feature engineering
* Model ensemble
* Model interpretation

In this projects, by solving a prediction problem with real-world data, we competed with other Virtual Teams and our classmates to have the best score :
Better score => More VTs defeated => higher grade.

The competition was hosted on Kaggle InClass, Kaggle is the largest platform for data science competitions

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
