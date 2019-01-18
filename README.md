# Title: How flights delay?
Team members: FU Yan, FENG Wentao, SUN Zhaodong, HUANG Yunbei

## Structure of repo
`Readme.md`: Simple introduction of the project.

`FINAL.ipynb`: The notebook including all codes and analysis of our data set.

`TransLearn.py`: The py containing functions used in transductive learning.

## Abstract
In this project we explored through our dataset and set up a model predicting delay for given conditions, and based on this model we can give advice on choosing flights on different seasons, airlines and hours. Due to the constraint on difficulties getting whole world delay dataset, and the US is the largest flight country, in our project the delay analysis is mostly based on the US data.

We want to know :

* What will affect mostly on the delay of a flight, could it be departure season, hours or airlines?
* And can we predict if and how long will a flight delays given certain situations?
* Or, if some one wants to fly from city A to city B, can we give him or her some advices on choose flights based on the delay rate?


## Dataset
In our project we used two data set, `OpenFlight` and `FlightDelay` data set.

`OpenFlight` dataset is obtained from: https://openflights.org/data.html

This OpenFlights/Airline Route Mapper Route Database contains 67,663 routes (EDGES) between 3,321 airports (NODES) on 548 airlines spanning the globe. 

`FlightDelay` is obtained from Kaggle:

https://www.kaggle.com/usdot/flight-delays#flights.csv

This dataset is collected by the U.S. Department of Transportation's (DOT) Bureau of Transportation Statistics, who tracks more than 5,714,000 samples of domestic flights operated by large air carriers from 01/01/2015 to 31/21/2015, with 322 airport. And features information flight number, airline, departure and arrival time, delay time, air time, distance, origin and destination airport and delay reason( not for all delayed flights). Also, the documents including relationship of IATA code and full information of airports and airlines are given. 

License(https://opendatacommons.org/licenses/odbl/1.0/) and Database Contents License(https://opendatacommons.org/licenses/dbcl/1.0/).


## Result
We created our graph using airports as nodes, distance bewteen airports after Gaussian kernel as weights.

We analyzed delay in two ways: first we binarized the delay time into 1 (the departure airport tends to delay) or -1 (the departure airport tends to arrive earlier), then we used k means, spectral graph and transductive learning to perform clustering. The **accuracy** are 64.3%(5 clusters), 69.4%(threshold eigenvalue is0.004) and 72.3%(recovering from 30% data) respetively.

Then we wanted to use more features than distance to predict the delay time. We used LightGBM, a tree based algorithm. After model building and hyperparameter tuning, we got a model with **prediction rmse = 2.3 (minutes)**, which worked quite well. ANd we also developed recommendation system. Given departure date and airports, our recommendation system will return the best combination of airline and departure time, and also the predicted delay minutes. 
