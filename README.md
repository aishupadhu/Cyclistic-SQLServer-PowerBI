# Cyclistic-SQLServer-PowerBI
Data Analysis case study of a bike sharing company (using SQL and Power BI)
Scenario
Cyclistic is a US based bike sharing company operating mainly in the Chicago, IL area. Riders can be Members (those who pay annual subscriptions are members) or Casual. The company believes that maximizing annual subscriptions is key to driving future growth. The data analyst team in Cyclistic has been tasked with analyzing historical ride data to identify how members and casual riders use the service differently. The Google Data Analytics approach has been adopted for this case study. This process breaks down a data analytics task into 6 steps:

Ask
Prepare
Process
Analyze
Share
Act
The sections below correspond to each of these 6 steps.

##Step 1: Ask - Understanding the Business Task
As part of this data analysis task, Cyclistic leadership would like to understand how members and casual riders use the service differently based on ride data for the past 12 months. Based on this analysis, a data-driven marketing strategy will be developed and deployed.

##Step 2: Prepare - Acquiring the Input Data Elements
The dataset used is a public dataset located at https://divvy-tripdata.s3.amazonaws.com/index.html. It is provided by Motivate International Inc., under this license - https://www.divvybikes.com/data-license-agreement as a part of the Google Data Analytics Certificate program. 12 months of data was used for the analysis from May 2021 to April 2022.

The dataset provides details of rides that users took in these 12 months and contains the following fields:

ride_id - Contains a unique identifier for each ride taken. This field can be used to remove any duplicate records present in the dataset.
rideable_type - Indicates the type of bike used for the ride (electric_bike, classic_bike or docked_bike). This field was not used in the analysis.
started_at - Contains the start date and time for each ride. This field is useful for analyzing usage patterns of members and casual users.
ended_at - Contains the end date and time for each ride. This field along with the started_at field can be used to determine the ride length of each ride.
start_station_name - Contains the station name where the ride originated. However, most records do not contain a value for this field and so this field was not used in the analysis.
start_station_id - Contains the station id where the ride originated. However, most records do not contain a value for this field and so this field was not used in the analysis.
end_station_name - Contains the station name where the ride ended. However, most records do not contain a value for this field and so this field was not used in the analysis.
end_station_id - Contains the station id where the ride ended. However, most records do not contain a value for this field and so this field was not used in the analysis.
start_lat - Contains the latitude where the ride originated. This field along with the start_lng indicates the location where the ride started.
start_lng - Contains the longitude where the ride originated.
end_lat - Contains the latitude where the ride ended. This field was not used in this analysis.
end_lng - Contains the longitude where the ride ended. This field was not used in this analysis.
member_casual - Indicates whether the rider was a member paying an annual subscription or a casual rider.
Since there is no rider information provided in this dataset, it is not possible to analyze behavior of individual riders, which would have provided further valuable insight for this analysis.

##Step 3: Process - Data Cleansing and Processing
 Microsoft SQL Server was used for data cleansing and processing.

The dataset is in the form of 12 CSV files, each containing ride data from May 2021 to April 2022. There are over 5 million records combined and R is a good choice to handle this volume. The following steps were performed as part of processing and preparing the dataset for visualizations.

<img src="/sqlimage/Data%20Combining.png" />



Data Cleansing
Fields not used in the analysis were dropped (to improve processing performance).
Any leading and trailing white spaces were removed in all fields.
140 invalid records were found and removed where the end time was prior to the start time.
Duplicate values were checked for based on the "ride_id" field, but none were detected.

<img src="/sqlimage/Data%20Cleaning.png" />


Data Processing
The following new fields were added to the dataset to be used in the visualizations:
"day_week_start_trip" - contains the day of the week on which the trip started (eg: Sunday, Monday etc.).
"ride_length_hours" - contains the the ride length in hours rounded to 2 decimal places (eg: 1.23).
"rtart_lat_rounded" - contains latitude rounded to 3 decimal places to remove clutter (eg: 41.891).
"start_lng_rounded" - contains longitude rounded to 3 decimal places to remove clutter (eg: -87.634).
A screenshot of the query that was run on SQL Server is shown below, the workflow file is available in this Github repository as well.

<img src="/sqlimage/Data%20Processing.png" />

## Step 4: Analyze - Analysis through Visualizations
**Power BI** was used for building the visualizations for this analysis.

The following visualizations were built to analyze how members and casual riders use bikes differently. Ride counts and ride lengths were analyzed by user type as well as by ride start location, month/quarter, and day of the week.


This chart below, shows the ride count by day of the week of the day. During the weekdays, most of the usage is by members.

<img src="/sqlimage/Count%20of%20rides%20by%20weekday.png" />

This chart below, shows how ridership varies across months and quarters between casual riders and members. Casual ridership seems to peak during the summer months while dropping off significantly in winter. While members' ridership drops off during winter as well, the drop is not as steep as for casual riders.

<img src="/sqlimage/Casual%20and%20member%20riders%20by%20month.png" />

The charts below ride length and count by origination location and user type. While the service seems to cover quite a large area, most of the activity seems to be focused in a handful of zip codes like 60610, 60611, 60614, 60654 and 60657. It can also be observed that while casual users overall seem to take fewer rides than members, casual users have longer ride durations.


<img src="/sqlimage/Rides%20by%20members%20and%20casual%20riders.png" />

## Step 5: Share - Presentation of Insights
The dashboard below shows seasonal as well as day wise usage by user type. This provides valuable insight into when marketing efforts can be deployed. For example, the marketing team may decide to run a campaign covering weekend afternoons in the summer months of June and July as this is the time there's likely to the largest reach into the casual userbase.

<img src="/sqlimage/Casual%20rider%20and%20member%20rides%20quarter%20comparision.png" />

The chart below shows the Stations with  most activity. This is helpful in identifying precise rider stations where traditional marketing tools can be leveraged. 
<img src="/sqlimage/Station%20popularity%20by%20riders.png" />

## Step 6: Act - Next Steps
As noted above, this analysis yielded valuable insights that the marketing team at Cyclistic can leverage to design their marketing campaigns. From the standpoint of the data analysis team, the following can be potential next steps:  
* Supporting the marketing team in tracking the effectiveness of various campaigns
* Considering ways to improve the current analysis:
	* Expanding the scope of the analysis from the past 12 months to even further in the past, which may help uncover longer multi-year trends
	* Bringing in additional data points like a user identifier (data can be appropriately de-identified so as to remove any Personally Identifiable Information), which would enable a variety of interesting analysis (eg: determining the revenue impact of converting casual users to members)
