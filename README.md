# NFL-Big-Data-Bowl
A machine learning model which predicted the number of yards a rushing player would gain on a given play. \
Team: Ishant Sharma and Keshuv Bagaria

__Understanding the Dataset:__\
 The training data that was provided to us had 510,000 tuples and 49 columns. 
 This data has been collected over the 2017 and 2018 regular season, i.e, excluding playoff games. 
 Each play in the data has 22 tuples corresponding to the 22 players on the field. 
 The submissions were evaluated by the Continuous Ranked Probability Score. 
 For the submission, we had to predict the number of yards gained for each PlayId,  
 and for each PlayId, we would have 199 columns( Yards-99 to Yards99 ) which would indicate that the player gains less than or equal to that many yards on the play. 
 For example, if a player gains 3 yards on a play, every column after Yards3 would contain 1. 
 
__Reducing Unwanted columns:__\
 We were given 49 parameters to work with and predict the yards a rusher would gain or lose in each place. We dropped some of the features that we found that did not work with our dataset based on plotting a feature correlation histogram and our NFL knowledge. 
We dropped the following features: 
  1. NflId 
  1. DisplayName
  1. NflIdRusher
  1. JerseyNumber
  1. GameClock
  1. FieldPosition
  1. TimeHandoff
  1. TimeSnap
  1. PlayerCollegeName
  1. Stadium
  1. StadiumType
  1. Location
  1. GameWeather
  1. Temperature
  1. Humidity
  1. WindDirection
  1. WindSpeed
  1. Turf
  1. Week
  
__Feature Engineering:__\
  We started our feature engineering by one-hot encoding of features that did not need any pre-processing and features that could be categorized easily by that technique. 
  So, we carried out __one hot encoding__ on the following features: 
  1. Dir
  1. Team
  1. PossessionTeam
  1. DefensePersonnel
  1. PlayDirection
  1. Position
  1. VisitorTeamAbbr
  1. HomeTeamAbbr
  1. OffenseFormation

__New Features Created:__\
  Then we decided to create some of our own features that we thought would help in predicting the yards gained by the rusher. We created these features based on our NFL knowledge. We tried to narrow down on some of the aspects of the game that we thought influenced the success or failure of a rushing play. List of features that we created along with a description of how we did it:
  1. WideReceivers: This feature was derived from the feature OffensePersonnel. It gives us the number of wide receivers in the offense. We decided to use this because the number of wide receivers in the offense often indicates to the defense whether the play would be a pass or a rush. Since all the plays in the data are rushing plays, higher number of wide receivers in the offense could trick the defense. Hence, allowing more yards gained on the play. 
  1. TightEnds: This feature was derived from the feature OffensePersonnel. It gives us the number of tight ends in the offense. A tight end can provide blocks and receive passes as well. We wanted to create this feature for exploratory reasons.
  1. RusherAge: This feature was derived from the feature PlayerBirthDate. It is simply the age of the rushing
  1. BMI: This feature was derived from PlayerHeight and PlayerWeight. It reduces the dimensions of our model. 
  1. Qb_To_LOS: This feature is the distance between the X, Y of the player at the center(at the line of scrimmage) and X, Y of the quarterback.
  1. Rusher_To_LOS:This feature is the distance between the X, Y of the player at the center(at the line of scrimmage) and X, Y of the rusher.
  1. x_Velocity: Horizontal component of the velocity of the rusher.
  1. y_Velocity: Vertical component of the velocity of the rusher.
  

__Model Training, Testing, and Validation:__\
We divide the training set into 70% training set and 30% validation set. However, it is important to note that when creating a kaggle notebook to predict the test set, we trained our model on the full training set. 

We used KNN and RandomForests with various hyperparameters. For Hyperparameter tuning of RandomForests, we used K-fold(n = 5) cross validation along with grid search. In our grid search, the parameters were: Estimators = 100, 50, 30, and max_depth = 30, 20, 10. 

Upon testing with our validation dataset, we got KNN score of 0.08750365817968979
And the validation score of the best model out of the RandomForest Grid search was 0.15. The best estimators turned out to be 50 and the best max_depth turned out to be 10 

  

