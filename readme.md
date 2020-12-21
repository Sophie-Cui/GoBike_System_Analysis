# Ford GoBike System Data Analysis
## by Murong (Sophie) Cui



> This data set includes information about individual rides made
in a bike-sharing system covering the greater San Francisco
Bay area. Note that this dataset will require some data wrangling in
order to make it tidy for analysis.

- What is the structure of your dataset? <br>
There are 174,951 rows representing 174951 rides during Feb 2019 in Great San Francisco (San Francisco, Oakland, San Jose) and 15 columns
 - Trip Duration (seconds)
 - Start Time and Date
 - Stop Time and Date
 - Start Station ID
 - Start Station Name
 - Start Station Latitude
 - Start Station Longitude
 - End Station ID
 - End Station Name
 - End Station Latitude
 - End Station Longitude
 - Bike ID
 - User Type (Customer = 24-hour pass or 3-day pass user; Subscriber = Annual Member)
 - Gender (Other; Male; Female)
 - Year of Birth
 - bike_share_for_all_trip, which tracks members who are enrolled in the Bike Share for All program for low-income residents.

- What is/are the main feature(s) of interest in your dataset?<br>
Gobike completed close to 200 thousand rides in San Francisco in one month (Fed 2019), which shows us a great need of short/medium bike transportation. So firstly, we could look at the popularity of stations and paths that may could help making business decision like where to add a station or add more bikes at certain station.
Secondly, we could also take a look at the customer segmentation. We have some user feature like, age, gender, subscribed or not, in the program 'bike share for all' or not ...<br>
Then, it is interesting to draw insights from share-mobility over time. But since we only have one month data, it is still worthy to take a look at the trip frequency by day of the week, or the hour of the day, etc....<br>

- What features in the dataset do you think will help support your investigation into your feature(s) of interest?<br>
Trip Duration, Start/End Time and Date, Latitude and Longitude, User Type, Gender, Year of Birth, bike share for all trip...

## Summary of Findings
![Alt text](pic/station_overview.png?raw=true "net departure and net arrival stations on morning and evening rush hour")
| *net departure and net arrival station on morning and evening rush hour* |
![Alt text](pic/station_detail.png?raw=true "net departure and net arrival stations on morning and evening rush hour (zoom in San Francisco)")
| *net departure and net arrival station on morning and evening rush hour (zoom in San Francisco)*|
> Yellow circle means net departures and blue circle means net arrival. Locations that have positive net departures in the morning rush hour 8am - 9am (left figure) have net arrivals in the evening rush hour 17pm - 18pm (right figure), likely matching the pattern that people going to work in the morning and back home evening. Also We could tell these are 3 main area in the greater SF area, San Francisco, Oakland, and San Jose. So we could add one more column to specific the area (San Francisco, Oakland, San Jose)

![Alt text](pic/path_detail.png?raw=true "net departure and net arrival stations on morning and evening rush hour (zoom in San Francisco)")
|*paths on weekday and weekend(zoom in San Francisco)* |
> The above are two graph plotting paths on the map, the left one is the paths on 8AM on Tuesday. And the right one is the paths on 17PM on Sunday. These is clear difference. The left shows At 8AM on Tuesday, a hight volume of path inbounding to the downtown San Francisco, Financial District, Downtown Oakland, Civic Center and Downtown San Jose. This is consistent with the station count geo plot before, indicating the rides are employed by morning commute.
The right plot capturing rides on Sunday evening shows no high volume path.

![Alt text](pic/uni1.png?raw=true)
> All the user information is based on the rides, which leads bias due the same user having multiple rides. Therefore all the insights about user segmentation in this pics is based on the total number of rides. We could say among certain 183214 of rides, 163414 rides are made by Subscribers and 19800 made by Customers, which means almost 90% ride were taken by subscribers, in other words, almost 9 out of 10 rides are part of a subscription package.  As for member gender, despite 8263 rides not containing information of user gender, 130500 rides out of 174951 were taken by males, and 40804 rides are taken by female (Only one in hour ride taken by female). It is fair to assume that the male VS female ratio is not close as well as female are more concerned about cosmetic side-effect and mess-up hair during riding. And for Bike Share for All program for low-income residents, there are 17346 out of 183214, around 9% rides are part of bike share for all program.

![Alt text](pic/uni2.png?raw=true)
> Not surprisingly, the main user are 17 year ago to 40 year ago; which seems like the bike sharing idea is more popular during the younger. However, surprisingly, these were some senior users who ages over 80s. If we treated senior riders as outliers, we could clean data later.

![Alt text](pic/uni3.png?raw=true)
> We look at the trip counts over 2 dimensions, day of week and hour of day. I plot the number of rides over day of week and we could tell that the number of trips on weekdays is around double than the number over the weekends. It seems like that more need to ride short commute or fulfill the last mile to their offices or destinations on weekdays.
And for hour of day, we could tell the two peaks around 8 o'clock and 17 o'clock, which indicates that the large needs around the morning and evening rush hour.

![Alt text](pic/uni4.png?raw=true)
![Alt text](pic/uni5.png?raw=true)
> Both trip duration and trip distance are right skewed, so I did log transformation to both of them.

![Alt text](pic/bi1.png?raw=true)
> I plot heatmaps, the heatmaps are capturing the number of rides over hour of day and day of week. When we look at the subscriber plot (right plot), there is a clear trajectory of rides taken by subscribers over time, which is that subscribers are taking rides on morning and evening rush hour on weekday. And the left plot is only for customers, same as the subscribers, customers take rides for weekday commuting. and interestingly, customers also have more need on weekend, which indicated that rids taken by customers on weekend may not be pre-scheduled.

![Alt text](pic/bi2.png?raw=true)
>I draw two line plots. The left plot is age vs average trip distance and the right plot is age VS average trip duration. Between 20 year age and 60 year ago, the average distance is relatively stable, and after 60 year ago, the trip distance and trip duration have large variance.

![Alt text](pic/multi1.png?raw=true)
> When Adding the cities (San Francisco, San Jose, Oakland) into the number of rides over time, We could tell all three cities shows the similar trends, a high volume on weekday commute rush hour and weekend afternoon. Among the cities, San Francisco has the highest sharing bike needs, and followed by Oakland and then San Jose.

![Alt text](pic/multi2.png?raw=true)
>For all four plots, it is suspicious that the member gender of other shows some usual thing for all plots. It is worthy to investigate it if we have more data. Besides, overall subscribers is generally taking rides with more distance and more duration. And there is no significant difference between male and female regarding average trip duration and average trip duration.


## Key Insights for Presentation

- Investigating distributions of individual variables, I looked at users segmentation, population phyramid, trip count over time, trip duration, and trip distance. There are some unusual points I found during univariate exploration.
- For trip duration and trip distance, I apply different transformations to normalize the data. And after scaling data, the data tends to be more likely the normal distribution.
- We could tell subscribers and customers did behave differently on weekend, customers rides seems show more needs on the weekend. It is a sign that a marketing campaign focus on promoting sharing bike on weekend event.
- From the geo analysis we did at the first part, we could see the three cluster on the map, San Francisco, Oakland, San Jose. It is worthy to take look at three cities separately in the future to understand how user in different cities engage bike sharing.
