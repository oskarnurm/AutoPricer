# AutoPricer

## Background and motivation
When buying a car it can be difficult to assess whether the price is too high, or if you are selling your car for a price too low.

We wanted to create a model that could as accurately as possible predict the price of an arbitrary car with a model year no older than ~1990. We went about achieving this with the dataset (Car Features and MSRP | Kaggle). The idea was to train a model on a car's more “basal” features like cylinder amount, car brand, driven wheels etc. We hoped to see what underlying features that would or would not have a great influence on a car’s price and to have some kind of more “objective” measurement of a car's value. The results of this project could be used by car retailers to set the price of their cars more effectively as well as consumers to determine whether the price of a car is fair.

## Dataset
The dataset we used consists of 11684 rows, each row representing a unique car. Each row has 16 columns.

The dataset was put together by the user Cooperunion on Kaggle in 2017. Thus the dataset contains cars up to 2017 and the price is also represented by 2017 prices. Also noteworthy is that Edmunds is an american company, thus the price is denoted in USD.

The data was mostly scraped from the car retailer Edmunds. On their website they have an application that lets users appraise their cars based on different parameters. These parameters are some of the features found in our dataset.

The feature “Popularity” was scraped from twitter, representing how much a specific car is talked about.

## Methodology
The main goal with this project was to predict the price of cars by using the aforementioned dataset, using different methods for Unsupervised- & Supervised learning, dimensionality reduction/feature selection. Before starting with any kind of machine learning we explored our dataset, ultimately cleaning it as you will see further down in the code section of the report. The Unsupervised methods we used were clustering, in particular we tried KModes & KPrototypes. KPrototypes being a combination between KModes and KMeans clustering. This was chosen because it can be used on datasets with mixed data types, to see if we could see any similarities between our data points. For our numerical features we used principal component analysis (PCA) to visualise and also to reduce dimensions.

To actually predict the price we used different regression algorithms, specifically “least absolute shrinkage and selection operator” (LASSO), Linear Regression & Random Forest Regression. Lasso being a modified Linear Regression, that tries to use as few parameters as possible to fit a line. The Random Forest is a lot of decision trees that predict the price and then returns the average of the predictions.

Before actually applying the different algorithms we split the dataset into a training set, an evaluation set and a test set. The evaluation set was used to fine-tune the parameters before testing it on the test set. This in order to get a better estimate of how well our model would generalize to new, unseen data if ever to be deployed into the real world. Before actually training our model we also One Hot Encoded (OHE) our categorical features, meaning that every categorical value becomes a feature of a data point with the value 0 or 1. E.G if a datapoint has the make-value “Volvo” it instead gets a feature called “Is Volvo” with the value 1 (it also gets for example a feature called “Is Ford” with the value 0).

To evaluate the project we mainly looked at the resulting RMSE (Root of the mean of the square error) of the predictions and also the R^2 score, which describes the amount of variance that can be described by the regression model. To evaluate we looked at the prediction of the actual price and the logarithmic price.

## Conclusion
Our model performs admirably considering the huge difference between many of the cars and their idiosyncrasies. The RMSE is not insignificant since it exceeds the list price of some of the cars in the dataset however when the range in price (and very sparse in the higher price classes) is this wide then minimising the mean squared error becomes very difficult.
