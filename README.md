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

