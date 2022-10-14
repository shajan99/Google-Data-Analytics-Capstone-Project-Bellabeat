# Google Data Analytics Capstone Project - Bellabeat

## Bellabeat Case Study

### Ask

**Business task**:  Analyze FitBit user data to discover trends that can be applied to Bellabeat users to inform Bellabeat's marketing strategy

Primary Stakeholders:  Executive team
Secondary stakeholders:  Marketing analytics team

### Prepare 

The downloaded zip file contains 18 CSV files.

Putting the data through the ROCCC process:
Reliability: This dataset is reliable to a good degree. For data to be reliable, it has to be accurate, unbiased, and complete. This dataset is accurate as it is directly collected from FitBit devices. It is unbiased as it contains data from 30 users, which is the minimum number of subjects needed for a sample to be representative of the population. It is, however, not complete, as there are a varying number of IDs in the 18 CSV files, indicating that not all users in this dataset tracked everything. 
Original: This dataset is original. It was generated by respondents to a distributed survey via Amazon Mechanica Turk in which the users agreed to share personal tracker data. The dataset was uploaded to Kaggle by Mobius, a healthcare data scientist and Kaggle Master. It was further sourced from Zenodo, published on 31st May 2016 by Furberg, Brinton, Keating, and Ortiz.
Comprehensive: This dataset is comprehensive down to the minute-level data, which is summed up to produce the day-level data.
Current: This dataset is not current. It covers the time period from 12th March 2016 to 12th May 2016, a 2-month period. 
Cited: This dataset is cited by Furberg, R., Brinton, J., Keating, M., & Ortiz, A. (2016). Crowd-sourced Fitbit datasets 03.12.2016-05.12.2016 [Data set]. Zenodo. https://doi.org/10.5281/zenodo.53894 on zenodo.org

Limitations in the data:
30 subjects are the minimum number required for the Central Limit Theorem to hold, so statistical tests can be run on this dataset. But it would be better if data for more users were available so that better analysis can be carried out.
The number of user IDs across the datasets is inconsistent, meaning that not all users entered complete data.

I am choosing to work with the datasets that focus on the daily use of FitBit as it is a lifestyle product. It matters more about what FitBit is used for in their day-to-day life, and where FitBit excels and falls short in this time frame. 

The datasets used are: dailyActivity, sleep, and weight.
These are in long format.

### Process

The data is processed in R for ease of data transformation and visualization.

Descriptions of each dataset along with error checks are as follows:

daily_activity
This dataset entirely includes the dailyCalories, dailyIntensities, and dailySteps data
Contains data for 33 unique IDs, which is more than the number of participants that took part in this survey.
ActivityDate variable should be date type instead of character type
TotalSteps is the number of steps taken in a day
TotalDistance is the total distance covered during a day through steps
TrackerDistance is largely conveying the same data as TotalDistance, so this column is being dropped
LoggedActivitiesDistance is ambiguous. Intuition is that this data is manually entered by the user. Since most values are zero, this column is being dropped
VeryActiveDistance is the distance covered by the user during vigorous activity
ModeratelyActiveDistance is the distance covered by the user during moderate activity
LightlyActiveDistance is the distance covered by the user during light activity
SedentaryActiveDistance is the distance covered by the user during little to no activity
VeryActiveMinutes is the duration the user engages in vigorous activity
ModeratelyActiveMinutes is the duration the user engages in moderate activity
FairlyActiveMinutes is the duration the user engages in light activity
SedentaryActiveMinutes is the duration the user engages in little to activity
Calories is the number of calories expended during the day
sleep


Contains data for 24 unique IDs
SleepDay should be split into Date & Time. Time column should be dropped as it is unnecessary for daily level analysis. Date column should be date type instead of character type
TotalSleepRecords is ambiguous. This column is being dropped.
TotalMinutesAsleep is the duration the user spent sleeping
TotalTimeInBed is the duration the user spent in bed, both sleeping and awake 
weight
Contains data for 8 unique IDs
Date should be split into Date & Time. Time column should be dropped as it is unnecessary for daily level analysis. Date column should be date type instead of character type
WeightKg is the bodyweight of the user in kilograms
WeightPound is the bodyweight of the user in pounds 
Fat is the body fat percentage of the user. 65 out of 67 entries are NA, indicating that the user did not input this data. This column is being dropped
BMI is the body mass index of the user
IsManualReport indicates whether the user manually entered body composition information or if it was uploaded automatically through a WiFi connected device
LogId is ambiguous. This column is being dropped

For the error checks above, include screenshots of code (distinct, NA, duplicate, structure)
Also include screenshots for the cleaning and transformation below

Data cleaning & transformation changelog (Description of what changed and why):

daily_activity
Changed Date variable to Date type using mutuate function
Dropped unnecessary columns using select function
TrackerDistance, as it is made redundant because of TotalDistance
LoggedActivitiesDistance, since most values are null
ActivityDate, since a new Date column was made with the correct type
Reordered columns using select function to bring Date column next to ID column
sleep
Removed duplicate entries using distinct function
Divided  Date Time column into two using separate function
Changing Date variable to Date type using mutate function
Dropped unnecessary columns using select function
TotalSleepRecords, as it is ambiguous
Time, as it is not needed for any analysis
Added TimeAwake column using mutate function as it is needed for analysis
weight
Divide Date Time column into two using separate function
Changed Date variable to Date type using mutate function
Dropped unnecessary columns using select function
Fat, because most columns are NA
LogID, because it is not needed for any analysis
Time, because it is not needed for any analysis
Merged the above datasets into merged_activity_sleep (merger of daily_activity and sleep), merged_activity_weight (merger of daily_activity and weight), and merged_data (merger of all 3 datasets). This was done using the merge function to allow for analysis 

### Analyze

The first step is checking the summary statistics of the 3 datasets using the summary function
Checking how users track their weight
Only 8 users track their weight, which is a tiny sample to perform analysis on. 
Of these, 5 people logged their data manually, out of which 4 people logged infrequently. 
Out of the 3 who tracked their weight automatically through a device, 2 did so only once. 
These findings suggest that this dataset is weak, so I conducted no further analysis using this dataset.
Are users falling asleep in a proper time frame
According to Healthline Media, which has strict sourcing guidelines, normal sleep for adults means falling asleep within 10 to 20 minutes.
https://www.healthline.com/health/healthy-sleep/how-long-does-it-take-to-fall-asleep
20 people out of 24 took more than 20 minutes to fall asleep.
5 users had a recurring problem with falling asleep within 20 minutes (more than 20 times over the 2-month time frame)
If this is a regular occurrence for a user, then they may have an issue, such as insomnia being on their phones.
Are users getting enough active minutes
According to Edward R. Laskowski, M.D., in his MayoClinic post, people need at least 150 minutes of moderate activity or 75 minutes of vigorous activity a week. This means at least 22 minutes of moderate activity or 11 minutes of vigorous activity a day for adults.
https://www.mayoclinic.org/healthy-lifestyle/fitness/expert-answers/exercise/faq-20057916#:~:text=As%20a%20general%20goal%2C%20aim,your%20risk%20of%20metabolic%20problems.
30 users met this guideline for activity duration on at least one occasion.
Of these 30, 10 users got in the required duration of activity frequently (more than 20 times over the 2-month time frame).
The 3rd quartile of fairly active minutes is 19. Less than 25% of observations were collected where users got in the required duration of moderate activity.
The mean of very active minutes is 21.16. More than 50% of observations were collected where users got in more than the required duration of vigorous activity.
Are users getting enough steps
According to Jennifer Huizen in her Medical News Today post, reviewed by Debra. Rose Wilson, Ph.D., MSN, less than 5000 steps a day is considered sedentary while 10,000 steps are a good aim for general fitness for adults.
https://www.medicalnewstoday.com/articles/average-steps-per-day#increasing-steps
25 users recorded getting more than 10,000 steps on at least one occasion.
Of these 25, only 7 users achieved 10,000 steps frequently (more than 20 times over the 2-month time frame).
All 33 users recorded getting less than 5000 on at least one occasion.
Of these 33, 5 users took less than 5000 steps frequently (more than 20 times over the 2-month time frame).
It is near the 3rd quartile that 10000 is achieved i.e for ~75% of observations users did not take enough steps.
Are users getting enough sleep
It is widely accepted that people need around 7 hours of sleep every night.
21 users got enough sleep on at least one occasion.
Out of these 21, only 3 users got more than 7 hours of sleep frequently (more than 20 times over the 2-month time frame).
23 users did not get enough sleep on at least one occasion
Out of these 23, only 2 users got less than 7 hours of sleep frequently (more than 20 times over the 2-month time frame).
The average time spent asleep is 419.2 minutes i.e. ~7 hours, which is according to the guideline.
The 1st Quartile is 361 minutes i.e. 6 hours.
The 2nd quartile is 490 minutes i.e. just above 8 hours.
For 50% of the observations in this dataset, users got between 6 to 8 hours of sleep
Plotting Calories Burned vs Steps Taken
As expected, more steps lead to more calories burned, as more energy is used
Plotting Calories Burned vs Distance Covered
How users cover their distance affects how many calories are burned
Surprisingly, beyond 5 km, covering distance in a lightly active way burns more energy than covering the distance in a moderately active way 
Plotting Calories Burned vs Minutes Active
As expected, higher activity levels burn more calories
Again, being fairly active for a longer time is at least as, if not more, energy demanding than being fairly active for a shorter time

### Share


### Act
