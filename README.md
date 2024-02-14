# Project_1
For this first project, we were tasked with finding and analyzing a dataset of our choice. 

## Project Proposal

#### Project Title: 
    Social Media's Impact on Mental Health Across Ages
#### Team Members: 
    Dominic Thomas, Jeff Neal, Karina Gonzalez, Angelie Wanner
#### Project Description: 
    While social media offers numerous avenues for connectivity in society, it also presents distinct challenges for various age groups. Adolescents navigating identity formation, adults managing societal pressures, and seniors grappling with digital connectivity all encounter unique mental health challenges. Through data analyses, we aim to investigate the correlation between social media usage and the propensity to seek mental health support. Our objective is to unveil patterns, trends, and potential solutions to promote a healthier digital landscape for individuals of all ages.
#### Research Questions to Answer:
    1. Does social media have a detrimental impact on mental health?
    2. Which social media platform is considered the most chaotic?
    3. Is there a discernible correlation between the age groups using social media and their mental health status?
#### Datasets to Be Used:
    * Surveys (i.e. preferred platform? time spent on social media? Etc.)
#### Rough Breakdown of Tasks: 
    * Clean up of datasets; merge dataset if possible.
    * Create graphs for following:
        - Social media usage between age groups
        - Mental health by age groups
	    - Social media platforms used the most by time spent and age group (scatter plot)
    	- Boxplots to identify any outliers
	* Correlation of social media usage and mental health diagnosis
#### Hypothesis: 
    If individuals spend a minimum of 4 hours on social media daily, a 30% increase in self-reported symptoms of anxiety and depression will be observed.
#### Null Hypothesis: 
    Spending at least 4 hours on social media does not have a high effect on individuals and their mental health.

## Process
Our group leveraged the activities we've learned so far throughout the boot camp. From importing csv file, data clean up, to visualization using bar charts and boxplots.
Dependencies leveraged for code:
    Pandas
    Numpy
    Matplotlib Pyplot
    Scipy Stats

Our first task was to clean up the data. Python code utilized to read in smmh.csv file as a pandas dataframe for cleaning before moving to the analysis and graphing process. Python code was utilized to remove erroneous columns, shorten and rename columns, and redefine hour ranges for sorting purposes later in analysis and graphing. Null values were then identified and replaced to preserve number of available data points for later use. Spelling errors were corrected and duplicates were located and consolidated. Lastly, python code was utilized for preparation of the data set by creating new columns based off of the sum of questionnaire scored responses and binned grouping based off of survey participant age.

## Analysis
* Our first question we wanted to answer was: Does social media have a detrimental impact on mental health? To answer this question, we analyzed the relationship between social media usage patterns (hours spent per day) and mental health scores.

![Daily Social Media Use vs. Mental Health Score](https://github.com/DominicT1995/Project_1/blob/main/Data_output/hours_used_vs_mhs_boxplot.png)
The boxplot shows few outliers in the 0-1, 1-2, 3-4, and 5+ hourly ranges. The boxplot also displays an upward trend in median and average mental health scores as time spent on social media increases. Python code performs an ANOVA test on hourly ranges of daily social media use by total mental health scores, resulting in a p-value of 8.11e-26 which shows significant difference mental health scores between hourly usage across the data set.

```
# Split dataframe to show only users with 0-4 hours of social media use per day
low_users_df = survey_df.loc[(survey_df["Hours per day"] == "0-1") | (survey_df["Hours per day"] == "1-2") | (survey_df["Hours per day"] == "2-3") | (survey_df["Hours per day"] == "3-4")]

# Split dataframe to show only users with 4-5+ hours of social media use per day
high_users_df = survey_df.loc[(survey_df["Hours per day"] == "4-5") | (survey_df["Hours per day"] == "5+")]

# Independent t-test of mental health scores of 0-4 hours daily social media users vs 4+ daily hours users
stats.ttest_ind(low_users_df["Total score"], high_users_df["Total score"], equal_var=False)
```
Python code then splits the total survey data frame between daily hour usage below 4 hours and above 4 hours and performs a two sample t-test on these two groups to look for significant difference between mental health scores. The resulting p-value of 2.81e-13 confirms that a significant difference in mental health scores between the two divisions of the dataframe is present.

```
# Calculate percent increase in mental health score from 0-4 hours used to 4+ hours
avg_lower = low_users_df["Total score"].mean()
avg_higher = high_users_df["Total score"].mean()
percent_increase = round((avg_higher - avg_lower) / avg_lower * 100, 2)
percent_increase
```
The python code then calculates the exact percent increase between average mental health score of users in the 0-4 hour daily social media usage range compared to those using social media for 4+ hours daily with the resulting percent increase noted at 17.23%

* Our second question we wanted to look at was: Which social media platform is considered the most chaotic? For this we looked at the different social media platforms used by participants and associated mental health scores to determine which exhibited the highest level of chaos or negativity.

![Social Media Type vs. Mental Health Score](https://github.com/DominicT1995/Project_1/blob/main/Data_output/platforms_vs_mhscore_boxplot.png)
Each social media platform contains different forms of content for the viewer to engage in. Depending on the content, it could result in different mental scores and help determine which platform is considered the more “chaotic”. As seen on the boxplot, there are outliers in the lower end of the mental health scores for majority of the social media platforms used; however, TikTok did have an outlier score of 60 (highest total mental health score) which we determined indicated that it is the more "chaotic" of all the social media platforms used by participants.

* Our third question was: Is there a discernible correlation between the age groups using social media and their mental health status? To investigate this question, we analyzed data on age groups, social media usage patterns, and mental health scores.

We were able to see significant correlation between social media use and mental health from the different ANOVA tests performed and the various boxplots analyzed. The following line graph does indicate an upward trend on mental health score as the avg hours per day increases.
![Average Mental Health Score vs. Social Media Use per Day](https://github.com/DominicT1995/Project_1/blob/main/Data_output/avg_mhs_vs_hours_used_by_age_multiline_graph.png)

## Conclusion
* Overall conclusion of our project analysis:
    - From tests we ran, we were able to see that there is some correlation between time spent on social media and reported mental health scores by individuals surveyed.
    - These tests did disprove the null hypothesis that any time spent of social media would not have an effect on an individual's mental health. 
    - And although it didn't quite meet our hypothesis that it would be a 30% increase in reported mental health scores, there was still a notable increase of at least 17% between individuals that spend less than 4 hours per day and those that spend at least 4 hours a day.

* Limitations we ran into during this project:
    - Availability of data -- we were able to find quite a bit of analytical articles discussing social media and its effects on mental health, but when it came down to available raw data, it was much harder to find.
    - Luckily we were able to find the dataset from kaggle. However, this was a rather small dataset with less than 500 participants. Although it had different age groups identified, majority of the participants were between 19-25 and didn't provide an even distribution of age population.
    - Additionally, the scores are self-reported and not a true representative of medical diagnosis so there is the risk of inconsistency from person to person -- meaning what one considers as deep depression can be different than another person.
    - Lastly, time! There were some data around mental health status of Americans and their social media habits, but the raw data we found required a lot of cleanup as it was not easily readable or digestible.

* Some additional analysis we were interested in had we had more time:
    - Taken a deeper look on whether there was significant difference on data between general mental health score and social media health score -- Dominic mentioned earlier that we did seperate the scores but ultimately decided to use the total mental health score in the analysis.
    - We also saw that there was indication that individuals in a relationship had better mental health score than those identified as single.
    - We had also initially wanted to analyze if content type also had any additional effect on mental health, but the data we worked with didn't have any information on this so we were unable to add this to our analysis. So while this was a limitation, it is something that can be further looked into.

## Additional info:
- Our presentation slides can be viewed in the 'Presentation Slides' folder of this github repository. 
- The various graphs and charts created from analysis can be viewed in the 'Data_output' folder of this repository.
- The csv dataset can be viewed in the 'Resources' folder of this repository.
- The final Python code can be viewed in the 'Project_Mental_Health' folder of this repository.


