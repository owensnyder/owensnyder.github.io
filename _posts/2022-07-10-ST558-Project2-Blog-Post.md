2022-07-10-ST558-Project2-Blog-Post
================
Owen Snyder
2022-07-11

## Links to Project

Link to the Github page:
<https://abmckeon.github.io/Project2McKeonSnyder/>  
Link to the Github repo:
<https://github.com/abmckeon/Project2McKeonSnyder>

## The Scope of Project 2

Ashlee and I set out to create reports for all six data channels within
the online news popularity data set with the number of shares being our
target variable of interest. The reports include data manipulation, a
basic exploratory data analysis, and a model fitting procedure.

However, before we started, it was important that we figured out which
variables we wanted to include in our EDA and model fitting. Once we
described our variables of interest, we then decided to create variables
that would encompass all the different subsets of data channel and
weekday. This would make automation and EDA much more efficient. We then
had a workable data set that we were happy with which allowed us to then
split the data into a training and test set with a 70/30 split. The
training data will be used for analysis and the test set will be used to
compare our models. Next, we started our data analysis which included
scatterplots, boxplots, and histograms along with contingency tables and
summary statistics that describe how our Shares variable is associated
with different predictor variables.

After we conducted an EDA, our next task was to use our variables of
interest and deploy them into four different regression models. Ashlee
and I each made one linear regression model, along with her Random
Forest model and my Boosted Tree model. Just like the EDA, the
regression models are automated for each of the six data channels. Now
that we had our models built, we decided that we would use RMSE as our
metric to determine the best model. Thus, we identified the lowest RMSE
for each model fit and a winner was declared for each channel.

## What would I do differently?

Something I would do differently is use more variables than we included
for our models. Part of the reason we did not include so many was that
the efficiency of automating the reports greatly improved with less
variables. However, we did feel like the variables we included were some
of the most commonly referenced/used. If I had better computing power or
“unlimited” resources, using a lot more variables and building more
complex models would have been optimal. Another thing I would do
differently is discuss the graphical procedures more in depth. I think
some of these variables got a bit confusing especially with employing
certain graph types to them. Part of this was due to there being so much
data and a very wide range of values. In fact, I would have liked to
include some ST503 topics of outlier removal to help improve some of the
visuals on the graphs. However, I did feel like my histogram,
scatterplot (links v. shares), and boxplots did a good job of
summarizing some of the variables we used.

## What was the most difficult part for me?

Stemming from what I said above, I think finding the right variables to
use and figuring out which plots would look best for the data were the
most difficult parts for me. These difficulties could have been
capitalized on if I had employed some of my previous statistical
knowledge on the data. However, with a limited amount of time, I wanted
to ensure that I had made the requirements in the scope of this course.
In fact, I am very excited to go back into this project in a few weeks
and tweak things with my knowledge from past coursework.

## What are my big take-aways from this project?

One of the biggest takeaways from this project is that I really enjoy
working with R and on these projects that we are assigned. I feel like
these skills are very important and I can’t wait to get started on my
own projects in a few weeks. I was also a lot more comfortable using
GitHub which helped the project documentation run much smoother.
