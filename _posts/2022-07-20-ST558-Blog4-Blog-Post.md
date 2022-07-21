2022-07-20-ST558-Blog4-Blog-Post
================
Owen Snyder
2022-07-20

There are many interesting machine learning methods that we have learned
this semester, some favorites include multiple linear regression,
logistic regression, and various ensemble methods. However, the one that
caught my interest the most was the Boosting Trees method.

The general idea of the Boosting Trees method is that trees are grown
sequentially, each subsequent tree is grown on a modified version of
original data, and predictions are updated as trees grown. To better
visualize this process we can use this step-by-step guide for our
Boosting Tree procedure (note I am leaving out some mathematical
formulas)

1.  Initialize predictors as 0  
2.  Find the residuals (observed-predicted), name that as set *r *
3.  Fit a tree with *d* splits (*d+1* terminal nodes) treating the
    residuals as the response  
4.  Update predictions  
5.  Update residuals for new predictions and repeat *B* times

I will now load some data from a Baseball package (the great Lahman
package) and perform a quick example of a Boosting Tree fit. I will also
be utilizing the `caret` package which can help streamline the process
of many machine learning methods.

``` r
library(Lahman)
library(tidyverse)
library(caret)
## load in the batting data set
##data("Batting")
myBatting <- as_tibble(Batting)

## i will now only filter for years 2018 and up and select the following variables of interest
new.batting <- myBatting %>% filter(yearID>=2018) %>% select(G,AB,R,H,HR,RBI)
new.batting
```

Now that I have some variables of interest, I will split that data into
a training and test data set. This will be an 80/20 split.

``` r
set.seed(558)
split <- createDataPartition(new.batting$G, p = 0.8, list = FALSE)
trainData <- new.batting[split, ]
testData <- new.batting[-split, ]
```

I will now perform a Boosting Tree fit using the `caret` package. This
model will try and predict the number of Home Runs a player could hit
using all other variables as predictors.

``` r
## set a grid of parameters for our Boosted Tree Model
gbmGrid <-  expand.grid(interaction.depth = c(1,2,3,4), 
                        n.trees = c(50,100,150,200), 
                        shrinkage = 0.1,
                        n.minobsinnode = 10)

## note, we are using the training data!
boostFit <- train(HR ~ .,
                  data = trainData,
                  method = "gbm",
                  trControl = trainControl(method = "repeatedcv", number = 5, repeats = 3),
                  preProcess = c("center", "scale"),
                  tuneGrid = gbmGrid,
                  verbose = FALSE)
## print model output
boostFit
```

    ## Stochastic Gradient Boosting 
    ## 
    ## 4938 samples
    ##    5 predictor
    ## 
    ## Pre-processing: centered (5), scaled (5) 
    ## Resampling: Cross-Validated (5 fold, repeated 3 times) 
    ## Summary of sample sizes: 3951, 3950, 3951, 3951, 3949, 3951, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   interaction.depth  n.trees  RMSE      Rsquared   MAE      
    ##   1                   50      2.108066  0.9130213  1.0655231
    ##   1                  100      2.001847  0.9207235  0.9693094
    ##   1                  150      1.951000  0.9245008  0.9293698
    ##   1                  200      1.917286  0.9269949  0.9081438
    ##   2                   50      1.982931  0.9227028  0.9715986
    ##   2                  100      1.869238  0.9306477  0.8821204
    ##   2                  150      1.838578  0.9327628  0.8570318
    ##   2                  200      1.827719  0.9335301  0.8466650
    ##   3                   50      1.886762  0.9296062  0.9096211
    ##   3                  100      1.821828  0.9339602  0.8480001
    ##   3                  150      1.817434  0.9343722  0.8343736
    ##   3                  200      1.822312  0.9340690  0.8316232
    ##   4                   50      1.862246  0.9312339  0.8911316
    ##   4                  100      1.823992  0.9338024  0.8415561
    ##   4                  150      1.824829  0.9337826  0.8311070
    ##   4                  200      1.833449  0.9332807  0.8285311
    ## 
    ## Tuning parameter 'shrinkage' was held constant at a value of 0.1
    ## Tuning parameter 'n.minobsinnode'
    ##  was held constant at a value of 10
    ## RMSE was used to select the optimal model using the smallest value.
    ## The final values used for the model were n.trees = 150, interaction.depth = 3, shrinkage = 0.1
    ##  and n.minobsinnode = 10.

Now we will use the RMSE metric to determine which model was best.
Generally, we choose the model with the **lowest** RMSE. Also to note,
there are many other metrics to choose from.

``` r
boostFit$results
which.min(boostFit$results$RMSE)
```

    ## [1] 11

From the output of 11, we see that Model 11 is our best fit model
according to RMSE.
