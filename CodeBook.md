The script created to complete this assignment is the run_analysis.R script. It performs data preparation (loading in necessary files) and then subsequent steps to meet the coure project requirements. The steps for this script are as follows:

1. Download the dataset
  - Download and extract file from zip file found online 
  - File name is UCI HAR Dataset
  
2. Assign each data to variables (use absolute file names to pull through folder)
  - features <- features.txt
    - 561 rows, 2 columns - features for database come from accelerometer and gyroscope 3-axial raw         signals
  - activites <- test/subject_text.txt
    - 6 rows, 2 cols - a list of all activites performed when measurements were taken, also includes       codes(labels for each activity)
  - subject_test <- test/subject_test.txt
    - 2947 rows, 1 column - contains test data from 9 of 30 test subjects
  - x_test <- test/X_test.txt
    - 2947 rows, 561 columns - contains recorded features for test data
  - y_test <- test/y_test.txt 
    - 2947 rows, 1 columns - contains test data of activites code labels
  - subject_train <- train/subject_train.txt 
    - 7352 rows, 1 column - contains train data of 21 of 30 test subjects
  - x_train <- train/X_train.txt
    - 7352 rows, 561 columns - contains recorded features train data
  - y_train <- train/y_train.txt
    - 7352 rows, 1 column - contains train data of activites code labels
    
3. Merge training and test sets to form single dataframe
  - X (10299 rows, 561 columns) created by joining x_test and x_train with rbind()
  - Y (10299 rows, 1 columns) created by joining y_test and y_train with rbind()
  - Subject (10299 rows, 1 columns) created by joining subject_test and subject_train with           rbind()
  - Merged_Data (10299 rows, 563 columns) created by joining X, Y and Subject with cbind()
  
4. Extracts only measurements ofmean and std for each measurement
  - tidy_data (10299 rows, 88 cols) create by subsetting Merged_Data and selecting only columns 
    subject, code and measurements containing "mean" or "std"

5. Uses descriptive activity names for each activity in data set
  - Replace entire code column in tidy_data with corresponding activity names taken from second 
    column of activites variable
6. Appropriately labels the data set with descriptive variable names
  - code column in tidy_data changed to activities
  - all "gyro" column names changed to accelerometer
  - all "BodyBody" column names change to Body
  - all "Mag" column names changed to Magnitude
  - all columns starting with "t" changed to Frequency
  - all columns starting with "n" changed to Time

7. From data set generated in step 4, create independent set with average of each variable for each activity and subject
  - final_data (180 rows, 88 columns) created by summarizing tidy_data taking means ofeach variable     for each subject and activity
  - export final_data to a text file final_data.txt