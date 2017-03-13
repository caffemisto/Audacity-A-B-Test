Udacity Data Analyst Nanodegree - Project 7 - A/B Testing - Timothy Najmolhoda

This file contains the qualitative and quantitative analysis concerning our A/B Test.

##Metric Choice

###Invariant Metrics
For this A/B Test, I chose to use three invariant metrics. They were as follows:

**1.Number of Cookies** - The number of unique cookies to view the Course Overview page in the control and experimental groups.

If the test is run correctly, cookies will be evenly divided into the control and experimental group at the time they go to the Course Overview page. Therefore, there should be little to no variance in the number of cookies that reach the page for each group.

**2.Number of Clicks** - The humber of unique cookies in each group to click the "Start free trial" button.

This experiment does not involve any changes to the Course Overview page, and thus nothing that should effect the likelihood that the participants will click on the "Start Free Trial" button. Therefore the number of clicks on the button should have little variance between the two groups. If this number is significantly different for the two groups, we will have reason to question the results of the test.

**3.Click-through Probability** - The number of unique cookies in each group to click the "Start free trial" button divided by the number of unique cookies to view the Course Overview page. 

Alternatively put, this is equal to the second invariant metric divided by the first. In a sense it is redundant to track this, but in the event that we have unexpected variance, this may give hints as to the overall effect.

###Evaluation Metrics
This A/B Test has three evaluation metrics. They are as follows:

**1. Gross Conversion** - The number of unique cookies to enter the free trial period of a lesson divided by the number of unique cookies to click on the "Start free trial" button.

The difference between the control and experimental groups is a small window questioning how much time potential students have available after clicking on "Start free trial." If they indicate a number below five hours, a message will appear discouraging them to start the free trial and suggesting they try some free materials. Tracking gross conversion will allow us to see what effect this has on the percent of students who go through with joining the free trial period. 

**2. Retention** - The number of user-ids to remain in a course for 14 days (and thus make at least one payment) divided by the number of unique cookies to enter the free trial period of a lesson.

Tracking retention as an evaluation metric will allow us to see if the warning window that appears has any effect on the percent of students who enroll in the course that actually stay in for more than two weeks. Importantly, it will let us know if the message properly warns students who may otherwise not remain in the class for the full trial duration.

**3. Net Conversion** - The number of user-ids to remain in a course for 14 days divided by the number of unique cookies to click on the "Start free trial" button.

Tracking net conversion will let us know if the warning message has any effect on the percent of users clicking on the "Start free trial" button who actually continue past the free trial. Of special note will be whether it has a negative effect on this number.

The hypothesis behind this experiment is that the warning window that pops up in the experimental group may set clearer expectations and therefore reduce the number of students who become discouraged mid-trial and quit, without significantly reducing the number of students who actually do follow through past the free trial.

The ideal results within the experimental group, that would lead us to launch the experiment live would be the following:

1 - A significant increase in the retention rate, indicating that a higher percentage of people who enter the free trial are following through with the full two weeks.

2 - A net conversion that does not significantly decrease, indicating that people who would otherwise finish the two weeks are not being turned away by the warning message.

3 - A gross conversion rate that remains the same, or has a significantly lower value in the experimental group, indicating that it is having a warning effect. This metric is the least important however, as it does not take into account people finishing the two-week trial.

###Unchosen Metrics

**1. Number of User-IDs** - This is the number of users who enter the free trial. This would not work as an invariant metric, since it would likely be affected the warning message in the experimental group. It is also not useful as an evaluation metric, because the three that were chosen tell a more complete story of the effect of the experiment.

##Measuring Standard Deviation

The analytic standard deviation was calculated below, given a sample size of 5000 cookies, and the following data:

Unique cookies to view page per day:	40000
Unique cookies to click "Start free trial" per day:	3200
Enrollments per day:	660
Click-through-probability on "Start free trial":	0.08
Probability of enrolling, given click:	0.20625
Probability of payment, given enroll:	0.53
Probability of payment, given click	0.1093125

The equation used to calculate them was the following equation:

square root ( ((probability) * (1 - probability)) / (5000 * Daily Average Ratio) )

The following values were determined.

**1. Gross Conversion** - .0202
**2. Retention** - .0549
**3. Net Conversion** - .0156

As this data is using constrained measurements rather than non-parametric values, the analytic standard deviation should be reliable, and emprical values should not need to be used.
