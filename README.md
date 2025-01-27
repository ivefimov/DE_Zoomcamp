# DE_Zoomcamp
HW_01

## Question 3. Trip Segmentation Count

During the period of October 1st 2019 (inclusive) and November 1st 2019 (exclusive), how many trips, **respectively**, happened:
1. Up to 1 mile

   **df[(df['lpep_pickup_date']>="2019-10-01")&(df['lpep_dropoff_date']<"2019-11-01") &(df['trip_distance']<=1)].trip_distance.count()**
3. In between 1 (exclusive) and 3 miles (inclusive),

    **df[(df['lpep_pickup_date']>="2019-10-01")&(df['lpep_dropoff_date']<"2019-11-01") &(df['trip_distance']>1)&(df['trip_distance']<=3)].trip_distance.count()**
5. In between 3 (exclusive) and 7 miles (inclusive),

   **df[(df['lpep_pickup_date']>="2019-10-01")&(df['lpep_dropoff_date']<"2019-11-01") &(df['trip_distance']>3)&(df['trip_distance']<=7)].trip_distance.count()**
7. In between 7 (exclusive) and 10 miles (inclusive), 

   **df[(df['lpep_pickup_date']>="2019-10-01")&(df['lpep_dropoff_date']<"2019-11-01") &(df['trip_distance']>3)&(df['trip_distance']<=7)].trip_distance.count()**
9. Over 10 miles

    **df[(df['lpep_pickup_date']>="2019-10-01")&(df['lpep_dropoff_date']<"2019-11-01") &(df['trip_distance']>10)].trip_distance.count()**

## Question 4. Longest trip for each day

Which was the pick up day with the longest trip distance?
Use the pick up time for your calculations.

**df.groupby(df['lpep_pickup_date'].dt.date).trip_distance.max().reset_index().sort_values(by='trip_distance', ascending=False)**

## Question 5. Three biggest pickup zones

Which were the top pickup locations with over 13,000 in
`total_amount` (across all trips) for 2019-10-18?

Consider only `lpep_pickup_datetime` when filtering by date.

**df2=df[df.lpep_pickup_date.dt.strftime('%Y-%m-%d') == '2019-10-18'].groupby('PULocationID').total_amount.sum().nlargest(3)**
**df2.reset_index().merge(dftz[['LocationID','Zone']],left_on='PULocationID',right_on='LocationID')**

## Question 6. Largest tip

For the passengers picked up in October 2019 in the zone
named "East Harlem North" which was the drop off zone that had
the largest tip?

**ltips=df[(df.lpep_pickup_date.dt.strftime('%Y-%m') == '2019-10') & (df.PULocationID == 74)].tip_amount.max()**
**df[df.tip_amount==ltips].merge(dftz[['LocationID','Zone']],left_on='DOLocationID',right_on='LocationID')**



