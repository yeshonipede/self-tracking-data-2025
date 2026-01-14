#### Due to the personal and sensitive nature of this self-tracking dataset, raw data files are not included in this repository. Instead, this directory documents the structure and relevant columns of each dataset used in the analyses.

For this project, I used a variety of data sources including weather data, behavioral data, physiological data from my Rinconn Gen 1 smart ring, and self-reported survey data about my mental state
#### Daily weather-related datasets:
- DayLength.csv: contains date, sunrise, sunset, and day length
- Weather2025.csv: contains the station code from which the measurements were recorded, the station name from which the measurements were recorded, the date, the average wind, amount of precipitation, average temperature, maximum temerature, minimmum temperature

#### Daily behavioral datasets
- ScreenTime.csv: contains date, screen time (min), time spent on Instagram (min), time spent on TikTok (min), time spent on iMessage (min), number of times picking up and unlocking my phone, number of messages about receiving a text message
- Meditation_Day.csv: contains date, a column indicating whether or not I completed a meditation on each day
- Habits.csv: contains date, columns indicating if I completed my habits that day (cleaning for 5 minutes, journaled, completed a workout, consumed any form of literature, completed my turkish practice, took a creatine supplement)

#### Daily physiological datasets
- Sleep_RC.csv: contains start Time, end Time, falling Asleep Time, wake-up Time, sleep Time Ratio(%), time Asleep(min), sleep Stages - Awake(min), sleep Stages - REM(min), sleep Stages - Light Sleep (min), sleep Stages - Deep Sleep (min)
- Vitals_RC.csv: contains date. avg. Heart Rate (bpm), min. Heart Rate (bpm), max. Heart Rate(bpm), avg. Spo2(%), min. Spo2(%), max. Spo2(%), avg. HRV(ms), min. HRV (ms), max. HRV(ms)
- Activity_RC.csv: contains date, steps, calories(kcal)

  
#### Daily self-Reported datasets
Each morning and evening I filled out a google form that I created to try and quanitfy how I was feeling mentally and physically about aspects of my upcoming and completed day

AM_Form_(Responses).csv
Questions on the AM Form:
- What day of the week is it?
- How optimistic are you for the day? (1=Maximum dread to 5= Feeling good and ready for the day)
- How does your mind feel today? (1=Foggy, anxious, defeated to 5=Clear, settled)
- What is your energy level for the day? (1=Tired, slow moving, groggy to 5=Energized, rested, ready to start the day)
- What is your top priority for the day? (productivity, recovery, fun, survival)
- Do you intend to complete a workout today? (yes or no)
- Do you have to work today? (yes - normal work day, kinda-have to work for part of the day, no)
- How excited do you feel about the weather today? (1=It is very scary and I want to avoid outside to 5=The weather is great and exciting)
- How well do you predict this day will go? (1= Will be a horrible, painful day to 5= Will be a great day and I will end feeling good)
- How crazy do you predict this day to be? (1= Mundane + boring to 5=Crazy and choatic)

PM_Form_(Responses).csv
Questions on the PM Form:
- Did you complete a workout today? (yes or no)
- Did you complete a meditation today? (yes or no)
- How tired do you feel physically? (1=Not at all tired to 5=Exhausted)
- How do you feel mentally? (1=Bad, foggy, anxious to 5=Feeling clear and chill)
- How fun was your day? (1=pretty bland to 5= very fun)
- How well do you think you stuck to your primary intention for the day? (1=Not one bit to 5=Was extremely focused on my main intention for the day)
- How satisfied to you feel with how the day went (1=That day slayed me to 5=I slayed that day)
