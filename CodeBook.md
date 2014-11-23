The data for this script is from: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

The run_analysis.R script works as follows:

1. Script reads X_train.txt, y_train.txt and subject_train.txt from the "UCI HAR Dataset/train" folder and store them in train, trainlabel and trainsubject variables.

2. Script reads X_test.txt, y_test.txt and subject_test.txt from the "UCI HAR Dataset/test" folder and store them in test, testlabel and testsubject variables.

3. Script concatenates test to train to generate bindeddata; concatenate testlabel to trainlabel to generate bindedlabel; concatenate testsubject to trainsubject to generate bindedsubject.

4. Script reads the features.txt file from the "UCI HAR Dataset" folder and store the data in a variable called features. Only measurements on the mean and standard deviation was extracted.

5. Script clean the column names of the subset. Script removes the "()" and "-" symbols in the names, as well as make the first letter of "mean" and "std" a capital letter "M" and "S”.

6. Script reads the activity_labels.txt file from the "UCI HAR Dataset "" folder and store the data in a variable called activity.

7. Script cleans the activity names in the second column of activity. Script makes all names to lower cases. If the name has an underscore between letters, script removes the underscore and capitalize the letter immediately after the underscore.

8. Script transforms the values of bindedlabel according to the activity data frame.

9. Script combines the bindeddata, bindedlabel and bindeddata by column."subject" and "activity" are the first two columns.

10. Script writes the bindeddata to "final_data.txt".
