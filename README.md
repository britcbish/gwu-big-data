# DNSC 6278 - Big Data
This repository contains project work for the Summer 2019 course at George Washington University: Big Data Analytics. We were asked to source, explore, and model a dataset as well as share our findings. 

## The group:
Archit Manuja, Anuj Patel, and Brittany Bishop

## Executive Summary:
Over the course of the past few weeks our team explored Amazon's Customer Reviews Dataset. Our initial goals included visualizing variance in the number of reviews by product category, attaching sentiment to the reviews, and seeing if we could predict whether or not a review would be helpful. Using Spark on Amazon EMR to handle the data and conduct analysis, we were able to make progress towards each of these goals. 

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
   
   To model predictions for the "helpful?" variable we used logistic regression - we did this because the target variable is binary.
   
   Initially, we attempted to model our entire dataset but we found we were unable to calculate our model statistics in a reasonable timeframe (under 8 hours.) One tactic we employed to improve the speed of our modeling was to filter our dataset to reviews that received more than 100 votes regarding their helpfulness. The next step we took was to leverage the partitions in the dataset and approach product categories separately. 
   
   We then formed a couple of hypothesis upon exploring the Books, Electronics, and Kitchen product categories. We thought that perhaps people interact with reviews for Books a little differently than they might with Electronics and Kitchen products. Based on our personal experiences, we consider books more personal purchases than electronics or kitchen items and so we thought different variables might drive the helpfulness of a review. 
   
   We used the same input variables across each product category for modeling purposes:
   * star_rating
   * total_votes
   * headline_polarity
   * body_polarity
   * headline_length
   * body_length
   * year_bkt
   * vine
   * verified_purchase
   
   Lastly, we split each product category dataset into training (70%) and testing (30%) datasets. This way we had a selection of the dataset to cleanly understand the performance of each of our models. 
  
## Results/Conclusions:
Our exploration of the data yielded some points of interest:
 * The vast majority of the reviews are from the US across all three product categories that we explored.
 * The Books product category has many more observations than either Kitchen or Electronics. Running around 20.7M entries, Books is a very large category. This makes sense, given that Amazon got its start in Books, reviews for this category date as far back as 1995. The earliest reviews for Electronics are from 1999 and for Kitchen are from 2000.
 * The proportion of verified purchases is quite different for Books when compared to Electronics and Kitchen. Purchases in the Books product category were verified for roughly 51% of the reviews whereas approximately 84% of purchases were verified for both Electronics and Kitchen.
 * After creating the "helpful?" variable for prediction, we checked its distribution within Books, Electronics, and Kitchen (36%, 23%, and 27% helpful - respectively.) While there was some variance between the three product categories, we did not feel the need to oversample or change our 0.75 cutoff in our calculation of the variable. 

Our models also produced interesting results. The model metrics themselves were as follows:

| Product Category | AUC | Precision | Accuracy |
| :-----: | :----: | :----: | :----: |
| Books | 0.51 | 0.42 | 0.65 |
| Electronics | 0.90 | 0.86 | 0.94 |
| Kitchen | 0.96 | 0.94 | 0.97 |

We found it really interesting that our model predicting the helpfulness of Book reviews performed markedly worse than either of the models for Electronics or Kitchen did. This tracked well with our hypothesis that perhaps customers are looking for something in their book reviews that they may not expect or look for in electronics or kitchen item reviews. However, our exploration of the product categories also gives merit to other theories; it is possible that difference in the size of the datasets played a role, or that the difference in the verified_purchases distributions contributed to the Books model's relatively poor performance.

## Future Work:

The dataset that we chose to work with is very rich and offers many opportunities for different paths of analysis. If we were to start again, we may have chosen to go down a more text analysis focused path, or we could have chosen to try to break the dataset along a different variable as opposed to using product category. In an effort to become more comfortable with datasets of this size, our initial objectives were focused on tasks that are more simple to execute in small data environments. We were able to attach sentiment to the reviews, to understand some of the surface level differences between the product categories that we explored, and to successfully model the helpfulness of the reviews across those same product categories. With many of those objectives completed or touched on, we think there would be room to expand on the modeling techniques we used and the feature engineering that we did. Another point of future work would be to attempt tuning our clusters to better handle modeling on the complete dataset as this was something that proved to be a challenge for us throughout.
 
