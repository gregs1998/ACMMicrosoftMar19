# Azure Notebooks + ML

## Create a New Azure Notebook
1) Sign into Azure Notebooks with Microsoft Account, create project "FirstProjectUKY", create notebook "HelloWorld.ipynb". The ipynb ending is important, don't omit it! 
2) Type `print("Hello world!")` in first cell, then *Shift+Enter* to run it. Notice the output! We just ran python code from a cloud-based environment, without installing anything on our local machine!!
3) Now, we need to access the public notebook for the tutorial. Notice this isn't a python machine learning workshop. The primary objective is to introduce you to Azure Notebooks, familiarize you with it and its capabilities. I'll briefly touch on each code segement, but since we have lots to cover, I don't want to spend too much time typing code. Ask questions if you want to know how something works.

## Accessing the Public Notebook
1) Go to https://bit.ly/2TNrUnJ and click **Clone**
2) Sign in with your microsoft account
3) Uncheck Public, if you wish
4) Click **Clone**
5) Click to open *FlightDelayML.ipynb*

## Getting Started - Importing Dataset
1) These blocks of code are called cells. We can run them individually or collectively. Note that often, cells above the current one must be run in order to resolve some references. Click in first code cell and click **Shift+Enter**
2) This cell imports our dataset, which we'll explore more soon
3) Click second cell, **Shift+Enter**
4) This creates a Pandas DataFrame. This is a 2-D datastructure with labeled columns. The output is first five rows of the DataFrame. Like a spreadsheet, a DataFrame can contain various types of data in its rows
5) This particular DataFrame contains on-time arrival information for a major US airline. It contains 11,000+ rows and 26 columns. One row in the DataFrame represents one single flight

## Cleaning Data
1) Next cell, **Shift+Enter**
2) This code checks for missing values in any column. Result is true, so we'll dig further to see what's missing
3) Next cell, **Shift+Enter**
4) This code presents a list of missing values in each column
5) Notice that "Unnamed: 25" is missing all 11,000+ rows, so we should drop it
6) Next cell, **Shift+Enter**
7) This cell dropped the column, notice from the ouput it is gone
8) We've dropped the column with all missing values, but now we want to clean further and drop some columns that aren't important to predictive model. 
9) Next cell, **Shift+Enter**
10) This cell retains only the specified columns and drops all others. Notice from output that only *ARR_DEL15* is missing rows
11) We want to see first five rows that are missing, so next cell **Shift+Enter**
12) We know that these are actually canceled or diverted flights. We could drop them, but will fill them with 1s in *ARR_DEL15* to indicate they were late
13) Next cell, **Shift+Enter**
14) From sample output, we see that 1s have been filled
15) I'm going to move a bit faster now so we aren't here forever. This next block will bucketize the time values by hour (divide 24-hour time value by 100). We have over 500 unique time values in the set, so this will help sort only by hour, more useful
16) Next cell, **Shift+Enter**
17) Next cell will convert ORIGIN and DEST fields from single column with code to distinct column with ones and zeros to indicate whether that airport is ORG/DEST or not
18) Next cell, **Shift+Enter**
19) Our code is clean and we're ready to build the ML model!

## Building the Model
1) Next cell, **Shift+Enter**
2) This cell imports Scikit-Learn's train_test_split helper function
3) Splits DataFrame into training set containing 80% for training, 20% for testing. This is important so we have set of data model has never seen in order to score accuracy. First and second params are DataFrames containing **Features** (what is used to predict) and **Labels** (what is predicted - late or not?)
4) Next cell, **Shift+Enter**
5) That cell displays rows+columns in DataFrame containing features to be used for training
6) Next cell, **Shift+Enter**
7) That cell returns the DataFrame containing features used for testing
8) We're going to train a binary classification model- two options, will it arrive on time or late?
9) We'll use Scikit-Learn's RandomForestClassifier class, which fits multiple decision trees to dataset to boost accuracy and limit overfitting
10) Next cell, **Shift+Enter**
11) That cell creates a RandomForestClassifier class object and trains it by calling *fit* method
12) The output shows parameters used for training. They are default, but we could modify to help improve accuracy
13) Next cell, **Shift+Enter** This next cell is going to call *Score* to determine the mean accuracy of the model
14) We see 86% mean accuracy. Looks good, but may not really represent how good the model is at determining late versus on-time
15) Next block we'll generate ROC score (*receiver operating characteristic score*)
16) It considers the probability in dataset of on-time versus late flight
17) Next cell, **Shift+Enter**
18) Notice lower 67% score, because dataset is far more likely to contain on-time flight data than late
19) In reality, you'd use lots of ways to make model more accurate, but we'll move on for now

## Visualizing Output with Matplotlib
1) Open-source graphics library for Python. Very popular, allows us to visualize model output
2) Next cell, **Shift+Enter**
3) Here we have mean accuracy as the blue line, 50% chance of getting it right as the dotted line in the middle

## Testing with Own Data + Plotting
1) The purpose of building this model was to predict whether a given flight would be on-time or late. Now we need to write a python function that calls the ML model to compute the likelihood
2) Next cell, **Shift+Enter** *Here is such a function*
3) It takes `date, time, origin airport, dest airport` as inputs, retuns probability the flight will arrive on-time from 0.0 to 1.0
4) In the function, we construct a Panda DataFrame that exactly matches the structure of the one used earlier. The date format is dd/mm/yyyy
5) Here we have two examples of flights **Shift+Enter** x2
6) Next, we'll use `predict_delay` and Matplotlib to plot the probability of on-time flights leaving from SEA to ATL at 9am, 12pm, 3pm, 6pm, and 9pm on January 30th
7) **Shift+Enter**

# LUIS
LUIS, Language Understanding Intelligent Service, helps your application understand what a person wants in their own words. We can use machine learning to allow developers to build applications that can receive user input in natural language, then extract meaning from it.

1) The application passes in an utterance (written, natural language phrase) to the API endpoint
2) It recognizes intent (what the user wants to do), and entities (*how* the user wants to do it, modifiers of intent)
Let's get started... We're going to keep with flight theme and build a customer service bot model for an airline

1) Go to www.luis.ai
2) Login, Create new app
3) Give name: AirlineHelpBot
4) We want to recognize, for demo purposes, two intents: BookFlight and CancelFlight
5) Intents -> **+ Create new intent**
6) *BookFlight*
7) Intents -> **+ Create new intent**
8) *CancelFlight*
9) We want to add entity: Location (type: list)... Add roles to entity: destination and origin
10) We need to add normalized values: Seattle, Lexington, Miami, Los Angeles, New York
11) Add synonyms: LA, NYC
12) We need to train with potential user patterns of text to book and cancel a flight
13) Patterns -> Select an Intent -> BookFlight: "I want to book a flight from {Location:Origin} to {Location:Destination}
14) Patterns -> BookFlight -> "I want to fly from {Location:Origin} to {Location:Destination}
15) Patterns -> CancelFlight -> "I want to cancel my flight to {Location:Destination}"
16) **Train**
17) **test**
18) **Publish**
19) This exposes an API endpoint where I can send an utterance in JSON format, and it will return intent with entities in JSON. We could parse this to tie into a reservation app and actually schedule the flight.

## Wrap-up

Questions??
