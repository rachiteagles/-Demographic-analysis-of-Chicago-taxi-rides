Datasets used

Kaggle Chicago taxi rides dataset 2016

○ Size: 2.1 GB
○ Link: https://www.kaggle.com/chicago/chicago-taxi-rides-
○ The dataset contains Chicago taxi rides for the year 2016 and has information about the trip such as
i. Pick up and drop off coordinates
ii. Time of day
iii. Duration of trip
iv. Total fare
v. Tip
○ Around 16% of the pick-up and drop off coordinates are missing
○ Additional data: JSON file to map coordinates from categories to real values

Kaggle Chicago taxi rides dataset
Datasets used

Python package ‘uszipcode’

a. Link: https://pypi.org/project/uszipcode/
b. Contains information at a zipcode level about
i. Median household income
ii. Racial distribution
iii. Educational attainment of residents

Combined Dataset

● By correlating zip codes from ‘uszipcodes’ and the coordinates from the Chicago taxi

dataset, we created a combined dataset

● This gives us a demographic profile of the pick-up and drop-off locations of each ride.

● Using this combined dataset, we can draw fascinating insights that would not have

been possible with either of the datasets in isolation.

Analytical goals

Distribution of taxi rides by income of neighbourhood
Analyse tips and fare by neighbourhood income
Analyse tips and fare by neighbourhood racial distribution
Analyse tips and fare by neighbourhood education level
Pipeline overview

● To map Taxi rides data to Census Data:
○ Collect distinct coordinates of taxi dataset on EMR
○ Map them to income, race, and educational attainment using the python census package - uszipcode

Pipeline overview

● Converted these demographic variables into categories
○ E.g., Median Household Income:
■ Less than 35k ⇒ Low Income
■ 35k to 70k ⇒ Medium Income
■ More than 70k ⇒ High Income
○ Racial Profile:
■ 66% or more residents of race X ⇒ X neighborhood
■ Else ⇒ Mixed Neighborhood
○ Education Level:
■ Average of years spent in education

Pipeline Overview

Data Cleaning:
● Convert numbers in strings to float
● Drop rows containing missing coordinates
● Restrict trip length to be less than 45 miles
● Restricting fare values to be less than 150 USD

The proportion of rides amongst income brackets

![alt text](newplot 5.png)

Most of the cabs originate from high-income neighborhoods

Average Fare by education attainment of neighborhood

The average fares are higher for neighborhoods populated by high school graduates.

Average Tip by education attainment of neighborhood

The maximum average tip comes from neighborhoods dominated by high school
graduates

Tip relative to fare by education attainment of neighborhood

Neighborhoods with highly educated residents result in relatively high tips (compared to
the fare) even though the absolute tip amount is small

Fare per mile amongst income brackets

Rides from high-income neighbourhood are costlier per mile

Tip percentage by income brackets

Rides originating from high-income neighborhoods and terminating in medium-income
neighborhoods result in higher tip per fare

Payment type by neighborhood

Cash and credit card are dominant modes of payment

Code optimization

● I used caching on the combined dataset because it was frequently used in
all the analyses
● This resulted in an 8x improvement in execution time.

Lessons Learnt

● Caching frequently used data frames helps reduce execution time significantly
● Lookup is also much faster than performing join operation, implemented while
bringing in the demographic information

Thank You