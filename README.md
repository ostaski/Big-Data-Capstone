# Big-Data-Capstone
Completed October 2016

These files are my submissions for the Capstone Project of the Big Data Specialization taught at UC San Diego via Coursera:
https://www.coursera.org/specializations/big-data



## Week1: Initial Technical Appendix

In this short Peer Review assignment, you will be guided in writing the portion of the final project technical appendix 
that records your actions and key findings from your data exploration phase.

The goal of the technical appendix is to serve as notes on what analysis you did and key findings you made. The appendix 
would be provided to high-level officers at Eglence, Inc. to accompany a short presentation and provide them a location to 
look for a bit more detail.

For this short section of the appendix you should document the data sets you had to work with and the basics of the initial 
exploratory analysis you did. Download and fill in this template (googledoc [Note: to make a copy, click on File and then 
Make a copy. Do not click on REQUEST FOR ACCESS.], or the attached Word file below) which asks you to:

1.    Provide a quick review of the data files available for analysis (Yes, we know that this information was provided to 
you in this reading, but it would be critical for one to provide in such a report. You should copy information over and, if 
needed, re-phrase or summarize).
2.    Report on your key findings from your aggregation analysis.
3.    Report on your key findings from your filtering analysis.  



## Week2: Data Classification with KNIME

Predicting which user is likely to purchase big-ticket items while playing Catch the Pink Flamingo is valuable knowledge to 
have for Eglence since in-app purchases are a major source of revenue. In this assignment, you will analyze available data 
to classify users as buyers of big-ticket items (“HighRollers”) vs. buyers of inexpensive items (“PennyPinchers”). 
Big-ticket items are those with a price of more than $5.00, and inexpensive items are those that cost $5.00 or less.

A data file named “combined_data.csv” has been created for this assignment. This file has some data derived from the log 
files. The contents of this file are described in this reading.

You will build a KNIME workflow to perform analysis for this classification problem. Note: As you go along, be sure to 
update node names (.e.g text below nodes) and workflow annotation.

Along the way you will be creating parts of your appendix for the final project which outlines your findings explains how 
you perform this classification problem.

### Setup

Be sure to read “Workflow Overview: Building a Decision Tree in KNIME” before beginning this assignment. Start with the 
sample decision tree workflow referred to in that reading. You will modify this workflow as you perform the tasks for this 
assignment. NOTE: All the nodes you need for the workflow to complete this assignment is described in that reading. If you 
need more review, check out this review page.

### Step 1: Data Preparation

The first step is to read in the data and prepare it for modeling in KNIME. Below is an overview of the steps you will need 
to take. Download and fill in this template (googledoc, word) as you complete these steps (the completed template will be 
used as a part of your technical appendix for your final project):

    Read in the data from the file combined_data.csv. Identify the number of samples. 
(4619 rows)

    Filter samples (i.e., rows) to only contain those with purchases and identify that number. Note: You will need to add a 
    new node to your KNIME workflow for this. The new node should be placed between the File Reader and Color Manager nodes.
(used Row Filter node) Include rows by attribute value; testing avg_price column; use range checking (o.o - 100.0)
(1411 rows)

    Create a new categorical attribute for the target. This new categorical attribute will be derived by binning an 
    existing numeric attribute. Remember that for this project, we want to define two categories for price which we will 
    use to distinguish between HighRollers (buyers of items that cost more than $5.00) and PennyPinchers (buyers of items 
    that cost $5.00 or less). Note: You will need to add a new node to your KNIME workflow for this. This new node should 
    be placed between the node that was added in #2 above and Color Manager.
(used Numeric Binner node) 
PennyPinchers : ] -8 ... 5.099999999999997 [ 
HighRollers : [ 5.099999999999997 ... 8 [
Append new column: avg_price_binned

    Filter the data to only contain the attributes (i.e., columns) that you want to use for your analysis. Hint: There are 
    attributes that can be immediately identified as being inappropriate for this classification task without any analysis; 
    those attributes should be filtered out. Note: You will need to add a new node to your KNIME workflow for this. This 
    new node should be placed between the node that was added in #3 above and Color Manager.
(used Column Filter)
only included userID, count_buyId, avg_price and avg_price_binned
later changed to platformType, count_hits and avg_price

    Remove nodes Scatter Plot and Interactive Table from the workflow. You will not need those nodes for this assignment. 

### Step 2: Data Partitioning and Modeling

With the prepared data, you are now ready to create your model to predict whether a user is HighRoller or PennyPincher Next 
you will be building a decision tree. Download and fill in this template (googledoc, word) as you complete these steps

    Partition the data set into train and test data sets (60% train and 40% test). When doing so, be sure to select 
    "Stratified sampling". Also select "Use random seed", and copy and paste this number for the random seed value: 
    1466016757670. You can check this reading for an explanation of Stratified sampling.
1st partition: 846 rows
2nd partition: 565 rows
1411 rows total
846 / 1411 = 60%
565 / 1411 = 40%

    Create a decision tree. Be sure to set the decision tree learner node to use pruning for induction (Use MDL for 
    pruning).

    Take a screenshot of your resulting decision tree.

### Step 3: Evaluation

Now that you have your model built and some results, you can assess your model’s performance. Download and fill in this 
template (googledoc, word) as you complete these steps

    Open the appropriate node to view the confusion matrix and accuracy. Take a screenshot.

    Identify the overall accuracy of the model.

    Describe what the values in the confusion matrix mean. Be sure to indicate which things are correctly or incorrectly 
    predicted. 

### Step 4: Analysis Conclusions

Create a screenshot of your final KNIME workflow and draw some conclusions and make some recommendations. Download and fill 
in this template (googledoc, word) to guide you.

    What makes a user a HighRoller? Draw some insights from your analysis. Hint: Look at the resulting decision tree.



## Week3: Machine Learning - Clustering to Improve Revenue

Next, we want you to implement your own ideas to use machine learning clustering techniques to provide insight and 
actionable recommendations to Eglence Inc. to help improve their business.

For this assignment you will follow the same basic steps as modeled the iPython notebook you should have just reviewed. 
However, you should identify and use your own ideas on what attributes to use to guide the analysis (possibly based on your 
thoughts and readings from the discussion prompts this week).

As with previous weeks, we've structured the effort into a series of prompts. Your responses to each of these prompts are 
guided by a template which will support you in designing the relevant portions of the technical appendix for your final 
project in the capstone.

    Attribute Selection. Select 3 partitioning attributes (features / characteristics) and explain how each captures an 
    aspect of a user’s behavior. Note that you can also use aggregates, such as total number of ad-clicks per user, sum of 
    money spent on a specific ad category or all ad categories by each user, game clicks per hour by each user etc. You are 
    free to use any mathematical operations on the fields provided in the CSV files when creating features.

    Training Data Set Creation. Create the training data set that you will use to form clusters (see process in iPython 
    notebook if needed). Create a screenshot of the first few lines of this data set (including the header). What are the 
    dimensions of your training data set (rows x columns)? How many clusters would you like to create from this dataset? 

    Train to Create Cluster Centers. Train a K-Means clustering model in Spark on your data set. Print a screenshot of the 
    centers of each cluster. Based on the feature values of these cluster centers, explain, how you could use this 
    information to distinguish users in one cluster from another. Note: This analysis requires you to compare the cluster 
    centers and find any ‘significant’ differences in the attribute values among centers. The answer to this question will 
    depend on the attributes you have chosen. Some attributes help distinguish the clusters remarkably while others may not 
    tell you much. At this point, if you don’t find clear distinguishing patterns, perhaps re-running the clustering model 
    with different numbers of clusters and revising the attributes you picked would be a good idea.

    Recommend Actions. From the analysis you have performed using K-Means clustering, recommend two or more actions 
    Eglence Inc. can take that will have a direct or indirect impact on their revenue. For each action you recommend, give 
    a rationale for the action you recommend and how it can possibly increase revenue for the company.



## Week4: Graph Analytics of Simulated Chat Data With Neo4j

In this short peer review assignment you will be guided in performing some analysis on graph networks of 
simulated chat data related to the fictitious "Catch the Pink Flamingos" game. The results of your 
analyses will be included in the technical appendix of the final capstone report, and also submitted 
here for review.

The goal of the technical appendix is to serve as notes on what analysis you did and key findings you 
made. The appendix would be provided to high-level officers at Eglence, Inc. to accompany a short 
presentation and provide them a location to look for a bit more detail.

Download this Google Doc template or this Word Doc to use as the basis for the report you will be 
submitting. Follow the instructions in the Reading on "Graph Analytics of Catch the Pink Flamingo Chat 
Data With Neo4j" and update the template with the results. Save your completed template as a PDF and 
submit it to this assignment for review by your peers.



## Week6: Final Presentation

As mentioned in the introductory module, your final project for this course will be submitted by Peer 
Review (the actual assignment can be found in next week's materials). Below find the description of the 2 
parts of the assignment along with details about how you will be reviewed and our motivations behind the 
review process.

    A PDF of slides for a 10-minute presentation, with an accompanying script of what you would say for 
    each slide. In the assignment we will provide a template to work from and instructions on how to 
    format your PDF. Your slides and transcript will be reviewed for general appropriateness and with the 
    intent to provide you constructive criticism that you could incorporate should you wish to improve 
    these materials for presentation in an e-portfolio or for use in a job interview.

    A PDF of a technical appendix, appropriate to be provided alongside such a presentation in 1. This 
    appendix you have already created, in pieces, for the Peer Reviews submitted each week. As such, you 
    will just need to paste them together as a single PDF. Although you will get points for submitting 
    this, you will not be evaluated on it again. Our intent is that you have used the initial evaluation 
    in each week to improve your technical appendix such that it is clear and correct at this point.
