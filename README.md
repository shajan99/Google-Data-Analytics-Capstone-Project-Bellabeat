# Google Data Analytics Capstone Project - Bellabeat

Welcome to my capstone project for the Google Data Analytics Certification. In this project, I highlight the data analysis skills I learned during the course using R.

The scenario is set as follows:

I am a junior data analyst working on the marketing analyst team at Bellabeat, a high-tech manufacturer of health-focused products for women. Bellabeat is a successful small company, but they have the potential to become a larger player in the global smart device market. Urška Sršen, cofounder and Chief Creative Officer of Bellabeat, believes that analyzing smart device fitness data could help unlock new growth opportunities for the company. I have been asked to focus on FitBit Fitness Tracker data to gain insight into how consumers are using their smart devices. The insights I discover will then be applied to a Bellabeat procduct of my choice and help guide marketing strategy for the company. 

## Ask phase

**Business task**:  Analyze FitBit user data to discover trends that can be applied to Bellabeat users to inform Bellabeat's marketing strategy

**Primary Stakeholders**:  Executive team

**Secondary stakeholders**:  Marketing analytics team


## Prepare phase

The downloaded zip file contains 18 CSV files.

Putting the data through the ROCCC process:
* Reliability: This dataset is reliable to a good degree. For data to be reliable, it has to be accurate, unbiased, and complete. This dataset is accurate as it is directly collected from FitBit devices. It is unbiased as it contains data from 30 users, which is the minimum number of subjects needed for a sample to be representative of the population. It is, however, not complete, as there are a varying number of IDs in the 18 CSV files, indicating that not all users in this dataset tracked everything. 
* Original: This dataset is original. It was generated by respondents to a distributed survey via Amazon Mechanica Turk in which the users agreed to share personal tracker data. The dataset was uploaded to Kaggle by Mobius, a healthcare data scientist and Kaggle Master. It was further sourced from Zenodo, published on 31st May 2016 by Furberg, Brinton, Keating, and Ortiz.
* Comprehensive: This dataset is comprehensive down to the minute-level data, which is summed up to produce the day-level data.
* Current: This dataset is not current. It covers the time period from 12th March 2016 to 12th May 2016, a 2-month period. 
* Cited: This dataset is cited by Furberg, R., Brinton, J., Keating, M., & Ortiz, A. (2016). Crowd-sourced Fitbit datasets 03.12.2016-05.12.2016 [Data set]. Zenodo. https://doi.org/10.5281/zenodo.53894 on zenodo.org

Limitations in the data:
* 30 subjects are the minimum number required for the Central Limit Theorem to hold, so statistical tests can be run on this dataset. But it would be better if data for more users were available so that better analysis can be carried out.
* The number of user IDs across the datasets is inconsistent, meaning that not all users entered complete data.
* In the weight dataset, the 6 of the 8 users who logged their data have done so inconsistently, making this dataset weak. 


I am choosing to work with the datasets that focus on the daily use of FitBit as it is a lifestyle product. It matters more about what FitBit is used for in their day-to-day life, and where FitBit excels and falls short in this time frame. 

The datasets used are: daily_activity, sleep, and weight.

These datasets are in long format.


## Process phase

The data is processed in R for ease of data transformation and visualization.

**Descriptions of each dataset along with error checks are as follows:**

* daily_activity
  * This dataset entirely includes the dailyCalories, dailyIntensities, and dailySteps data
  * Contains data for 33 unique IDs, which is more than the number of participants that took part in this survey.
  * ActivityDate variable should be date type instead of character type
  * TotalSteps is the number of steps taken in a day
  * TotalDistance is the total distance covered during a day through steps
  * TrackerDistance is largely conveying the same data as TotalDistance, so this column is being dropped
  * LoggedActivitiesDistance is ambiguous. Intuition is that this data is manually entered by the user. Since most values are zero, this column is being dropped
  * VeryActiveDistance is the distance covered by the user during vigorous activity
  * ModeratelyActiveDistance is the distance covered by the user during moderate activity
  * LightlyActiveDistance is the distance covered by the user during light activity
  * SedentaryActiveDistance is the distance covered by the user during little to no activity
  * VeryActiveMinutes is the duration the user engages in vigorous activity
  * ModeratelyActiveMinutes is the duration the user engages in moderate activity
  * FairlyActiveMinutes is the duration the user engages in light activity
  * SedentaryActiveMinutes is the duration the user engages in little to activity
  * Calories is the number of calories expended during the day

* sleep
  * Contains data for 24 unique IDs
  * SleepDay should be split into Date & Time. Time column should be dropped as it is unnecessary for daily level analysis. Date column should be date type instead of character type
  * TotalSleepRecords is ambiguous. This column is being dropped.
  * TotalMinutesAsleep is the duration the user spent sleeping
  * TotalTimeInBed is the duration the user spent in bed, both sleeping and awake 

* weight
  * Contains data for 8 unique IDs
  * Date should be split into Date & Time. Time column should be dropped as it is unnecessary for daily level analysis. Date column should be date type instead of character type
  * WeightKg is the bodyweight of the user in kilograms
  * WeightPound is the bodyweight of the user in pounds 
  * Fat is the body fat percentage of the user. 65 out of 67 entries are NA, indicating that the user did not input this data. This column is being dropped
  * BMI is the body mass index of the user
  * IsManualReport indicates whether the user manually entered body weight information or if it was uploaded automatically through a WiFi connected device
  * LogId is ambiguous. This column is being dropped


**Data cleaning & transformation changelog (Description of what changed and why):**

* daily_activity
  * Changed Date variable to Date type using mutuate function
  * Dropped unnecessary columns using select function
    * TrackerDistance, as it is made redundant because of TotalDistance
    * LoggedActivitiesDistance, since most values are null
    * ActivityDate, since a new Date column was made with the correct type
  * Reordered columns using select function to bring Date column next to ID column

* sleep
  * Removed duplicate entries using distinct function
  * Divided  Date Time column into two using separate function
  * Changing Date variable to Date type using mutate function
  * Dropped unnecessary columns using select function
    * TotalSleepRecords, as it is ambiguous
    * Time, as it is not needed for any analysis
  * Added TimeAwake column using mutate function as it is needed for analysis

* weight
  * Divide Date Time column into two using separate function
  * Changed Date variable to Date type using mutate function
  * Dropped unnecessary columns using select function
    * Fat, because most columns are NA
    * LogID, because it is not needed for any analysis
    * Time, because it is not needed for any analysis

* Merged the above datasets into merged_activity_sleep (merger of daily_activity and sleep), merged_activity_weight (merger of daily_activity and weight), and merged_data (merger of all 3 datasets). This was done using the merge function to allow for analysis 


## Continue to:
1. *R code*, for all code, including error checks, data cleaning, data transformation, and analysis
2. *Analysis and Visualtizations*, for a summary of the analysis carried out and the visualizations produced
3. *Recommendations*, for my final recommendations to the Bellabeat team
