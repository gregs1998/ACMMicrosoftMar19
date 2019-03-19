# Predict flight delays by creating a machine learning model in Python

This README was prepared as part of a workshop presented at the University of Kentucky in March 2019. The workshop is adapted from content available at docs.microsoft.com/en-us/learn/.

## Create an Azure Notebook and Import Data

First, we need to create a new Azure notebook:

1. Navigate to https://notebooks.azure.com in your browser.
2. Sign in using your Microsoft account.
3. Click **My Projects** in the menu at the top of the page, then click **+ New Project** at the top of the "My Projects" page.
4. Create a new project named "ML Notebooks" or something similar. It can be public or private, your choice.
![create new project dialog box](https://docs.microsoft.com/en-us/learn/student-evangelism/predict-flight-delays-with-python/media/1-add-project.png)
*Creating a project*
5. Click **+ New** and select **Notebook** from the menu to add a notebook to the project.
![new dropdown menu](https://docs.microsoft.com/en-us/learn/student-evangelism/predict-flight-delays-with-python/media/1-add-notebook-1.png)
*Adding a notebook to the project*
6. Give the notebook a name, like "On-Time Flight Arrivals.ipynb," and select **Python 3.6** as the language.
7. Click on the notebook to open it.

Jupyter notebooks are highly interactive and provide a great platform for manipulating data and building models from it.

1. Enter the following command into the first cell of the notebook:
```bash
!curl https://topcs.blob.core.windows.net/public/FlightData.csv -o flightdata.csv
```
2. Click the **Run** button to execute the `curl` command.
![Importing a dataset](https://docs.microsoft.com/en-us/learn/student-evangelism/predict-flight-delays-with-python/media/1-import-dataset.png)
*Importing a dataset*
3. In the notebook's second cell, enter the following Python code to: load **flightdata.csv**, create a Pandas DataFrame frome it, and display the first five rows.
```python
import pandas as pd

df = pd.read_csv('flightdata.csv')
df.head()
```
> A **DataFrame** is a two-dimensional labeled data structure. The columns can be of different types, just like a spreadsheet or database table.
4. Click the **Run** button to execute the code, your output should resemble the output below.
![Loading the dataset](https://docs.microsoft.com/en-us/learn/student-evangelism/predict-flight-delays-with-python/media/1-load-dataset.png)
*Loading the dataset*
This **DataFrame** contains on-time arrival information for an unmentioned major U.S. airline. It has 11,000 rows and 26 columns. Each row represents a flight and contains information like origin airport, destination, scheduled departure time, and whether the flight was on-time or late.

## Clean and Prepare the Data

In this section, we'll be examining the DataFrame we created earlier -- and the data inside it -- more closely.
1. To get a count of how many rows are contained in the dataset, type the following statement into an empty cell at the end of the notebook and run it:
```python
df.shape
```
The set should contain 11,231 row and 26 columns.
2. Examine the 26 columns in the dataset. They contain some important information, including:

     YEAR, MONTH, DAY_OF_MONT: Date the flight took place
     ORIGIN, DEST: Origin and destination
     CRS_DEP_TIME and CRS_ARR_TIM: Scheduled departure and arrival times
     ARR_DELAY: Difference between scheduled arrival time and actual arrivala time in mins
     ARR_DEL15: Whether the flight was late by 15 mins or more
     
One of the most important things when preparing a dataset is selecting the "feature"
