---
title       : Developing Data Products
subtitle    : Assignment 1
author      : Joseph Walkenhorst
job         : Business Analyst/Data Scientist
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Understanding Logistic Regression Predictions

- Ever wondered how to interpret the probabilistic predictions made by a logistic regression model?

![width](questions.jpg)

- Using my app "Understanding Logistic Regression Predictions", now you can!

--- .class #id 

## Source Data

- The source data used for this app was the training data available from the Kaggle web site for the Titanic competition. 
- This competition provides data for each passenger on the 1912 maiden voyage of the RMS Titanic passenger ship, including whether they survived the ship colliding with an ice berg and sinking.
- The model was trained using 70% of the training data, with the other 30% used to compute the accuracy statistics for the app:

```r
library(caret)
titanicTrain = read.csv("titanic train.csv")
titanicTrain$Survived = as.factor(titanicTrain$Survived)
trainBool = createDataPartition(titanicTrain$Survived, p=0.7, list=FALSE)
trainSet = titanicTrain[trainBool,]
testSet = titanicTrain[-trainBool,]
```

--- .class #id 

## Defining the Model
 - The model uses the passenger class, sex and age to predict the probability of survival:

```r
fit = glm(Survived~Pclass+Sex+SibSp, data=trainSet, family="binomial")
```

```
##               Estimate Std. Error    z value     Pr(>|z|)
## (Intercept)  3.2891914  0.3606529   9.120102 7.505348e-20
## Pclass      -0.8732780  0.1265815  -6.898941 5.239171e-12
## Sexmale     -2.6901579  0.2229434 -12.066551 1.586449e-33
## SibSp       -0.2872521  0.1063234  -2.701683 6.898951e-03
```

--- .class #id 

## Using the App

- Simply tweak the threshold to see how the performance of the model is affected.
- Key statistical measures are given and a ROC curve is shown with the location of the specificity-sensitivity point for the given threshold.
- You can find the app here: https://walkenhorst.shinyapps.io/Assignment
