Udacity Data Analyst Nanodegree<br>
Project 7 - A/B Testing<br> 
Timothy Najmolhoda

This file contains the qualitative and quantitative analysis concerning our A/B Test.

##References

I referenced several threads on the Udacity forum for this project, particularly those in this subforum:
https://discussions.udacity.com/c/nd002-p7-design-an-a-b-test

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

**1. Gross Conversion** - The number of unique cookies to enter the free trial period of a lesson divided by the number of unique cookies to enroll in the free trial.

The difference between the control and experimental groups is a small window questioning how much time potential students have available after clicking on "Start free trial." If they indicate a number below five hours, a message will appear discouraging them to start the free trial and suggesting they try some free materials. Tracking gross conversion will allow us to see what effect this has on the percent of students who go through with joining the free trial period. 

**2. Retention** - The number of user-ids to remain in a course for 14 days (and thus make at least one payment) divided by the number of unique cookies to enter the free trial period of a lesson.

Tracking retention as an evaluation metric will allow us to see if the warning window that appears has any effect on the percent of students who enroll in the course that actually stay in for more than two weeks. Importantly, it will let us know if the message properly warns students who may otherwise not remain in the class for the full trial duration.

**3. Net Conversion** - The number of user-ids to remain in a course for 14 days divided by the number of unique cookies to click on the "Start free trial" button.

Tracking net conversion will let us know if the warning message has any effect on the percent of users clicking on the "Start free trial" button who actually continue past the free trial. Of special note will be whether it has a negative effect on this number.

The hypothesis behind this experiment is that the warning window that pops up in the experimental group may set clearer expectations and therefore reduce the number of students who become discouraged mid-trial and quit, without significantly reducing the number of students who actually do follow through past the free trial.

The ideal results within the experimental group, that would lead us to launch the experiment live would be the following:

1 - A significant increase in the retention rate, indicating that a higher percentage of people who enter the free trial are following through with the full two weeks.

2 - A net conversion that does not significantly decrease, indicating that people who would otherwise finish the two weeks are not being turned away by the warning message.

3 - A significant decrease in the gross conversion, indicating that people that some users are in fact being turned away from the warning message.

The combination of these metrics will indicate that the pop-up message in the experimental group is effective in discouraging some users from entering the course, but that the effect is focused largely on the people who would not otherwise complete the two-week trial period.

###Unchosen Metrics

**1. Number of User-IDs** - This is the number of users who enter the free trial. This would not work as an invariant metric, since it would likely be affected by the warning message in the experimental group. 

It is also not optimal for use as an evaluation metric. It does give us a window into the effect that the experimental changes are having on people entering the free trial. However, as a metric for doing so, it is weaker than gross conversion rate, since it does so in a global rather than normalised manner. As such, we will use gross conversion rate to glean this particular data.

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

**1. Gross Conversion** - .0202<br>
**2. Retention** - .0549<br>
**3. Net Conversion** - .0156

These analytical estimates should be reliable. Our unit of diversion are cookies with further tracking by user-id at the point of registration. The evaluation metrics are measuring rates of users, with the rates being taken out of user-ids (retention) and cookies (gross and net conversion). As these are matching measurement categories, we can rely on the analytic estimates and do not need to calculate the empirical values.

##Sizing

For this evaluation, I opted not to do the Bonferroni correction. I made this decision based on the fact I was looking for a specific outcome in each of my evaluation metrics, therefore my metrics are inherently conservative, and should not need the extra caution of the Bonferroni correction in avoiding Type 1 errors. Instead, I chose not to use it in order to minimize Type II errors. (For further detail, please refer to the Summary Section).

After putting the values in the sample size calculator (http://www.evanmiller.org/ab-testing/sample-size.html) and multiplying by the likelihood ratios for each event, I received the following necessary sample sizes in pageviews for each group:

**1. Gross Conversion** - 322,937.5<br>
**2. Retention** - 3,368,909.1<br>
**3. Net Conversion** - 342,662.5

At first glance, that number for retention is untennably high. At 40,000 pageviews per day, It would take over 75 days per group if we were to divert 100% of our traffic, which is far longer than we want to use. So we will be forced to focus on gross coversion and net conversion.

By doubling the higher of those two numbers, we can determine that we will need a total of **685325** pageviews in order to ensure that our experiment provides the requesite amount statistical information.

##Duration & Exposure

There are three sorts of risk to consider here.

Firstly, we can consider the potential risks to revenue if the experimental change has a very negative effect. Here that seems unlikely since the only change is a simple pop-up box that will only appear for a portion of the experimental group. Still, it is worth considering that the experiment may have an effect other than what we hope for and anticipate.

Secondly, we must consider whether there is any sensitive data being tracked. It seems that is not the case here. We are only tracking by cookies and user ids, and when it comes to the ladder, we are not attaching it to any sensitive personal information such as sexuality or private health data.

Thirdly, we should consider whether the experiment will have any potential adverse effects on users, such as emotional damage. Here there is a potential that a user will become discouraged upon seeing a message that the course is not a good fit for them, however this potential is likely more or less equal to the discouragement that would occur from joining the free trial and finding it to be too much work. Moreveover, the level of discouragement it would provide would be accompanied by a suggestion for improvement, and would almost certainly not lead to longterm psychological effects.

With all of these in mind, I decided it was prudent to proceed with the experiment and dedicate a large portion of our traffic toward it. Therefore, It was decided to divert 75% of the traffic for this experiment. At that rate, we would be able to achieve 685,325 pageviews within 23 days.

##Sanity Checks

For my invariant metrics, I calculated and observed the following values:

###Number of Cookies
**Lower Bound** - .4988<br>
**Upper Bound** - .5012<br>
**Observed Value** .5006- 

###Number of Clicks on "Free trial"
**Lower Bound** - .4959<br>
**Upper Bound** - .5041<br>
**Observed Value** .5005

###Click-through Probability
**Lower Bound** - -.0013<br>
**Upper Bound** - .0013<br>
**Observed Value** - .0000 

It appears that all of my invariant metrics are within their expected values, and that traffic was likely diverted correctly. These sanity checks were passed.

##Effect Size Tests

For my two remaining evaluation metrics, I calculated a 95% percent interval for the likely effect size of the change made in the experimental group. They were as follows:

###Gross Conversion
**Lower Bound** - -.0291<br>
**Upper Bound** - -.0120

###Net Conversion
**Lower Bound** - -.0016<br>
**Upper Bound** - .0019

These results show that the changes in the experimental group had a negative effect on gross conversion that was both statistically significant and practically significant.

They also indicate that in the experimental group there was neither a statistically or practically significant change to the net conversion rate.

##Sign Tests

Our sign tests (calculated using http://graphpad.com/quickcalcs/binomial1.cfm) yielded the following p-values for a 95% confidence interval:

**Gross Conversion** - .0026<br>
**Net Conversion** - .6776<br>

This indicates that the p-value of our gross conversion is indeed statistically significant, and the p-value for our net conversion is not statistically significant.

##Summary

In this experiment, I opted not to use the Bonferroni correction. I did this because in this experiment, I had two evaluation metrics, and I was interested in tracking both of theirs. That is to say, in order to recommend launching this experiment live, I wanted to demonstrate a significant decrease in gross conversion AND not show any evidence of a significant change in net conversion. Since I was looking for both metrics to match my expectations, the experiment was at greater risk of a Type II error (failing to reject a false null hypthothesis) than a Type I error (rejecting a true null hypothesis). As the Bonferroni reduces Type I errors and makes Type II errors more likely, I did not use it.

Our results show that the decision to not use the Bonferroni correction was sound, as both the Effect Size Test and the Sign Test gave the same results, a significant negative statistical effect within the experiment group, and no significant observable effect on net conversion.

##Recommendation

After looking at the results of this A/B Test, my recommendation is that we do not push our experiment live. This is based on the following observations:

1 - The gross conversion rate in our experimental group was significantly lower than that in our control group. This significance was both statistical and practical. This meant that the changes in our experimental group were indeed discouraging some users who clicked on "Start free trial" from entering the two week trial.

2 - The net conversion rate in our experimental group showed no statistical significant difference from that in our control group. However, our confidence interval above did cross over into the threshold of practical significance (-.0075) that we were looking to avoid. 

Taken together, this shows that the changes to the experimental group did statistically impact the gross conversion rate, but there is also evidence that it may have had a negative practical effect on net conversion that Audacity wants to avoid. Based on these results, my recommendation is that we continue to test other means that that affect gross conversion rate whilst more clearly avoiding negative consequences to our negative conversion rate.

##Follow-up Experiment

Audacity is interested increasing the number of students who follow through with their two week trial, so it will be worthwhile to further test things that can impact this. The preceding experiment tested whether warning students about time commitment might have an effect. However, another limiting factor worth considering might be a student's existing knowledge base.

For this experiment, I would divide traffic into two groups. Users in the control group would get the same user experience Audacity users normally do when viewing the Course Overview page. However, in the experimental group, upon clicking on "Start free trial," students would be given a brief quiz of three questions on foundational material necessary for the course. If the student got all three correct, they would be taken to the registration page.

If the student got any of them wrong, they would still be given the option to register, however they would also be given a specific recommendation on something to study instead (via an Audacity free course, or a known credible free alternative) to polish up on before enrolling.

The hypothetical benefit of this approach is that it gives students who may be lacking in necessary skills a specific, tangible suggestion that they can improve on, and thus they may be likely to follow this advice.

As this experiment centers largely around the same slice of user experience that our previous experiment did, we could use the same invartiant metrics (number of cookies, number of clicks, and click-through probability), and focus on the same evaluation metrics (gross conversion and net conversion). Just as with the previous experiment, we would be looking to significantly decrease gross conversion without decreasing our net conversion significantly.
