#Libraries
library(data.table)
library(dplyr)

#Downloading and unziping the data
download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip","dataset.zip")
unzip("dataset.zip")

#1. Merges the training and the test sets to create one data set.
#Read and fusion "x" data
x_train <- read.table("./UCI HAR Dataset/train/X_train.txt")
x_test <- read.table("./UCI HAR Dataset/test/X_test.txt")
x <- rbind(x_train,x_test)

#Read and fusion "y" data
y_train <- read.table("./UCI HAR Dataset/train/Y_train.txt")
y_test <- read.table("./UCI HAR Dataset/test/Y_test.txt")
y <- rbind(y_train,y_test)

#Read and fusion "subject" data
subject_train <- read.table("./UCI HAR Dataset/train/subject_train.txt")
subject_test <- read.table("./UCI HAR Dataset/test/subject_test.txt")
subject <- rbind(subject_train,subject_test)

#Read features names
features <- read.table("./UCI HAR Dataset/features.txt")

#Read activity labels
activity_labels <- read.table("./UCI HAR Dataset/activity_labels.txt")

#Create one data set with identity of each individual + inputs(x) + output(y)
dt1 <- cbind(subject,y,x)

#Remove unneeded datasets to increase available memory
rm(x_train,x_test,x)
rm(y_train,y_test,y)
rm(subject_train,subject_test,subject)

#4. Appropriately labels the data set with descriptive variable names.
# I prefer to change names before filtering data, as it is much easy then to work with the data
# We assign the first two names directly and we get the names of the features from the features dataset, 
#... transforming to lower case and removing special characters
dt4 <- dt1
names(dt4) <- c("subject","activity",gsub("[-(),]","",tolower(as.character(features[,2]))))


#2. Extracts only the measurements on the mean and standard deviation for each measurement.
# We filter all the column names with the word mean or std + the two initial columns that should always be there

dt2<-dt4[,c("subject","activity",grep("mean|std",names(dt4),value=T))]

#3. Uses descriptive activity names to name the activities in the data set
#We need to merge the dataset with the activity_labels data we read before

dt3 <- dt2 %>% 
  merge(activity_labels,by.x="activity",by.y="V1") %>%    #Merge data and labels
  select(-c(activity)) %>%                                #Remove the old label
  rename(activity=V2) %>%                                 #Rename the label as the old one
  select(activity,subject:anglezgravitymean)              #Re-order variables, activity again in the 1st position

#5. From the data set in step 4, creates a second, 
# independent tidy data set with the average of each variable for each activity and each subject.
dt5 <- dt3 %>% melt(c("activity","subject")) %>% dcast(activity + subject ~ variable,mean)

