# 2025 End of Year Personal Data Analysis Project

Over the past few years, I’ve become increasingly excited by wearable technology and the idea of collecting and analyzing data from my own everyday life.

Starting in May, I began pairing data from my smart ring and smart watch with daily self-reported check-ins. Each morning and night, I fill out a short Google Form rating things like optimism, energy, and physical and mental state on a 1–5 scale. The goal isn't self-optimization — it is curiosity: can I spot patterns in my own data that I wouldn’t notice day to day?

## Data
For this project, I used a variety of data sources including weather data, behavioral data, physiological data from my Rinconn Gen 1 smart ring, and self-reported survey data about my mental state
#### Daily weather-related datasets:
- DayLength.csv
- Weather2025.csv

#### Daily behavioral datasets
- ScreenTime.csv
- Meditation_Day.csv
- Habits.csv

#### Daily physiological datasets
- Sleep_RC.csv
- Vitals_RC.csv
- Activity_RC.csv
  
#### Daily self-Reported datasets
Each morning and evening I filled out a google form that I created to try and quanitfy how I was feeling mentally and physically about aspects of my upcoming and completed day
- AM_Form_(Responses).csv
- PM_Form_(Responses).csv


## Data Processing 
All raw CSV files are ingested and standardized using a shared preprocessing notebook  
[`Data_Loading.ipynb`](shared/Data_Loading.ipynb

This notebook handles:
- reading and validating raw CSV inputs
- cleaning and standardizing datasets
- renaming columns for consistency across sources
- converting and aligning timestamps to enable dataset merging in downstream analyses
  
## Analyses
I completed 5 separate analyses centered around the following questions:
#### How Does Weather Affect How I Feel and What I Do?
#### How Does the Day of the Week Influence How I Feel?
#### How Does My Behavior Change Throughout the Week?
#### Do My Best Physical Days Align with My Best Mental Days?
#### How Do My Habits Affect How I Feel?

## How Does Weather Affect How I Feel and What I Do?
I am someone who has always felt like the weather noticeably affects how I feel. A question that I answer each morning is “how excited do I feel about the weather today?”. I answered the question from 1 (“it is scary and I want to avoid outside”) to 5 (“the weather is great and exciting”). Pairing these responses with a weather dataset and my Ringconn smart ring data allowed me to answer a few key questions:
#### Which weather variables carried the most weight in my daily weather ratings?
To better understand how different weather variables relate to my overall weather optimism, I trained a Random Forest model using daily weather variables (temp, day length, precipitation, and wind) to predict my self-reported AM weather optimism score. I split the data into training and test sets, then used the model’s feature importances to see which variables contributed most to its predictions.

I found that max temperature, avg temperature, and day length carried the most weight. What surprised me was how strongly day length mattered — I don’t consciously consider daylight hours the way I do temperature or precipitation, yet it clearly contributes to how I feel about the weather.

![Random forest feature importance for weather variables](analyses%20/weather/figures/RF_Importance.png)

### Does my perceived energy and fatigue change as a function of day length?
After realizing the relevance of day length, I became curious if it also related to how energized I feel. I plotted trends between day length and both my self-reported AM energy (1 = tired and groggy, 5 = energized and ready to start the day) and PM fatigue (1 = not tired at all, 5 = exhausted).

The pattern aligned closely with my experience of feeling extra tired in the winter: as day length increased, my AM energy increased, and my PM fatigue decreased at a noticeable rate. Seeing this relationship emerge in the data made me rethink winter as a natural time for rest rather than something to push through.
![Perceived energy vs day length trends](analyses%20/weather/figures/Energy_Fatigue_Smoothed.png)

### Does my sleep schedule shift at all in the winter?
Given the relationship between day length and perceived fatigue, I wondered if this shift showed up behaviorally too. I binned day length into short, medium, and long days, then examined my falling asleep and wake-up times since May (which also taught me that averaging times on a clock is not as simple as I thought).

As expected, my sleep schedule did shift: on shorter days, I slept roughly from 11:55 pm to 8:10 am, whereas on longer days my sleep shifted later, closer to 12:20 am to 8:20 am. This reinforced the idea that day length affects not just how I feel, but how I behave.
![Sleep patterns vs day length](analyses%20/weather/figures/WakeUp_FallAsleeo_Clock.png)

### What daily minimum temperature makes me excited about the weather?
Since temperature played a strong role in weather optimism, I wanted to know what my personal “sweet spot” was for me to feel excited about the weather that day. I plotted the distribution of min temperatures on days when I rated my weather optimism as a 4 or 5.

The results suggest that I feel best about the weather when the minimum temperature falls between roughly 45 and 65 degrees!
![Sleep patterns vs day length](analyses%20/weather/figures/MinTempDistribution.png)

## How Does the Day of the Week Influence How I Feel?
I really like to embrace routine, so I was curious whether my mood, expectations, and physiology follow predictable weekday patterns. I grouped my self-report and wearable data by day of the week — and a few patterns stood out immediately.

### Which weekdays start strong -- and which actually end strong? 
I created two summary variables from my daily questionnaires to answer this question:
- AM morale: how optimistic I feel about the day + how settled my mind feels 
- PM morale: how I feel mentally + my satisfaction with the day + how much fun I had + how well I stuck to my main intention 

I plotted these averaged scores across weekdays and found:
- AM morale is the lowest on Mondays and highest on Tuesdays 
- PM morale is the lowest on Tuesdays and Fridays and highest on Wednesdays and Thursdays 

The standout pattern: Tuesdays start out mentally strong but end up being my worst mental days!
![AM vs PM morale](analyses%20/day_of_week/figures/Morale.png)
### When am I most wrong about how my days will go?
That Tuesday pattern made me curious about how my expectations differ from my reality. I compared:
- The prediction error of how well my days go ( AM's "How well will today go?" - PM's "How satisfied was I with this day?")
- The prediction error of how crazy my day would be (AM's "How crazy will today be?" - PM's "How crazy was this day?")

By looking at prediction error (AM − PM) — where positive values mean I overestimated and negative values mean I underestimated — I found:
- I underestimate how chaotic my days are every single weekday (by ~14%)
- Tuesdays are the biggest miss - I consistently underestimate how crazy they will be (by almost 20%)
- I overestimate how satisfied I will be on Tuesdays and Fridays, which aligns with those being my lowest PM morale days 
- Thursdays are the day I most consistently feel better than how I predict I will feel (by ~8%) 
- Wednesdays are the day when I most accurately predict how crazy and satisfied I will feel about my day

My expectations for Tuesdays and Fridays are consistently too high and I consistently underestimate how chaotic my days will be.
![Prediction Errors](analyses%20/day_of_week/figures/PredictionErrors.png)

### How does my physiological data change across the week — and does it match how I feel?
I then looked at sleep, reported AM energy and PM fatigue, HRV, and resting HR across the week to see whether my body tells the same story as my self-reports.
- Wednesdays stand out as the day I sleep the most, feel the most energized in the morning, and most tired at night -- suggesting its a consistent "push" day for me 
- HRV decreases and resting HR increases as the week goes on 

Physically, I seem to feel best early in the week and gradually wear down -- even though mentally, Monday mornings feel the worst 

What surprised me most was the disconnect between how I feel physically vs mentally at the start of the week — and how reliably my expectations miss reality on certain days. This kind of analysis makes it possible to intervene earlier, not just reflect later.
![Fatigue Variables](analyses%20/day_of_week/figures/Fatigue.png)

## How Does My Behavior Change Throughout the Week?
After learning which days of the week I tend to feel my best and worst, I got curious about something deeper:

How does what I do differ across the week — and how does that relate to how I feel at the end of the day?

### How do my intentions differ across the week?
Each morning I set one main intention for the day: fun, productivity, recovery, or survival. Over time, clear trends emerged:
- Monday are usually focused on recovery
- Tuesday - Thursday are focused on productivity
- Weekends are mostly focused on fun
Before any behavior, my week already has structure.
![Priorities](analyses%20/day_of_week_behavior/figures/Priorities_Bar.png)

### Which days do I complete my habits most consistently?
I tracked six core habits and plotted their frequency of completion by weekday.
- Tuesdays have the highest habit completion, followed by Mondays. 
This suggests that I start out the week strong in terms of habit execution.
![Habit Radar Chart](analyses%20/day_of_week_behavior/figures/RadarChart.png)

### How does overall behavioral engagement relate to how I feel at the end of the day?
I treated each weekday as a behavioral system by combining movement, habit completion, and phone use into a single behavioral load score (z-scored within each domain).

A heatmap of these systems revealed a few insights:
- Thursday, Wednesdays, and Mondays are the days I end feeling best mentally -- and they're also the days with the the highest overall behavioral loads. For me, being meaningfully occupied across these three categories seems to support better end-of-day mental state
- Friday, Saturday, and Sunday are my lightest days behaviorally -- less activity, phone use, and habit completion -- and they're also the days that I tend to feel my worst mentally
- Screen time isn’t inherently negative for me. Higher phone use, when embedded within otherwise engaged days, is associated with better mental outcomes.
- I just hate Tuesdays -- despite similar behavioral patterns to higher performing weekdays like Monday and Thursdays, my mental state is consistently lower Tuesday night -- suggesting that factors beyond observable behavior may be at play
![Heatmap](analyses%20/day_of_week_behavior/figures/Heatmap.png)


#### Overall takeaways:
- 36% of my Thursdays are focused on survival -- that's 20% more than any other day. Aside from Monday mornings, Thursdays are also the day with my lowest AM morale. Behaviorally, I have had slightly less than average activity, much higher than average screen time, and slightly higher than average habit completion on Thursdays. This suggests that due to my low AM morale on Thursdays, I give myself an "easier" day across the board, which results in me feeling mentally strong on by Thursday nights.
- Tuesdays are my worst mental day of the week. Yesterday I learned that I start Tuesday mornings with my highest morale rating and then most frequently overestimate how successful the day will be. Tuesday are also the days where I most consistently complete habits. This suggests that maybe I am overly ambitious on Tuesday mornings and burn out by the end of the day

## Do My Best Physical Days Align with My Best Mental Days?
I've been curious -- are my best physical days also my best mental days?

### Do my physical and mental states occur in "streaks"? 
Using data from my smart ring (HRV, resting HR) and daily survey responses, each day got both a physical score and a mental score. I plotted calendar heatmaps for each in an attempt to spot patterns. For both physical and mental state, streaks emerged, but no overwhelming patterns stood out, highlighting how different each day is for me physically and mentally.
![Physical Scores Heatmap](analyses%20/physical_mental_overlap/figures/PhysicalHeatmap.png)
![Mental Scores Heatmap](analyses%20/physical_mental_overlap/figures/MentalHeatmap.png)

### Do my best physical days line up with my best mental days?
When I compared my 20 days with the highest physical scores with the 20 days with the highest mental scores, only 4 overlapped -- just 20%. Similarly, only 6 of my lowest physical days were the same as my lowest mental days (30%). Spearman correlation between physical and mental score percentiles? Practically 0 (0.02). Very rarely do my best physical days coincide with my best mental days.
![Mental Score Physical Score Correlation Plot](analyses%20/physical_mental_overlap/figures/CorrPlot.png)

### On average, Which behaviors differed between my best physical days and worst physical days?
- Message notifications: 150% fewer on my best physical days 
- Cleaning habit: 48% more on my best physical days
![Physical Score Behaviors](analyses%20/physical_mental_overlap/figures/PhysicalBehavior.png)


### Which behaviors, on average, differed between my best mental days and my worst mental days?
- Time spent on Instagram: 76% less on my best mental days
- Time spent texting: 65% less on my best mental days
- Working out: 35% more frequent on my best mental days
![Mental Score Behaviors](analyses%20/physical_mental_overlap/figures/Mental_Behaviors.png)

#### Overall takeaways:
This analysis highlighted to me how my physical and mental states are largely independent - and how some of my everyday behaviors reflect them differently.

### How Do My Habits Affect How I Feel?
For my final analysis, I wanted to see how completing certain daily habits influenced my mental and physical state. I ran paired t-tests comparing days I did the habit vs days I didn’t, focusing only on statistically significant differences (p < 0.05).

Here is what stood out:
- 🧘‍♀️ Meditation: my average HRV was 3.5% higher than on days that I meditated vs those that I did not. My resting HR was also 2% lower, suggesting that meditating is a habit that can measurably reduce physiological stress.
- 📖 Reading/Audiobooks: My end-of-day mental well-being rating was ~12% higher on days that I consumed literature vs those that I did not. This suggests that my daily reading habit could be a good mental break for my day. 
- 📒 Journaling: My nighttime fatigue rating was ~13% lower and my rating of "How crazy was this day?" was ~15.5% lower. This could mean that journaling in the moments helps me feel like I have a plan for the day and gives me a chance to offload mental clutter that otherwise might tire me out.
- 🏋‍♂️ On days in which I completed a workout, my end-of-day mental rating was 12.5% higher, my end-of-day satisfaction rating was 11% higher, and my end-of-day craziness rating was 11.6% lower. This suggests that working out really is something that I do for my mind. It leaves me feeling accomplished and grounded, and enhances my mood.



