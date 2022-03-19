# Football-Analysis

1.  Research/Business goal. 

Our goal is to use data mining to find insightful statistics and patterns for the soccer leagues and players data. We aim to compare different metrics to find interesting inferences for different players and teams in various soccer leagues. 

2.  Queries worked on. 

    Best and worst performing teams and players in the world. 

    Best improving teams and players over time. 

    To check for team and player performances in a season that are outliers. 

    Using metrics to cluster good players/teams from average players/teams. 
       ID - Nominal data with a unique value assigned to everyone in the dataset. (Integer) 

# Data Attributes:  
    country_id - Nominal data value.  (integer) 

    league_id - Nominal data value. (integer) 

    Season - Interval data value. (string) 

    Stage – Ratio data value. (integer) 

    Date – Interval data value. (Datetime) 

    Match_id - a nominal data with a unique value assigned to everyone in the dataset. (integer) 

    Home team_id - Nominal data value. (integer)  

    Away Team_id - Nominal data value. (integer) 

    Home team goals - Ratio data value. (Integer) 

    Away Team goals- Ratio data value.  (Integer) 

    Names of Players - Nominal data value. (String) 
    Below is the null value summary of our dataset: 
Only buildUpPlayDribbling has missing values in our dataset. 

![image](https://user-images.githubusercontent.com/43316158/159100887-998e3fd9-0d8d-40fa-89b3-d6ce25a5082c.png)

# Outlier and Skewness Summary: 

We used histograms to check if there were any outlier in our datasets and we did not find any outliers. But we did notice that some of our attributes were slightly skewed for which normalizing did not make a difference and hence we left it as it is. We also calculate the skewness of all the attributes in our dataset, for which we saw minimal skewness and hence did not use any normalizing technique. 

 

Skewness values – As skewness is less, we did not need to use box-cox transformation. We ignore team_api_id as it is nominal and doesn’t make sense to normalize. Below is the mentioned skewness for all attributes. 

![image](https://user-images.githubusercontent.com/43316158/159100903-4152155d-a561-4880-b006-c4d31512ec04.png)

Below is an example of histograms before and after using min-max normalization for slightly skewed attribute buildUpPlayPassing: 
![image](https://user-images.githubusercontent.com/43316158/159100914-f5ead35a-659f-4cd5-a113-74d4eb9f10df.png)
![image](https://user-images.githubusercontent.com/43316158/159100920-e66674e9-dc61-4406-b01b-1005c4866b50.png)

As there is minimal change in distribution, we did not use any normalization and we see the exact same thing for other slightly skewed attributes. 

Imputing missing values: 

In our soccer dataset we had 969 missing values for attribute buildupPlayDribbling. 
![image](https://user-images.githubusercontent.com/43316158/159100937-c958f3da-5fcd-40ff-b64b-44cff909645b.png)

We have another attribute buildupPlayDribblingClass where we have 3 categorical values which are Little, Normal and Lots.  

The steps we decided to impute the missing values are mentioned below: 

    The mean of buildupPlayDribbling, based on each category in buildupDribblingClass (Little, Normal and Lots) was calculated. 

    For every missing value in buildupPlayDribbling we find its corresponding buildupDribblingClass value. 

    For the corresponding buildupDribblingClass class we fill the mean value we calculated before. 

 

After step 3 we successfully imputed the missing values with the means of buildupPlayDribbling based on the value of buildupDribblingClass. 

 

The above steps were the best way from our point of view to impute the missing values.

Steps 
For the standardization of Data set we had removed all the categorical values from our dataset and had a total of 9 columns to apply PCA on.
Then we normalize our Data set using standard scaler which transforms it in the range of values [-1,1].
Using this we started applying the PCA algorithm changing the number of total components the algorithm is applied on.

| n      | Variance ratio       | 
| ------------- |:-------------:|
| 1 | 24.406673639137065 |
| 2 | 41.84661049018683 |
| 3 | 53.35834531220723 |
| 4 | 63.989262713048774 |
| 5 | 73.60653911557237 |
| 6 | 81.58585532621117 |
| 7 | 89.31171697394592 |
| 8 | 95.42032183185319 |
| 9 | 100 |

n	Variance ratio
1	24.406673639137065
2	41.84661049018683
3	53.35834531220723
4	63.989262713048774
5	73.60653911557237
6	81.58585532621117
7	89.31171697394592
8	95.42032183185319
9	100

Graphs showing cumulative frequency for different number of total components. 
![image](https://user-images.githubusercontent.com/43316158/159101169-d5b6c7f9-64a2-4555-98b9-4f900398baf6.png)

![image](https://user-images.githubusercontent.com/43316158/159101177-6df911c9-790c-4506-8d41-3fcfaa643a46.png)
For the component number 5 we got a explained variance ratio of 73.6 % and although it increased for columns more than 5 but for the added complexity it is not efficient enough for our model compared to 5 components hence we have taken our total components as 5 for the PCA algorithm.  
BIPLOT for 5 principal components

![image](https://user-images.githubusercontent.com/43316158/159101192-dee5d42d-9fee-4188-a20d-3c0bc7cc3ca7.png)
3D BIPLOT for 5 principal components

![image](https://user-images.githubusercontent.com/43316158/159101207-472b7571-3554-4801-9375-91397884c19e.png)

1. Finding player positions using attributes
The statistical method used to address this query is K-means clustering. 
On the y-axis we have finishing rating, and on the x-axis we have standing tackling rating of the players from the dataset.
The scatterplot for the same is plotted below:

![image](https://user-images.githubusercontent.com/43316158/159101232-d1c4ba60-2f0a-47e3-9a14-6d14d9f516de.png)
After applying K-means clustering the clusters looks like plotted below.

![image](https://user-images.githubusercontent.com/43316158/159101245-ab68d04f-9d4d-4987-b41b-fd73dbaca1c9.png)

Using this clustering technique as mentioned before we will divide it into four clusters (to map goal-keepers, defenders, midfielders and strikers into clusters). 
•	The players with great finishing skills and low standing tackle, in this case the cyan region are the strikers as they are supposed to have good finishing.
•	The players with high finishing skills as well as high rating for standard tackle in this case the blue region is classified as midfielders as midfielders are supposed to be good at both tackling and finishing.
•	The players with high standing tackle and low finishing skills in this case the yellow region is classified as defenders as defenders are primarily required to defend and tackle opponent attackers.
•	The players with low finishing skills and low standing tackle in this case the red region are goalkeepers as finishing and standing tackle are not needed for a goalkeeper.

2. Best and worst performing teams and players in the English Premier League.
For this query we first plot a scatterplot for goals scored vs goals conceded in the 2008-09 premier league season for all 20 teams in the division. Here we use hierarchical clustering to separate the strong teams from the average/weak teams.
![image](https://user-images.githubusercontent.com/43316158/159101262-9991fdb4-bc6c-4fe7-8532-bf95c9e897cf.png)

•	The clusters in blue are strong teams as they have conceded the least number of goals and scored the most of them. 
•	The average teams are in yellow as these teams have scored and conceded the average amount of goals. 
•	The weakest teams are in pink as these teams have scored the least goals and conceded the most goals throughout the season

The Teams for the same can be identified below:
![image](https://user-images.githubusercontent.com/43316158/159101281-9ebdb228-b177-4a81-8c2d-d892a499cda4.png)

![image](https://user-images.githubusercontent.com/43316158/159101270-a4cdda19-47f6-4d07-8786-548617bacbfb.png)

3. Best improving and non-improving teams over time.
Linear regression to find the performance of the team throughout the seasons.
Below is a scatterplot of Goal Difference of Manchester united throughout the seasons. 
Goal Difference = Goal Scored – Goal conceded.

![image](https://user-images.githubusercontent.com/43316158/159101309-e44b8eb1-7558-4784-bfe3-46392133273e.png)

Calculating the linear Regression lines of various teams based on goal difference and plotting them below:

![image](https://user-images.githubusercontent.com/43316158/159101356-67ec8e75-c418-4df5-8c9e-1dd5b8fed6ca.png)

From the plots it can be seen Manchester United and Chelsea have steeper slopes and their performances have been decreasing over the past few seasons. Even Arsenal have had a downward trajectory in terms of performances in the past few seasons.

Liverpool is on similar paths as Manchester United and Chelsea, whereas Manchester City and Tottenham have been the better teams recently.
![image](https://user-images.githubusercontent.com/43316158/159101416-d109dd3d-e861-42d8-bf40-b4e87b020b5a.png)

Bottom teams in the division
Similarly for the bottom 6 teams Swansea have a bad trajectory in terms of performance. West Bromwich Albion and Southampton are flying over the past few seasons. 
If a team finishes in bottom three positions, they get relegated to the lower division in the next season hence some points are missing in the x-axis in the scatterplot.

![image](https://user-images.githubusercontent.com/43316158/159101463-f6e72514-b349-4cd7-8610-c33f3ddf0f24.png)
Wigan athletic are at the same place whereas Stoke city are getting better and Fulham are in a downward trajectory down.

![image](https://user-images.githubusercontent.com/43316158/159101487-531dbeae-d997-401b-a8bc-4a7654d0d40e.png)

These are some of the analysis and inferences we could get of the teams by applying statistical modelling and algorithm to answer the research queries on our dataset.

