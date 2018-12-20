# hockeyGoals
A classifier that determines what factors impact a goal being scored in a hockey game.

Hockey, unlike other sports has much more to do with luck than pure skill. One of my favorite things about hockey IS the variability. One of the things that makes hockey so special are the on-ice factors players can’t control. One of the most significant and unique to the sport are bounces the puck takes on the ice. There can be referees in the way, rough patches in ice, and other players that can impact the movement of the puck. Adding the skills of an individual goalie playing in a game, there are many factors that make hockey incredibly hard to predict. 

Another example of hockey’s variability, parity in the playoffs. Hockey has had more underdog teams make it to the playoffs and win it all than in other sports like basketball. Of the big 5 north American tam sports, basketball can attribute most league standings to pure skill and hockey has skill account for less than 50% of team standings. 

This project hopes to investigate if we can predict a player scoring a goal, based on his other game stats like giveaways and face-offs. 

Why this problem? 

There have been several others who’ve tried to predict the outcome of a single game. With so much of hockey wins composed of luck, I wanted to take a deeper look at those composed of skill. I wanted to tackle the problem of predicting individual goals based on the other metric’s of a player’s performance within one game.

This dataset does not factor in the player’s overall stats or overall team stats. I took a player by player approach to prediction because there are on average 18-20 players in a game. This is a slightly less complex problem because the algorithm has less dense data to consider.  

Neural Network Architecture

For this project I created a deep neural network with 4 dense layers and 3 dropout layers that had a learning rate of 0.1. After fitting my model to the training data with a batch size of 7 and 100 epochs I used a GridSearch algorithm to help me find the best parameters. After using some discoveries from the GridSearchCV I retrained my model with the batch size of 20 for 500 epochs. I also and added dropout layers to combat the extreme overfitting my first models had, they were only 26% accurate on the test set before dropout. 

Results:

Undeniably I was able to create a pretty skilled model. While the neural network was able to score 91% accuracy on the test set, that doesn’t show a full picture of the data. The model’s f1 score was 62% which is more along the lines of the state of the art single game hockey predictors. This is an important distinction because while I had 00k rows of data, only ~12k represented goals while the other ~76k represented players who did not score a goal in a particular game. Since the imbalance between my classes is significant the F1 score tacks into account both precision and recall. 

 For my data I was able to achieve a 91% AUC score. This does show signs of an effective model, but we have to keep in mind the null accuracy.

The null accuracy for the player stats data is 86%. This number represents the percent of correct predictions my algorithm would guess if it made a guess for the class 0 or no goal 100% of the time. This makes sense when we think about the imbalanced classes. If there are 76k rows where the correct answer is 0 and only 12k when the correct answer is 1, my model needs to perform better than .86% to be better than a random guess.

With some problems we’re more concerned with the rate of misclassifications (healthcare, finance, etc) however in our case the classification error is not our biggest factor. The DNN created only misclassifies goals 8% of the time. 

What’s Next?

I would like to take a deeper look into model parameters, first to see if GridSearch can accurately help find a good number or layers for the model. I want to combine the data from each player and compare it to the players of his “line” or other forwards from the same team who usually play at the same time. This would give a better understanding of how lines in hockey do well or poorly together. This also opens some investigation into taking individual player statistics into account for single game predictions. My goal is to create more accurate single game predictions by looking at the skill of each player in the game and either some amount of noise or a Bayesian model for predicting luck better in hockey. 

