# Word-Cup-2022-Prediction

## Data analysis 

According to the past matches record starting from 1932 up to 2014, there’re totally 851 records. Each of them records the information like time, place and number of attendances. Of course, the most important ones are the home team and away time and their final goals. 

 
## Data preparation 

### Main Data: 

1930-2014 FIFA World Cup history data: From Kaggle (For Training) 

2022 FIFA World Cup schedule data: From FIFA official website (For Predicting) 


### Secondary data: 

GDP&Population: Representing a kind of status of a country, which may have effects on predicting. 

FIFA Rank: FIFA rank is a public measure of their actual strength in football, posted by International Federation of Association Football. This would be an influential feature. 

Followed by some suggestions searched online, we also collected some other features like oddest. By observing the accuracy of prediction of each learning algorithm, finally we only kept FIFA rank as one of the training features. 


## Data preprocessing 

In this section, we dropped all error codes of raw csv file, updated the format of data, merged all the data into one single file and made them numerical. For example, the score of two teams in a game can be combined into one data, which is called different goals between two teams.  

Additionally, we did some visualizations of the data. You can see figures of history winners, history of runner-up's, history of thirds, World Cup winning counts, match outcomes by home and away teams and goals in World Cup of all participated countries. 


## Data mining 

### Feature selection: 

For feature selection, we considered potential factors such as population, GDP, odds and FIFA ranking. Through the importance of comparison characteristics of basic model training, we find that FIFA ranking and odds are the most influential factors, while GDP and population differences have little or even negative impact on results. One intuitive explanation is that countries like Brazil and Argentina have a much lower GDP, per capita GDP and population size than the United States. In the World Cup, Brazil and Argentina have long been favorites, while the United States doesn't seem strong. There are many factors that can affect a country's football strength, such as race, climate, culture and so on. It is not possible to consider too many influencing factors here, we removed feature columns like GDP, population and use the FIFA ranking as an important reference. Due to the limitations of data collection, we do not consider the odds for the time being, although it’s a very valuable influence factor for reference. Considering the low dimension of the features, we analyzed the teams based on historical data and added feature columns including the team's historical World Cup win rate, historical goals per game and historical goal difference per game. 

 
### Model Training: 

Considering the large span of historical data years, the reference value of early data (such as data before 2000) may be limited, we added a sample weight column to assign increasing weights to the sample data by year, for example, the sample weight assignment of 2014 is 1, while that of 1930 is 0.45. Through experiments, it can be found that the influence range of sample weight on the overall accuracy of the model is controlled within 0.01-0.05. It seems to have little impact, but it also improves the prediction accuracy to a certain extent. It is believed that sample weight allocation will bring better prediction performance when the data volume is large enough. 

We use a variety of machine learning algorithms for horizontal comparison, such as KNN, logistic regression, SVM, Adaboost, Random Forest, decision tree, etc. For the model prediction results, since it’s the classifier which predicts the highest accuracy, so confusion matrix and ROC graph were drawn for analysis. 

From both ROC curve and confusion matrix you can see that, actually our model has a very good predictions for win and lose class, but it’s hard for it to predict a ‘draw’ result and that’s the main limitation of accuracy.  

In the past trials, we also tried some adjustments like increasing the sample weights of draw data, but there was no obvious effect. This is the hardest not-solved problem left in our project, and if there is more time, it is also one of the parts that need to be improved in future work. 

### Model Analysis: 

By comparing the prediction results of various models, we found that the prediction accuracy of random forest was close to 70%, while the prediction accuracy of other models, such as logistic regression and SVM, did not exceed 60%. We have reason to believe that under the condition of more perfect covariate variables such as odds, FIFA world cup ranking and team data, random forest can show higher accuracy. The random forest first builds many decision trees on the training data, and then summarizes the prediction of each decision tree by taking the mode of the predicted classes. Compared with the conventional decision tree, the random forest reduces the tendency of overfitting. Under the same feature selection, the random forest proved to provide very satisfactory results, which will prompt us to apply the random forest model to predict the upcoming 2022 FIFA World Cup. 

 
## Result display 

In terms of predicting the results of the 2022 FIFA World Cup, we predict the results of the group stages, eighth finals, quarter finals, semi-finals and the finals, according to the official FIFA World Cup rules. According to our predictions, Brazil will win the 2022 World Cup, while traditional powerhouses such as Germany, France, Italy and the Netherlands have all finished well in the group stages, eighth finals and quarter finals. The considerable prediction results are generally consistent with the comprehensive strength of each team, which also enhances the interpretability of our model on the other hand. 

 

## Future Work 

Future expandable work is mainly reflected in the expansion of data dimensions, such as the total player value of World Cup teams in each year, odds, average age of players, and the statistical data of ordinary leagues before the World Cup. Based on the rich data, we can expand from predicting winning categories to predicting richer outcomes such as the final score and the probability of a team winning. 
