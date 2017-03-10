Udacity Data Analyst Nanodegree
Project 7 - A/B Testing
Timothy Najmolhoda



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

If the experimental group shows a significantly higher retention rate, while avoiding a significantly negative change to the net conversion rate, this will support our hypothesis, and we will consider launching.

##Measuring Standard Deviation
