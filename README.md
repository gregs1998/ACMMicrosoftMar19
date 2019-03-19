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
3. 
