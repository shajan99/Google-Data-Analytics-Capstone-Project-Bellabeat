### Analyze

#### The first step is checking the summary statistics of the 3 datasets using the summary function
```
summary(daily_activity_cleaned)
summary(sleep_cleaned)
summary(weight_cleaned)
```


#### Checking how users track their weight
```
weight_cleaned %>% 
  filter(IsManualReport == "True") %>% 
  group_by(Id) %>% 
  summarise("Manual Weight Report"=n()) %>%
  distinct()

weight_cleaned %>% 
  filter(IsManualReport == "False") %>% 
  group_by(Id) %>% 
  summarise("Automatic Weight Report"=n()) %>%
  distinct()
```
  * Only 8 users track their weight, which is a tiny sample to perform analysis on. 
  * Of these, 5 people logged their data manually, out of which 4 people logged infrequently. 
  * Out of the 3 who tracked their weight automatically through a device, 2 did so only once. 
  * These findings suggest that this dataset is weak, so I conducted no further analysis using this dataset.


#### Are users falling asleep in a proper time frame
  * According to [Healthline Media](https://www.healthline.com/health/healthy-sleep/how-long-does-it-take-to-fall-asleep), which has strict sourcing guidelines, normal sleep for adults means falling asleep within 10 to 20 minutes.
```
  sleep_cleaned %>% 
  filter(TimeAwake > 20) %>% 
  group_by(Id) %>% 
  summarise("Sleep problem"=n()) %>%
  distinct()
  ```
  * 20 people out of 24 took more than 20 minutes to fall asleep.
  * 5 users had a recurring problem with falling asleep within 20 minutes (more than 20 times over the 2-month time frame)
  * If this is a regular occurrence for a user, then they may have an issue, such as insomnia being on their phones.


#### Are users getting enough active minutes
  * According to Edward R. Laskowski, M.D., in his [MayoClinic post](https://www.mayoclinic.org/healthy-lifestyle/fitness/expert-answers/exercise/faq-20057916#:~:text=As%20a%20general%20goal%2C%20aim,your%20risk%20of%20metabolic%20problems.), people need at least 150 minutes of moderate activity or 75 minutes of vigorous activity a week.
```
daily_activity_cleaned %>% 
  filter(FairlyActiveMinutes >= 22 | VeryActiveMinutes >= 11) %>% 
  group_by(Id) %>% 
  summarise("Active enough"=n()) %>%
  distinct()%>%
  print(n = 30)
```
  * This means at least 22 minutes of moderate activity or 11 minutes of vigorous activity a day for adults.
  * 30 users met this guideline for activity duration on at least one occasion.
  * Of these 30, 10 users got in the required duration of activity frequently (more than 20 times over the 2-month time frame).
  * The 3rd quartile of fairly active minutes is 19. Less than 25% of observations were collected where users got in the required duration of moderate activity.
  * The mean of very active minutes is 21.16. More than 50% of observations were collected where users got in more than the required duration of vigorous activity.


#### Are users getting enough steps
  * According to Jennifer Huizen in her [Medical News Today post](https://www.medicalnewstoday.com/articles/average-steps-per-day#increasing-steps), reviewed by Debra. Rose Wilson, Ph.D., MSN, less than 5000 steps a day is considered sedentary while 10,000 steps are a good aim for general fitness for adults.
```
daily_activity_cleaned %>% 
  filter(TotalSteps > 10000) %>% 
  group_by(Id) %>% 
  summarise("Enough steps"=n()) %>%
  distinct()%>%
  print(n = 25)

daily_activity_cleaned %>% 
  filter(TotalSteps < 5000) %>% 
  group_by(Id) %>% 
  summarise("Not enough steps"=n()) %>%
  distinct()%>%
  print(n = 33)
```
  * 25 users recorded getting more than 10,000 steps on at least one occasion.
  * Of these 25, only 7 users achieved 10,000 steps frequently (more than 20 times over the 2-month time frame).
  * All 33 users recorded getting less than 5000 on at least one occasion.
  * Of these 33, 5 users took less than 5000 steps frequently (more than 20 times over the 2-month time frame).
  * It is near the 3rd quartile that 10000 is achieved i.e for ~75% of observations users did not take enough steps.


#### Are users getting enough sleep
  * It is widely accepted that people need around 7 hours of sleep every night.
```
sleep_cleaned %>% 
  filter(TotalMinutesAsleep > 420) %>% 
  group_by(Id) %>% 
  summarise("Enough sleep"=n()) %>%
  distinct()%>%
  print(n = 21)

sleep_cleaned %>% 
  filter(TotalMinutesAsleep < 420) %>% 
  group_by(Id) %>% 
  summarise("Not enough sleep"=n()) %>%
  distinct()%>%
  print(n = 23)
```
  * 21 users got enough sleep on at least one occasion.
  * Out of these 21, only 3 users got more than 7 hours of sleep frequently (more than 20 times over the 2-month time frame).
  * 23 users did not get enough sleep on at least one occasion
  * Out of these 23, only 2 users got less than 7 hours of sleep frequently (more than 20 times over the 2-month time frame).
  * The average time spent asleep is 419.2 minutes i.e. ~7 hours, which is according to the guideline.
  * The 1st Quartile is 361 minutes i.e. 6 hours.
  * The 2nd quartile is 490 minutes i.e. just above 8 hours.
  * For 50% of the observations in this dataset, users got between 6 to 8 hours of sleep


#### Plotting Calories Burned vs Steps Taken
```
ggplot(data=daily_activity_cleaned, aes(x=TotalSteps, y = Calories, color=TotalDistance))+ 
  geom_point()+ 
  geom_smooth(method='loess')+
  scale_color_gradient(low="steelblue", high="red")+
  labs(title = 'Calories Burned vs Steps Taken') +
  xlab('Total Steps') +
  ylab('Calories Burned')
```
* As expected, more steps lead to more calories burned, as more energy is used


#### Plotting Calories Burned vs Distance Covered
```
ggplot(data=daily_activity_cleaned) +
  geom_smooth(method='loess', aes(x = VeryActiveDistance, y = Calories), color = "red") +
  geom_smooth(method='loess', aes(x = ModeratelyActiveDistance, y = Calories), color = "yellow") +
  geom_smooth(method='loess', aes(x = LightActiveDistance, y = Calories), color = "green") +
  geom_smooth(method='loess', aes(x = SedentaryActiveDistance, y = Calories), color = "blue") +
  annotate("text", x = c(15,7,10.1), y = c(3820, 2150,3250), label = c("Very Active", "Moderately Active", "Lightly Active") , color="black", size=4, fontface="bold") +
  labs(title = 'Calories Burned vs Distance Covered') +
  xlab('Distance Covered') +
  ylab('Calories Burned')
```
  * How vigorously users cover their distance affects how many calories are burned
  * Surprisingly, beyond 5 km, covering distance in a lightly active way burns more energy than covering the distance in a moderately active way 


#### Plotting Calories Burned vs Minutes Active
```
ggplot(data=daily_activity_cleaned) + 
  geom_smooth(method='loess', aes(x = VeryActiveMinutes, y = Calories), color = "red") +
  geom_smooth(method='loess', aes(x = FairlyActiveMinutes, y = Calories), color = "yellow") +
  geom_smooth(method='loess', aes(x = LightlyActiveMinutes, y = Calories), color = "green") +
  geom_smooth(method='loess', aes(x = SedentaryMinutes, y = Calories), color = "blue") +
  annotate("text", x = c(265,215,580,850), y = c(4250, 1970,2800,2200), label = c("Very Active", "Moderately Active", "Lightly Active", "Sedentary") , color="black", size=4, fontface="bold") +
  labs(title = 'Calories Burned vs Minutes Active') +
  xlab('Active Minutes') +
  ylab('Calories Burned')
```
  * As expected, higher activity levels burn more calories
  * Again, being fairly active for a longer time is at least as, if not more, energy demanding than being fairly active for a shorter time

