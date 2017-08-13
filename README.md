# Probiotic_prediction

Data was obtained from: ftp://ftp.microbio.me/AmericanGut/ag-April-26-2017/07-taxa.zip

Dataset was manually curated to remove redundant variables, no fecal samplas and low variance data

Need for probiotic was defined based on the ratio between Firmicutes and Bacteroidetes.

Discretization:

if FBratio>= 1.0 and Fbratio <= 5.6:
  Probiotic_need = Healthy
 else:
  Probiotic_need = Yes

# Analyses were performed in R:
  
library("e1071")
library("party")

# Import dataset

raw <- read.csv("ag-cleaned_L2.txt", header=TRUE, sep="\t")


# Select fecal samples

fecal <- raw[raw$TITLE_BODY_SITE=="AGP-FECAL",]


# Exclude missing data

agut <- na.exclude(fecal)


# Set training and test set

set.seed(1234)

train.index <- sample(seq_len(nrow(agut)), size = 7500)

train.set <- agut[train.index, ]
test.set <- agut[-train.index, ]
 



# Conditional inference tree

cit <- ctree(Probiotic_need~., train.set, control=ctree_control(testtype = "Bonferroni", mincriterion=0.95, maxdepth=4))

plot(cit)

predCIT <- predict(cit, newdata=test.set)

conf_matrix_CUT <- table(predCIT, test.set$Probiotic_need)

write.csv(conf_matrix_CIT, "confusionCIT.csv")





# Naive Bayes

nBayes <- naiveBayes(Probiotic_need~., train.set)

predBayes <- predict(nBayes, newdata=test.set)

conf_matrix_nB <- table(predBayes, test.set$Probiotic_need)

write.csv(conf_matrix_nB, "confusionBayes.csv")
