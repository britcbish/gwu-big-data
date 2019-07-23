# DNSC 6278 - Big Data
This repository contains project work for the Summer 2019 course at George Washington University: Big Data Analytics. We were asked to source, explore, and model a dataset as well as share our findings. 

## The group:
Archit Manuja, Anuj Patel, and Brittany Bishop

## Executive Summary:
Over the course of the past few weeks our team explored Amazon's Customer Reviews Dataset. Our initial goals included visualizing variance in the number of reviews by product category, attaching sentiment to the reviews, and seeing if we could predict whether or not a review would be helpful based on the variables available. Using Spark on Amazon EMR to handle the data and conduct analysis, we were able to make progress towards each of these goals. 

## Introduction:
We chose to explore the Amazon Customer Reviews Dataset which contains 130M+ customer reviews and associated metadata from 1995 until 2015. We worked with the dataset that is in <a href="s3://amazon-reviews-pds/parquet/" rel="nofollow">Parquet format</a> although it is also available in <a href="s3://amazon-reviews-pds/tsv/" rel="nofollow">Tab Separated Value format</a>. Even upon varying our cluster specifications, we encountered memory issues when attempting to evaluate model statistics for the full dataset and so  we chose to operate within the dataset partitions. Our work focused on the following product categories: books, kitchen, and electronics.

## Code Files:
Our code files fall into two categories:
* Data Exploration:
  * <a href="https://github.com/britcbish/gwu-big-data/blob/master/Data%20Exploration%20-%20Books.ipynb" rel="nofollow">Books Product Category Exploration</a>
  * <a href="https://github.com/britcbish/gwu-big-data/blob/master/Data%20Exploration%20-%20Electronics.ipynb" rel="nofollow">Electronics Product Category Exploration</a>
  * <a href="https://github.com/britcbish/gwu-big-data/blob/master/Data%20Exploration%20-%20Kitchen.ipynb" rel="nofollow">Kitchen Product Category Exploration</a>
* Modeling:
  * <a href="https://github.com/britcbish/gwu-big-data/blob/master/Amazon%20Reviews%20-%20Model%20Books.ipynb" rel = "nofollow">Books Model</a>
  * <a href="https://github.com/britcbish/gwu-big-data/blob/master/Amazon%20Reviews%20-%20Model%20Electronics.ipynb" rel = "nofollow">Electronics Model</a>
  * <a href="https://github.com/britcbish/gwu-big-data/blob/master/Amazon%20Reviews%20-%20Model%20Kitchen.ipynb" rel = "nofollow">Kitchen Model</a>

## Methods:
* Data Cleaning and Preparation:
  We chose to create several new variables to better understand our data:
   * Review polarity: using the textblob package we attached sentiment polarity to the headline and body portions of each review
   * Review length: the length of each review headline and body
   * helpful_ratio: a calculated variable of the number of helpful votes over the total number of votes a review received
   * helpful?: a binary variable indicating that a review is helpful if the helpful_ratio > 0.75
  This last variable is what we chose to model as we wanted to see if we could predict if a review would be helpful given our other input variables.
 * Tools:
  We used Spark to analyze the dataset and to build our models.
 * Modeling:
  To model predictions for the "helpful?" variable we used logistic regression - we did this because the target variable is binary. Initially, we attempted to model our entire dataset but we found we were unable to calculate our model statistics in a reasonable timeframe (under 8 hours.) After we chose to use the partitions in the dataset to approach categories separately, we formed a couple of hypothesis upon exploring the Books, Electronics, and Kitchen product categories. We thought that perhaps people interact with Books a little differently than they might with Electronics and Kitchen products.
  
## Results/Conclusions:

