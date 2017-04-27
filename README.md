# A/B Testing analysis by Germanas

# Experiment Design
## Metric Choice
### Invariant metrics:
Invariate metrics are the metrics that should not change across experimental or control groups. These metrics are measured before the point where experiment occurs. Thats why I choose these metrics as invariant metrics.
* Number of cookies. number of unique cookies to view the course overview page.  This will be used as population sizing metric that will be split between the control and experiment groups.
* Number of clicks. That is, number of unique cookies to click the "Start free trial" button. The button is clicked before the trial screen.
* Click through probability. That is, number of unique cookies to click the "Start free trial" button divided by number of unique cookies to view the course overview page. 
### Evaluation Metrics
These metrics change during the experiment and are used to evaluate the success of experiment
* Gross conversion. That is, number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the "Start free trial" button. This is a good evaluation metric because it is directly dependent on the effect of the experiment.
* Retention. That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. This metric is measured during the experiment and therefore is a evaluation metric.
* Net conversion. That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the "Start free trial" button. Not a good invariance metric and a good evaluation metric because it directly depends on the effect of experiment.
### Unused metrics
* Number of user-id. hat is, number of users who enroll in the free trial. I did not use this metric because the number of visitors could be different between the experiment and control groups and also the users who enroll in free trial also depends on experiment.
To launch the experiment I will look at gross conversion to be significantly decreased and net conversion to significantly increase.
## Measuring Standard Deviation
To calculate the standart deviations I used formula: sqrt(p(1-p)/n) where p is probability and n is population size.
|Evaluation Metric   |Standard Deviation   |
|---|---|
|Gross Conversion   |0.0202   |
|Retention   |0.0549   |
|Net Conversion	   |0.0156   |

The unit of diversion for gross conversion and net conversion is a cookie, and the denominator in each of these is also a cookie thats why their standart deviations are the lowest. I expect empirical variability to be close to analytical variability. Retention has a higher standart deviation because of the denominator being the number of users and the unit of diversion is a cookie. For retention I expect tat there will be a difference between the empirical and analytical variability.

## Sizing
### Number of Samples vs. Power
I will not use Bonferroni correlation. I calculated the pageviews needed is: 4,741,212. The total number of pageviews are: 

|Evaluation Metric   |Sample size needed   | Number of pageviews needed|
|---|---|---|
|Gross Conversion   |25,835   | 646,450|
|Retention   |39,115   |  4741212|
|Net Conversion	   |27,413  |   685,325|

Need to remove retention from evaluation metrics because it would take all the site traffic. Would take 118 days to run the experiment.
### Duration vs. Exposure
I think that this experiment is not risky for udacity, therefore I would suggest to divert 100% of traffic. If I would choose retention as evaluation metric, I would have to wait 118 days for experiment to run. Removing this evaluation metric will take me only 18 days. With 100% of traffic diverted I would split 50% and 50% for controll and experiment for best results. 
# Experiment Analysis
## Sanity Checks
With  95% confidence interval I got these values for my invariant metrics:

|Evaluation Metric   |Lower bound   | Upper bound| Observed| Passes |
|---|---|---|---|---|
|Number of cookies   |0.4988203   | 0.5011797| 0.5006396669| True|
|Number of clicks   |0.4959| 0.5041| 0.5004673474| True |
|Click-through-probability	   |0.0812058   |0.0830458| 0.0830458| True |

## Result Analysis
### Effect Size Tests
Confidence interval at 95% below:

|Evaluation Metric   |Lower bound   | Upper bound| Is statisticaly significant? | Is practicaly significant? |
|---|---|---|---|---|
|Gross conversion   |-0.0291   | -0.012| True| True|
|Net conversion   |-0.0116| 0.0019| False| False |

### Sign Tests
Using this calculator: http://graphpad.com/quickcalcs/binomial1.cfm. I computed the sign test using the day-by-day data provided by udacity.

|Evaluation Metric   |P-value   | Is statistically significant? |
|---|---|---|
|Gross Conversion   |0.0026   | True|
|Net conversion   |0.6776   | False|

### Summary
I did not use Bonferroni correction because my metrics are correlated already in that gross conversion and net conversion depends on eachother. The Bonefonni correction is a method to limit / control the risk of Type 1 errors in multiple independent metrics comparisons. If I would have used 1 metric then I would consider using the Bonferonni correction. 

Based on the significance of the effective size and sign tests, gross conversion will decrease while net conversion will not be significantly impacted.
## Recommendation
Based on the analysis above I would not recommend launching the experiment. Gross conversion was reduced practicaly and statisticaly. But net conversion failed to come up practicaly and statisticaly significant. Launching the experiment could not meet the business goals or could even reduce the revenue. Therefore I would suggest against it.
# Follow-Up Experiment
Talking from my own experience with trials I would say that for me the lower trial error leads to subscription more often I would suggest a follow-up experiment on lowering the free trial from 14 days to 7 days. I understand that at this time when I am writing this analysis, the trial is 7 days and It actualy helped me decide to subscribe to this service. After the user signs up to the trial service, I would use user-id as unit of diversion. In the experiment I would test user activity each day to the last day of the trial. I would track how much lessons the user passes and track if the user activity goes lower. I would consider the experiment as successfull if the experiment group would retain their activity even in the end of experiment and the controll group with 14 days of trial would lose the activity in the end.
My hyphothesis is that if we decrease the time of the free trial, the user activity of experiment group would be higher than in controll group. And that would lead to better Net Conversion.

* Unit of Diversion: user id. Only loged in users could be able to participate in experiment. Also it ensures that the same user would not be in both experiment and controll groups.
* Invariant Metric: user id. As the experiment is tracked after the user signs in for the trial. User id would be good invariant metric.
* Evaluation Metric: Net conversion. Number of user-ids to remain enrolled past the 7 day boundary divided by the amount of total user-id's that signed up for the trial during the same time period.

# References
* Sign test calculator http://graphpad.com/quickcalcs/binomial1.cfm
* Confidence interval http://www.wikihow.com/Calculate-Confidence-Interval



