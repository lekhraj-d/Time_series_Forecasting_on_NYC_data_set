# Forecast Number of Pickups using NYC Yellow Taxi Records Data

#### Data Information:-
I have downloaded data from link:- https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page
 Jan2015 data

#### About data:-
The yellow and green taxi trip records include fields capturing pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts. The data used in the attached datasets were collected and provided to the NYC Taxi and Limousine Commission (TLC) by technology providers authorized under the Taxicab & Livery Passenger Enhancement Programs (TPEP/LPEP).

# Script:-
1. Exploratory Data Analysis ----> scripts/eda.ipynb
2. Data Cleaning and Data Preparation ---> scripts/data_cleaning.ipynb
4. Model and Training ---> scripts/model.ipynb
5. Inference  ----> scripts/inference.ipynb


## Lets start  Exploratory Data Analysis
Detailed  univariate analysis for each feature can be found in script/eda.ipynb
Data size :- (12748986, 19)

###### So here we can see total 18 columns is there details of each column can be found pdf link .
https://data.cityofnewyork.us/api/views/biws-g3hs/files/eb3ccc47-317f-4b2a-8f49-5a684b0b1ecc?download=true&filename=data_dictionary_trip_records_yellow.pdf

For our Analysis i will use few columns and details of columns are:-
1. tpep_pickup_datetime -- The date and time when the meter was engaged.
2. tpep_dropoff_datetime -- The date and time when the meter was disengaged.
3. Passenger_count -- The number of passengers in the vehicle.
4. Trip_distance -- The elapsed trip distance in miles reported by the taximeter.
5. Pickup_longitude -- Longitude where the meter was engaged.
6. Pickup_latitude -- Latitude where the meter was engaged.
7. Dropoff_longitude -- Longitude where the meter was disengaged.
8. Dropoff_ latitude -- Latitude where the meter was disengaged.
9. Fare_amount -- The time-and-distance fare calculated by the meter.
10. Total_amount -- The total amount charged to passengers. Does not include cash tips.


## EDA Observation: -
There are few ideas for Machine learning point of you: -
1. As we are having pickup records for full jan2015, we can segment pickup time for some interval (like 10 minutes, 20 minutes) and forecast for future intervals.
2. we have total fare and using this feature we can segment it for week or got s day and can-do forecasting of total revenue for future week or day.
3. we have geographical data pickup and drop latitude and longitude, now we can do clustering for various small region of NY and predict number of pickups on various time interval like 10 mint, 1hr, or day interval, so that can guide drivers where need stand for quickly services.
4. We have history trip duration and speed; we can forecast possible trip duration for any pickup.

## ML Problem Formulation
Now Based on above point we are going to solve below challenge using ML
<p>Time-series forecasting and Regression</p>
To find number of pickups, given location coordinates (latitude and longitude) and time, in the query religion and surrounding regions.
 
To solve the above we would be using data collected in 1-Jan-2015 to 20-jan-2015 and for predication rest jan2015 data .


Data Clean and Data Preparation:-
1. Data cleaning:- removes all outliers which we observe during EDA
2. We have geographical data pickup and drop latitude and longitude based on that we will Segment using Clustering.
Script:- ../scripts/data_cleaning.ipynb

## Feature Selecation:-
As for baseline models and some ML model, we will take previous interval pickups( P(t-1), P(t-2).....P(t-n)) as feature to predict pickups at P(t)
where n is hyperparameter, need to find best n.
<p>In later part we can use other parameter like weeks, weekends, ratio etc feature to improve our model, as of now will try only previous pickups details</p>

##  Performance metrics
1. Mean Absolute percentage error.
https://en.wikipedia.org/wiki/Mean_absolute_percentage_error

## Train Test Split:-
<p>1-jan-2015 to 19-jan-2015 --> Train</p>
20-jan-2016 to 31-jan-2015 --->Test


## Result Observation:-

<p>1.We can see Best MAPE we got from Light GBM model.</p>
<p>2. But still its looks high, we can go for hyperparameter tuning to improve model performance.</p>
<p>3. And Here we are using just one month data with feature as previous 5 interval, if want to improve, we can add some more month data for feature Extraction</p>


