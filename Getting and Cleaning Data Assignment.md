#Download Data

library(dplyr)

fileurl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileurl,"UCIHARDataset.zip", mode="wb")

datafile <-"UCIHARDataset.zip"
unzip(datafile)




#Read Data

list.files("Home/maxlearn")

features<- read.table("UCI HAR Dataset/features.txt",as.is = TRUE)
activity_labels<- read.table("UCI HAR Dataset/activity_labels.txt")

train_x <- read.table("UCI HAR Dataset/train/X_train.txt")
train_y <- read.table("UCI HAR Dataset/train/y_train.txt")
train_subject <- read.table("UCI HAR Dataset/train/subject_train.txt")

test_x <- read.table("UCI HAR Dataset/test/X_test.txt")
test_y <- read.table("UCI HAR Dataset/test/y_test.txt")
test_subject <- read.table("UCI HAR Dataset/test/subject_test.txt")

#merge into one table

x<-rbind(train_x,test_x)
colnames(x)<-c(features[,2])

y<-rbind(train_y,test_y)
colnames(y)<-c("activity")

subject<-rbind(train_subject,test_subject)
colnames(subject)<-c("subject")

merged_activities<-cbind(subject,y,x)

#Extrac only the measurements on the mean and standard deviation for each measurement

colmns<-grepl("subject|actvity|mean|std",colnames(merged_activities))

merged_activities1<-merged_activities[,colmns]


