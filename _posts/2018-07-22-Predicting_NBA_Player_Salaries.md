# Creating a Salary Estimator

For my next project at Metis, the ask was to create a modelling tool using linear regression. With NBA free agency in full swing, I set out to build a tool to help price our free agents and estimate their average annual salary from their previous year's performance. 


## The Data

To do this, I gathered data from multiple sports related sites through webscraping using BeautifulSoup. 
[Basketball-Reference](http://www.basketball-reference.com) for stats
[Spotrac](https://www.spotrac.com/nba/contracts/) for contract details

For our first version of this tool, we made the following assumptions. 
  - I studied only contract year performance. The idea being that the contract year's performance will have the highest impact on new contracts.
  - I looked at only active contracts. (Older and expired contracts will require further data wrangling)
  - Rookie contracts were not used. Since we are looking at free agent contracts, rookie contracts were ignored. 
  - Average Annual Salary was used instead of total contract values to ensure all calculations were on the same scale.

## Creating the model
After bringing in all the data and cleaning it. The first step was to look at the features we had and see if there were anything interesting using Seaborn heatmap and pairplot functions.

![](https://github.com/alfordlew/alfordlew.github.io/blob/master/images/heatmap.png?raw=true "Heat Map")


![](https://github.com/alfordlew/alfordlew.github.io/blob/master/images/pairplot.png?raw=true "Pair plot")


After removing some very obvious collinear features, I began by running all the features as is through our Linear, Lasso, and Ridge Regressions. I targeted root mean squared error in this project to try to make my model as accurate as possible. Our first models returned root mean squared errors of ~$7.6M. This was extremely high. 

I continued to review the features and explored their p-values in our linear regression as well as look at each feature's pairplot with the actual average salary. Ultimately, I removed features that were not useful and expanded some features to their 2nd degree. 

This lead to reducing our mean squared errors to ~$5.6M for our current model. Here is the prediction error plot for the current model.

![](https://github.com/alfordlew/alfordlew.github.io/blob/master/images/Current_model_pred_act.png?raw=true "Error plot")

I went with the linear model so that we can still maintain some interpretability with our results. For example, it is interesting to note that assists were the most highly correleated with pay, followed by points. One would think points per game would be the most deciding factor. 


## Model Review / Next Steps

Our model currently still has work to do. If you look at the error plot, you can see there are some misses near the top end salaris. It suggests that my model is missing a feature that seems to seperate the max contract salaries vs some of the lower contracts. I believe adding some accolades categories may help to alleviate some of the discrepancies. For example, adding in all-star selection, MVP, and 1st-team NBA as features may help make this model better in the future. 


## Playing with the Model

I ultimately tested my model with one of the Chicago Bull's newest signings. 

![](https://github.com/alfordlew/alfordlew.github.io/blob/master/images/lavine.jpg?raw=true "Lavine")

Zach LaVine signed a $78M 4/yr contract with Bulls this summer. This comes out to $19.5M annually. Most pundits viewed this signing as too high of a price to pay for LaVine's services. So I ran his numbers through the model and his expected salary was $13.6M. My model agrees.



