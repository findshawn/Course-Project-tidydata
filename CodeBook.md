### Summary:

This is the code book that describes the variables, the data, and any transformations or work performed to clean up the data.

### Background:

One of the most exciting areas in all of data science right now is wearable computing. Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Here are the data for the project:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

### What does the script *run_analysis.R* do:

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

### What does the output (tidy) data look like:

1. **35 oberservations** (unique subject & activity combinations) and **66 calculated fields**.
2. The 66 calculated fields are the average value for each variable given the subject and his/her activity.

### Features in raw data:

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

### Features in output (tidy) data:

Key terms in the 66 variable names:

- **Time:** time domain signals
- **Frequency:** frequency domain signals
- **Body-Acceleration:** body acceration signals 
- **Gravity-Acceleration:** gravity acceration signals 
- **Jerk:** Jerk signals derived from the body linear acceleration and angular velocity
- **Magnitude:** the magnitude of these three-dimensional signals calculated using the Euclidean norm
- **Gyration:** gyration signals captured by gyroscope
- **XYZ:** the 3-axial signals in the X, Y and Z directions

- **mean:** the average value (same unit from the raw data)
- **std:** standard deviation (1 equals to one standard deviation)

### Detailed data cleaning process:

1. Download, unzip and load the raw data into R.
2. Combine the train and test data.
3. Get column names from the file *features.txt* and apply them to the combined data frame.
4. Extracts only the measurements on the mean and standard deviation for each measurement by searching the patterns "mean()" or "std()" in variable names.
5. Append the activity names to the data frame using the files *y_train.txt*, *y_test.txt*, and the lookup table *activity_labels.txt*.
6. Append the subject id to the data frame using the files *subject_train.txt* and *subject_test.txt*.
7. Clean the variable names using the following transformation rules:
    - "t" -> "Time"
    - "f" -> "Frequency"
    - "Acc" -> "Acceleration"
    - "Gyro" -> "Gyration"
    - "Mag" -> "Magnitude"
    - "-" -> make sure every two words are seperated by one "-"
    - "(" -> removed
    - ")" -> removed
8. Rollup the dataset by *Subject* and *Activity*, and calculate the mean of each variable to populated the output (tidy) data.
