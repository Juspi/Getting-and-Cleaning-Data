#Reads and binds data
train<-read.csv("UCI Har Dataset/train/X_train.txt", sep="", header=FALSE)
trainlabel<-read.csv("UCI Har Dataset/train/y_train.txt", sep="", header=FALSE)
trainsubject<-read.csv("UCI Har Dataset/train/subject_train.txt", sep="", header=FALSE)

test<-read.csv("UCI Har Dataset/test/X_test.txt", sep="", header=FALSE)
testlabel<-read.csv("UCI Har Dataset/test/y_test.txt", sep="", header=FALSE)
testsubject<-read.csv("UCI Har Dataset/test/subject_test.txt", sep="", header=FALSE)

bindeddata<-rbind(train, test)
bindedlabel<-rbind(trainlabel, testlabel)
bindedsubject<-rbind(trainsubject, testsubject)

#Reads features and extracts only the measurements on the mean and standard
features <- read.csv("UCI Har Dataset/features.txt", sep="", header=FALSE)

meanStdvalues <- grep("mean\\(\\)|std\\(\\)", features[, 2])

bindeddata <- bindeddata[, meanStdvalues]

names(bindeddata) <- gsub("\\(\\)", "", features[meanStdarvot, 2]) # remove "()"
names(bindeddata) <- gsub("mean", "Mean", names(bindeddata)) # capitalize M
names(bindeddata) <- gsub("std", "Std", names(bindeddata)) # capitalize S
names(bindeddata) <- gsub("[-()]", "", names(bindeddata)) # remove "-" in column names

#Uses descriptive activity names to name the activities in the data set
activity <- read.csv("UCI Har Dataset/activity_labels.txt", sep="", header=FALSE)

activity[, 2] <- tolower(gsub("_", "", activity[, 2]))
substr(activity[2, 2], 8, 8) <- toupper(substr(activity[2, 2], 8, 8))
substr(activity[3, 2], 8, 8) <- toupper(substr(activity[3, 2], 8, 8))
activitylabel <- activity[bindedlabel[, 1], 2]
bindedlabel[, 1] <- activitylabel
names(bindedlabel) <- "activity"
names(bindedsubject) <- "subject"

#Binds the data and writes final_data 
finaldata <- cbind(bindedsubject, bindedlabel, bindeddata)
write.table(finaldata, "tidy_data.txt")
