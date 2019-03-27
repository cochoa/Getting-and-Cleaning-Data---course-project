==================================================================
Getting and Cleaning Data - Course Project
Data cleaing for the data "Human Activity Recognition Using Smartphones Dataset"
==================================================================
Carlos Ochoa
2019/03/27
==================================================================

The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. You will be graded by your peers on a series of yes/no questions related to the project. You will be required to submit: 1) a tidy data set as described below, 2) a link to a Github repository with your script for performing the analysis, and 3) a code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.

You should create one R script called run_analysis.R that does the following.

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject. 

Comments
======================================

I have decided to move the step 4 to 2nd position, as it is easier to work with the data once
proper variable names have been set.

The exercise produces the following datasets:
=========================================

Each name of the dataset corresponds to an exercise. So, dtn means the "dataset" for "n" exercise.
(One exception: as we have moved the exercise 4 to the second place, there is not dt4.)

- dt: fusion af all the datasets available, both test and train. 10299 observations x 563 variables. Variable names properly set up.

- dt2: extraction from dt of all mean and std variables. To get this file, we look for the words "mean" and "std" within the variable names.

- dt3: it is the same information of dt2 but changing the code for activity to a label that we get from the features dataset already read.

- dt5: The average of each measurement of dt3 per activity and subject.

 

