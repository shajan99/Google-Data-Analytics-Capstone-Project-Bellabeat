### Analyze

* The first step is checking the summary statistics of the 3 datasets using the summary function

* Checking how users track their weight
  * Only 8 users track their weight, which is a tiny sample to perform analysis on. 
  * Of these, 5 people logged their data manually, out of which 4 people logged infrequently. 
  * Out of the 3 who tracked their weight automatically through a device, 2 did so only once. 
  * These findings suggest that this dataset is weak, so I conducted no further analysis using this dataset.

* Are users falling asleep in a proper time frame
  * According to Healthline Media, which has strict sourcing guidelines, normal sleep for adults means falling asleep within 10 to 20 minutes.
  * https://www.healthline.com/health/healthy-sleep/how-long-does-it-take-to-fall-asleep
  * 20 people out of 24 took more than 20 minutes to fall asleep.
  * 5 users had a recurring problem with falling asleep within 20 minutes (more than 20 times over the 2-month time frame)
  * If this is a regular occurrence for a user, then they may have an issue, such as insomnia being on their phones.

* Are users getting enough active minutes
  * According to Edward R. Laskowski, M.D., in his MayoClinic post, people need at least 150 minutes of moderate activity or 75 minutes of vigorous activity a week.
  * This means at least 22 minutes of moderate activity or 11 minutes of vigorous activity a day for adults.
  * https://www.mayoclinic.org/healthy-lifestyle/fitness/expert-answers/exercise/faq-20057916#:~:text=As%20a%20general%20goal%2C%20aim,your%20risk%20of%20metabolic%20problems.
  * 30 users met this guideline for activity duration on at least one occasion.
  * Of these 30, 10 users got in the required duration of activity frequently (more than 20 times over the 2-month time frame).
  * The 3rd quartile of fairly active minutes is 19. Less than 25% of observations were collected where users got in the required duration of moderate activity.
  * The mean of very active minutes is 21.16. More than 50% of observations were collected where users got in more than the required duration of vigorous activity.

* Are users getting enough steps
  * According to Jennifer Huizen in her Medical News Today post, reviewed by Debra. Rose Wilson, Ph.D., MSN, less than 5000 steps a day is considered sedentary while 10,000 steps are a good aim for general fitness for adults.
  * https://www.medicalnewstoday.com/articles/average-steps-per-day#increasing-steps
  * 25 users recorded getting more than 10,000 steps on at least one occasion.
  * Of these 25, only 7 users achieved 10,000 steps frequently (more than 20 times over the 2-month time frame).
  * All 33 users recorded getting less than 5000 on at least one occasion.
  * Of these 33, 5 users took less than 5000 steps frequently (more than 20 times over the 2-month time frame).
  * It is near the 3rd quartile that 10000 is achieved i.e for ~75% of observations users did not take enough steps.

* Are users getting enough sleep
  * It is widely accepted that people need around 7 hours of sleep every night.
  * 21 users got enough sleep on at least one occasion.
  * Out of these 21, only 3 users got more than 7 hours of sleep frequently (more than 20 times over the 2-month time frame).
  * 23 users did not get enough sleep on at least one occasion
  * Out of these 23, only 2 users got less than 7 hours of sleep frequently (more than 20 times over the 2-month time frame).
  * The average time spent asleep is 419.2 minutes i.e. ~7 hours, which is according to the guideline.
  * The 1st Quartile is 361 minutes i.e. 6 hours.
  * The 2nd quartile is 490 minutes i.e. just above 8 hours.
  * For 50% of the observations in this dataset, users got between 6 to 8 hours of sleep

* Plotting Calories Burned vs Steps Taken
  * As expected, more steps lead to more calories burned, as more energy is used

* Plotting Calories Burned vs Distance Covered
  * How users cover their distance affects how many calories are burned
  * Surprisingly, beyond 5 km, covering distance in a lightly active way burns more energy than covering the distance in a moderately active way 

* Plotting Calories Burned vs Minutes Active
  * As expected, higher activity levels burn more calories
  * Again, being fairly active for a longer time is at least as, if not more, energy demanding than being fairly active for a shorter time

