# PyBer_Analysis

### Resources
- Python 3.7.6, Jupyter Notebook, Pandas, Matplotlib
- CSV files with source data are in the [Resources](https://github.com/adampaseltiner/PyBer_Analysis/tree/main/Resources) folder

## Overview
The purpose of this project was to analyze ride share data for PyBer to help discover the correlation between city types and their fare metrics based on the average number of rides and drivers. Creating a line-graph to display the metrics for each city type ultimately informed the CEO of these correlations in hopes of guiding her decisions on PyBer's policies regarding rider/driver affordability and company profitability.

## Results

To begin the analysis I created a DataFrame that would show the average metrics for each city type based on "Total Rides", "Total Drivers" and "Total Fares". To calculate the totals for each field I used the `groupby()` function, as follows:

`city_rides_total = pyber_data_df.groupby(["type"]).count()["ride_id"]`

Using this function gives the output:

![City_Rides_Output](https://user-images.githubusercontent.com/82347825/119233377-bd903d80-baf6-11eb-84a5-e4c752c16446.png)

After gathering the totals, I then calculated the average fares. For example:

`city_average_fare = (city_fares_total / city_rides_total)`

![Average_Fare_Output](https://user-images.githubusercontent.com/82347825/119234845-faabfe00-bafd-11eb-9ebb-679e9a20ed51.png)

Using the outputs from each field, the assembled DataFrame looked as follows:

![Pyber_Summary_DataFrame](https://user-images.githubusercontent.com/82347825/119239133-1a9aec00-bb15-11eb-83b7-eabda790b8bb.png)

![Summary_DataFrame](https://user-images.githubusercontent.com/82347825/119235280-b0c41780-baff-11eb-946a-4dbb76aae208.png)

To complete the analysis I then decided to create a multi-line chart that showed the total weekly fares for each city type. 

I began this step by again using `groupby()` to create a new DataFrame showing the sum of fares for each date in each city:

`city_dates_count = pyber_data_df.groupby(["type", "date"]).sum()["fare"]`

![Sum_of_fares_by_city_and_date](https://user-images.githubusercontent.com/82347825/119235873-86278e00-bb02-11eb-9848-7fec257729e7.png)

I was then able to create a pivot table DataFrame which filtered the data to show the sum of fares for each week for each city type:

`pyber_pivot_resample = pyber_pivot_daterange.resample('W').sum()`

![Final_DataFrame_for_line_chart](https://user-images.githubusercontent.com/82347825/119236001-1b2a8700-bb03-11eb-9431-4800441ad26c.png)

Using this final DataFrame, I was then able to create a multi-line chart which showed the weekly fares by city type over the given date range:

![Line_Chart_Code](https://user-images.githubusercontent.com/82347825/119239228-b6c4f300-bb15-11eb-8164-96f7ff9a577d.png)

![Pyber_fare_summary](https://user-images.githubusercontent.com/82347825/119236066-6775c700-bb03-11eb-8a17-beb7ffe25233.png)

When viewing the above DataFrames and summary chart we can deduce several key conclusions from the data:
- Urban cities have a much higher number of rides and drivers than in rural and suburban cities.
- Although the highest volume of drivers and rides are in urban cities, the average fare per ride and fare per driver are by far the highest in rural cities.
- Urban cities are still the most profitable for PyBer in terms of volume, even though these numbers show it may not be as beneficial to the drivers themselves.

## Summary

Based on the results above, I would offer the CEO of PyBer the following suggestions:
- It would be beneficial to include the average distance per ride in the analysis, since it would allow us to account for the differences in fares between city types.
- We should also include an analysis of the average ride duration, since the time each ride lasts could also provide useful information about the correlation between rides, drivers, fare and overall revenue.
- Analyzing frequency of a ride per driver would help model the price of fares by city type, since PyBer might be able to charge more for rural rides and less for urban rides to account for the overall volume disparity
