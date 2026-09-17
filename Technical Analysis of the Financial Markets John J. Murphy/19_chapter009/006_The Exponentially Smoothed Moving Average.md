# 19_chapter009

## The Exponentially Smoothed Moving Average


This type of average addresses both of the problems associated with the simple moving average. First, the exponentially smoothed average assigns a greater weight to the more recent data. Therefore, it is a weighted moving average. But while it assigns lesser importance to past price data, it does include in its calculation all of the data in the life of the instrument. In addition, the user is able to adjust the weighting to give greater or lesser weight to the most recent day’s price. This is done by assigning a percentage value to the last day’s price, which is added to a percentage of the previous day’s value. The sum of both percentage values adds up to 100. For example, the last day’s price could be assigned a value of 10% (.10), which is added to the previous day’s value of 90% (.90). That gives the last day 10% of the total weighting. That would be the equivalent of a 20 day average. By giving the last day’s price a smaller value of 5% (.05), lesser weight is given to the last day’s data and the average is less sensitive. That would be the equivalent of a 40 day moving average. (See Figure 9.2.)

Figure 9.2 The 40 day exponential moving average (dotted line) is more sensitive than the simple arithmetic 40 day moving average (solid line).

The computer makes this all very easy for you. You just have to choose the number of days you want in the moving average—10, 20, 40, etc. Then select the type of average you want—simple, weighted, or exponentially smoothed. You can also select as many averages as you want—one, two, or three.
