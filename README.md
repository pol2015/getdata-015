# getdata-015
Getting and Cleaning Data - Assignment

#Install dplyr required for step # 5

#install.packages("dplyr")
#library(dplyr)


#STEP 0 - Read training and the test sets

# training and the test sets location in my PC

string_train_df <- c("C:/Users/-6/Downloads/getdata_projectfiles_UCI HAR Dataset/UCI HAR Dataset/train/X_train.txt")
string_test_df <- c("C:/Users/-6/Downloads/getdata_projectfiles_UCI HAR Dataset/UCI HAR Dataset/test/X_test.txt")

# Create training Raw DataFrame

train_df <- read.table(string_train_df)
#nrow(train_df) 7352 checking # of rows for training set
#ncol(train_df) 561 checking # of columns for training set

# Create Test Raw DataFrame

test_df <- read.table(string_test_df)
#nrow(test_df) 2947 number of rows for test set
#ncol(test_df) 561 number of columns for test set

##STEP 1 - Merges the training and the test sets to create one data set named train_test_df

train_test_df <- rbind(train_df,test_df)
#nrow(train_test_df) 10299 number of rows ok (7352 + 2947) 
#ncol(train_test_df) 561 number of columns ok



#STEP 2 - Extracts only the measurements on the mean and standard deviation for each measurement:

# get selected columns that cointains "mean" string based on features.txt information 
# get selected columns that cointains "std" string based on features.txt information
  
mean_train_test_df <- train_test_df[, c(1,2,3,41,42,43,81,82,83,121,122,123,161,162,163,201,214,227,240,253,266,267,268,294,295,296,345,346,347,373,374,375,424,425,426,452,453,454,503,513,516,526,529,539,542,552)]


standard_train_test_df <- train_test_df[, c(4,5,6,44,45,46,84,85,86,124,125,126,164,165,166,202,215,228,241,254,269,270,271,348,349,350,427,428,429,504,517,530,543)]

# Merge mean and standard deviation dataframes into a single one
mean_standard_train_test_df <- cbind(mean_train_test_df,standard_train_test_df)
#ncol(mean_standard_train_test_df) 79

#STEP 3 - Uses descriptive activity names to name the activities in the data set:

string_activities_train_df <- c("C:/Users/-6/Downloads/getdata_projectfiles_UCI HAR Dataset/UCI HAR Dataset/train/y_train.txt")
string_activities_test_df <- c("C:/Users/-6/Downloads/getdata_projectfiles_UCI HAR Dataset/UCI HAR Dataset/test/y_test.txt")

# Create activity training raw DataFrame

activities_train_df <- read.table(string_activities_train_df)
#nrow(activities_train_df) 7352

# Create activity test raw DataFrame

activities_test_df <- read.table(string_activities_test_df)
#nrow(activities_test_df) 2947

# Merge both activity training and activity test DataFrames

activities_train_test_df <- rbind(activities_train_df,activities_test_df)
#nrow(activities_train_test_df) 10299
#ncol(activities_train_test_df) 1


# Replace Activity index with Activity Names for the activity training test DataFrame


activities_train_test_df[activities_train_test_df$V1 == 1 ,] <- c("WALKING")
activities_train_test_df[activities_train_test_df$V1 == 2 ,] <- c("WALKING_UPSTAIRS")
activities_train_test_df[activities_train_test_df$V1 == 3 ,] <- c("WALKING_DOWNSTAIRS")
activities_train_test_df[activities_train_test_df$V1 == 4 ,] <- c("SITTING")
activities_train_test_df[activities_train_test_df$V1 == 5 ,] <- c("STANDING")
activities_train_test_df[activities_train_test_df$V1 == 6 ,] <- c("LAYING")




string_subject_train_df <- c("C:/Users/-6/Downloads/getdata_projectfiles_UCI HAR Dataset/UCI HAR Dataset/train/subject_train.txt")
string_subject_test_df <- c("C:/Users/-6/Downloads/getdata_projectfiles_UCI HAR Dataset/UCI HAR Dataset/test/subject_test.txt")

subject_train_df <- read.table(string_subject_train_df)
#nrow(subject_train_df) 7352

subject_test_df <- read.table(string_subject_test_df)
#nrow(subject_test_df) 2947


subject_train_test_df <- rbind(subject_train_df,subject_test_df)
#nrow(subject_train_test_df) 10299

# Merge Activities and Subject Name DataFrame into main dataset from Step # 2


mean_standard_train_test_activities_subject_df <- cbind(mean_standard_train_test_df,activities_train_test_df,subject_train_test_df)




#STEP 4 - Appropriately labels the data set with descriptive variable names. 


colnames(mean_standard_train_test_activities_subject_df) <- c("tBodyAcc_mean_X","tBodyAcc_mean_Y","tBodyAcc_mean_Z","tGravityAcc_mean_X","tGravityAcc_mean_Y","tGravityAcc_mean_Z","tBodyAccJerk_mean_X","tBodyAccJerk_mean_Y","tBodyAccJerk_mean_Z","tBodyGyro_mean_X","tBodyGyro_mean_Y","tBodyGyro_mean_Z","tBodyGyroJerk_mean_X","tBodyGyroJerk_mean_Y","tBodyGyroJerk_mean_Z","tBodyAccMag_mean","tGravityAccMag_mean","tBodyAccJerkMag_mean","tBodyGyroMag_mean","tBodyGyroJerkMag_mean","fBodyAcc_mean_X","fBodyAcc_mean_Y","fBodyAcc_mean_Z","fBodyAcc_meanFreq_X","fBodyAcc_meanFreq_Y","fBodyAcc_meanFreq_Z","fBodyAccJerk_mean_X","fBodyAccJerk_mean_Y","fBodyAccJerk_mean_Z","fBodyAccJerk_meanFreq_X","fBodyAccJerk_meanFreq_Y","fBodyAccJerk_meanFreq_Z","fBodyGyro_mean_X","fBodyGyro_mean_Y","fBodyGyro_mean_Z","fBodyGyro_meanFreq_X","fBodyGyro_meanFreq_Y","fBodyGyro_meanFreq_Z","fBodyAccMag_mean","fBodyAccMag_meanFreq","fBodyBodyAccJerkMag_mean","fBodyBodyAccJerkMag_meanFreq","fBodyBodyGyroMag_mean","fBodyBodyGyroMag_meanFreq","fBodyBodyGyroJerkMag_mean","fBodyBodyGyroJerkMag_meanFreq","tBodyAcc_std_X","tBodyAcc_std_Y","tBodyAcc_std_Z","tGravityAcc_std_X","tGravityAcc_std_Y","tGravityAcc_std_Z","tBodyAccJerk_std_X","tBodyAccJerk_std_Y","tBodyAccJerk_std_Z","tBodyGyro_std_X","tBodyGyro_std_Y","tBodyGyro_std_Z","tBodyGyroJerk_std_X","tBodyGyroJerk_std_Y","tBodyGyroJerk_std_Z","tBodyAccMag_std","tGravityAccMag_std","tBodyAccJerkMag_std","tBodyGyroMag_std","tBodyGyroJerkMag_std","fBodyAcc_std_X","fBodyAcc_std_Y","fBodyAcc_std_Z","fBodyAccJerk_std_X","fBodyAccJerk_std_Y","fBodyAccJerk_std_Z","fBodyGyro_std_X","fBodyGyro_std_Y","fBodyGyro_std_Z","fBodyAccMag_std","fBodyBodyAccJerkMag_std","fBodyBodyGyroMag_std","fBodyBodyGyroJerkMag_std","Activity_Name","Subject")
#ncol(mean_standard_train_test_activities_subject_df) 81


#STEP 5 From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.


tiny_data <- mean_standard_train_test_activities_subject_df %>%
  group_by(Activity_Name,Subject)  %>%
  summarise(tBodyAcc_mean_X_avg = mean(tBodyAcc_mean_X),tBodyAcc_mean_Y_avg = mean(tBodyAcc_mean_Y),tBodyAcc_mean_Z_avg = mean(tBodyAcc_mean_Z),tGravityAcc_mean_X_avg = mean(tGravityAcc_mean_X),tGravityAcc_mean_Y_avg = mean(tGravityAcc_mean_Y),tGravityAcc_mean_Z_avg = mean(tGravityAcc_mean_Z),tBodyAccJerk_mean_X_avg = mean(tBodyAccJerk_mean_X),tBodyAccJerk_mean_Y_avg = mean(tBodyAccJerk_mean_Y),tBodyAccJerk_mean_Z_avg = mean(tBodyAccJerk_mean_Z),tBodyGyro_mean_X_avg = mean(tBodyGyro_mean_X),tBodyGyro_mean_Y_avg = mean(tBodyGyro_mean_Y),tBodyGyro_mean_Z_avg = mean(tBodyGyro_mean_Z),tBodyGyroJerk_mean_X_avg = mean(tBodyGyroJerk_mean_X),tBodyGyroJerk_mean_Y_avg = mean(tBodyGyroJerk_mean_Y),tBodyGyroJerk_mean_Z_avg = mean(tBodyGyroJerk_mean_Z),tBodyAccMag_mean_avg = mean(tBodyAccMag_mean),tGravityAccMag_mean_avg = mean(tGravityAccMag_mean),tBodyAccJerkMag_mean_avg = mean(tBodyAccJerkMag_mean),tBodyGyroMag_mean_avg = mean(tBodyGyroMag_mean),tBodyGyroJerkMag_mean_avg = mean(tBodyGyroJerkMag_mean),fBodyAcc_mean_X_avg = mean(fBodyAcc_mean_X),fBodyAcc_mean_Y_avg = mean(fBodyAcc_mean_Y),fBodyAcc_mean_Z_avg = mean(fBodyAcc_mean_Z),fBodyAcc_meanFreq_X_avg = mean(fBodyAcc_meanFreq_X),fBodyAcc_meanFreq_Y_avg = mean(fBodyAcc_meanFreq_Y),fBodyAcc_meanFreq_Z_avg = mean(fBodyAcc_meanFreq_Z),fBodyAccJerk_mean_X_avg = mean(fBodyAccJerk_mean_X),fBodyAccJerk_mean_Y_avg = mean(fBodyAccJerk_mean_Y),fBodyAccJerk_mean_Z_avg = mean(fBodyAccJerk_mean_Z),fBodyAccJerk_meanFreq_X_avg = mean(fBodyAccJerk_meanFreq_X),fBodyAccJerk_meanFreq_Y_avg = mean(fBodyAccJerk_meanFreq_Y),fBodyAccJerk_meanFreq_Z_avg = mean(fBodyAccJerk_meanFreq_Z),fBodyGyro_mean_X_avg = mean(fBodyGyro_mean_X),fBodyGyro_mean_Y_avg = mean(fBodyGyro_mean_Y),fBodyGyro_mean_Z_avg = mean(fBodyGyro_mean_Z),fBodyGyro_meanFreq_X_avg = mean(fBodyGyro_meanFreq_X),fBodyGyro_meanFreq_Y_avg = mean(fBodyGyro_meanFreq_Y),fBodyGyro_meanFreq_Z_avg = mean(fBodyGyro_meanFreq_Z),fBodyAccMag_mean_avg = mean(fBodyAccMag_mean),fBodyAccMag_meanFreq_avg = mean(fBodyAccMag_meanFreq),fBodyBodyAccJerkMag_mean_avg = mean(fBodyBodyAccJerkMag_mean),fBodyBodyAccJerkMag_meanFreq_avg = mean(fBodyBodyAccJerkMag_meanFreq),fBodyBodyGyroMag_mean_avg = mean(fBodyBodyGyroMag_mean),fBodyBodyGyroMag_meanFreq_avg = mean(fBodyBodyGyroMag_meanFreq),fBodyBodyGyroJerkMag_mean_avg = mean(fBodyBodyGyroJerkMag_mean),fBodyBodyGyroJerkMag_meanFreq_avg = mean(fBodyBodyGyroJerkMag_meanFreq),tBodyAcc_std_X_avg = mean(tBodyAcc_std_X),tBodyAcc_std_Y_avg = mean(tBodyAcc_std_Y),tBodyAcc_std_Z_avg = mean(tBodyAcc_std_Z),tGravityAcc_std_X_avg = mean(tGravityAcc_std_X),tGravityAcc_std_Y_avg = mean(tGravityAcc_std_Y),tGravityAcc_std_Z_avg = mean(tGravityAcc_std_Z),tBodyAccJerk_std_X_avg = mean(tBodyAccJerk_std_X),tBodyAccJerk_std_Y_avg = mean(tBodyAccJerk_std_Y),tBodyAccJerk_std_Z_avg = mean(tBodyAccJerk_std_Z),tBodyGyro_std_X_avg = mean(tBodyGyro_std_X),tBodyGyro_std_Y_avg = mean(tBodyGyro_std_Y),tBodyGyro_std_Z_avg = mean(tBodyGyro_std_Z),tBodyGyroJerk_std_X_avg = mean(tBodyGyroJerk_std_X),tBodyGyroJerk_std_Y_avg = mean(tBodyGyroJerk_std_Y),tBodyGyroJerk_std_Z_avg = mean(tBodyGyroJerk_std_Z),tBodyAccMag_std_avg = mean(tBodyAccMag_std),tGravityAccMag_std_avg = mean(tGravityAccMag_std),tBodyAccJerkMag_std_avg = mean(tBodyAccJerkMag_std),tBodyGyroMag_std_avg = mean(tBodyGyroMag_std),tBodyGyroJerkMag_std_avg = mean(tBodyGyroJerkMag_std),fBodyAcc_std_X_avg = mean(fBodyAcc_std_X),fBodyAcc_std_Y_avg = mean(fBodyAcc_std_Y),fBodyAcc_std_Z_avg = mean(fBodyAcc_std_Z),fBodyAccJerk_std_X_avg = mean(fBodyAccJerk_std_X),fBodyAccJerk_std_Y_avg = mean(fBodyAccJerk_std_Y),fBodyAccJerk_std_Z_avg = mean(fBodyAccJerk_std_Z),fBodyGyro_std_X_avg = mean(fBodyGyro_std_X),fBodyGyro_std_Y_avg = mean(fBodyGyro_std_Y),fBodyGyro_std_Z_avg = mean(fBodyGyro_std_Z),fBodyAccMag_std_avg = mean(fBodyAccMag_std),fBodyBodyAccJerkMag_std_avg = mean(fBodyBodyAccJerkMag_std),fBodyBodyGyroMag_std_avg = mean(fBodyBodyGyroMag_std),fBodyBodyGyroJerkMag_std_avg = mean(fBodyBodyGyroJerkMag_std)
)

#nrow(tiny_data) 180
#ncol(tiny_data) 81

write.table(tiny_data,"tiny_data_final.txt",row.names=FALSE)

