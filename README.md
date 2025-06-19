# CYCLISTIC BIKE-SHARE CASE STUDY PROJECT REPORT

## INTRODUCTION

In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geo-tracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. 
Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

## PROBLEM STATEMENT
Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, Moreno, Cyclistic’s director of marketing, believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a solid opportunity to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs. 
Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends.
Three questions will guide the future marketing program: 
1. How do annual members and casual riders use Cyclistic bikes differently? 
2. Why would casual riders buy Cyclistic annual memberships? 
3. How can Cyclistic use digital media to influence casual riders to become members?


## DATA ANALYSIS PROCESS

### ASK PHASE
The questions that would be guiding future marketing programs are:
1. How do annual members and casual riders use Cyclistic bikes differently? 
2. Why would casual riders buy Cyclistic annual memberships? 
3. How can Cyclistic use digital media to influence casual riders to become members?

This project report has been specifically tasked with answering the first question, this is, how do annual members and casual riders use Cyclistic bikes differently in the last one year?

### PREPARE PHASE
The data to be used for this project is gotten from Cyclistic’s historical trip data linked here. This is a public data that can be used to explore how different customer types are using Cyclistic bikes and also used to analyze and identify trends. (Note: The datasets have a different name because Cyclistic is a fictional company. For the purposes of this case study, the datasets are appropriate and will enable you to answer the business questions. The data has been made available by Motivate International Inc. under this license.)
The data linked above contains trip data based on months from April, 2020 till the last month before this analysis, the data are updated after the end of every month. A snippet of how the data is organized is shown below:
 
![image](https://github.com/user-attachments/assets/da4cc128-0da4-4ebd-9ff0-ca3109919912)

**Metadata:**
ride_id: Unique ID for each ride
rideable_type: Kind of bike used for the ride
started_at: Date and time when ride started
ended_at: Date and time when ride ended
start_station_name: Station where ride started
start_station_id: ID of station where ride started
end_station_name: Station where ride ended
end_station_id: ID of station where ride ended
start_lat: Latitude of station where ride started 
start_lng: Longitude of station where ride started
end_lat: Latitude of station where ride ended
end_lng: Longitude of station where ride ended
member_casual: Membership type 

### PROCESS PHASE
The following steps taken to process data
1. Download the previous 12 months of trip data. 
2. Unzip the files. 
3. Create a folder on desktop to house the files. Use appropriate file-naming conventions. 
4. Create subfolders for the .csv file and the .xlsx or Sheets file so that original copy of data is available. Move the downloaded files to the appropriate subfolder. 
In Excel
5. Launch Excel, open each file, and choose to Save As an Excel Workbook file. Put it in the subfolder you created for .xlsx files. 
6. Open spreadsheet and create a column called ride_length. Calculate the length of each ride by subtracting the column started_at from the column ended_at (for example, =D2-C2) and format as HH:MM:SS using Format > Cells > Time > 37:30:55, then populate across each record. 
7. Create a column called day_of_week, and calculate the day of the week that each ride started using the WEEKDAY command (for example, =WEEKDAY(C2,1)) in each file. Format as General or as a number with no decimals, noting that 1 = Sunday and 7 = Saturday, then populate across each record. 
8. Create another column called month, and input the month of each ride using the TEXT() function (for example, =TEXT(D2,”mmmm”)) and format as General, then populate across each record. 
9. Proceed to remove duplicate data using Remove Duplicates, on Data tab > Data Tools > Remove Duplicates
10. Remove columns that would not be needed for analysis, columns such as started_at, ended_at, start_station_name, start_staion_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng.
11. Remove null values and unreadable text from the remaining columns using filter and sort
12. Check to confirm that each columns are in the correct format.
13. Redo from 1-12 for the other datasets
After all the steps above, a snippet of the data is shown below:

![image](https://github.com/user-attachments/assets/3c66f90e-3244-462c-86bb-cbfde6d047fd)
 
### ANALYZE PHASE
Open one of the Excel data, then complete the following steps:
Excel (Conduct Descriptive Analysis)

1.	On the opened workbook, run a few calculations to get a better sense of the data layout.
•	Calculate the mean of ride_length. For example, on cell H2, input =AVERAGE(C:C), and format as HH:MM:SS using Format > Cells > Time > 37:30:55
•	Calculate the max of ride_length. For example, on cell H3, input =MAX(C:C), and format as HH:MM:SS using Format > Cells > Time > 37:30:55
•	Calculate the mode of day_of_week. For example, on cell H4, input =MODE(D:D)

2.	Create a pivot table to quickly calculate and visualize the data. 
•	Calculate the average ride_length for members and casual riders. Try rows = member_casual; Values = Average of ride_length. 
•	Calculate the average ride_length for users by day_of_week. Try columns = day_of_week; Rows = member_casual; Values = Average of ride_length. 
•	Calculate the number of rides for users by day_of_week by adding Count of trip_id to Values.

3.	Open another file and perform the same descriptive analysis steps. Explore different seasons to make some initial observations.

4.	Once this is done, merge them into a full-year view.
SQL (PostgreSQL)

5.	Make sure the location of all 12 is easily accessible

6.	Open PostgreSQL and connect to server, then create a database, follow the steps below:
•	Left click Databases > Create > Databases
•	Fill in the name of the database (TRIPDATA) and click save

7.	Open TRIPDATA database and create tables for each data. Follow the steps below:
•	Extend view of Databases > extend view of TRIPDATA > extend view of Schemas > Tables > Query Tool
•	In the Query editor displayed, type in and execute the following:

```
CREATE TABLE IF NOT EXISTS public.tripdata01
(
    ride_id text COLLATE pg_catalog."default",
    rideable_type text COLLATE pg_catalog."default",
    ride_length interval,
    day_of_week text COLLATE pg_catalog."default",
    month text COLLATE pg_catalog."default",
    member_casual text COLLATE pg_catalog."default"
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.tripdata01
    OWNER to postgres;
```

•	Refresh the database
•	This creates and formats Tripdata01
•	Do this for the remaining 11 table and name accordingly, that is, tripdata02, tripdata03, tripdata04 and so on.

8.	Import data into tables created in TRIPDATA database, follow the steps below:
•	Right click tripdata01 > Import/Export Data
•	Check Import on General tab, input file path for data to be imported or search for file
•	Select comma (,) delimiter and check Header in the Options tab and click Ok
•	Do this for the remaining data with January’s data as Tripdata01 and December’s data as Tripdata12 for easy identification.

9.	To merge all of the month’s data to get a full-year view, Open the Query Editor and input the following:
```
WITH total AS
(SELECT *
FROM tripdata01
 UNION ALL
 SELECT *
 FROM tripdata02
 UNION ALL
 SELECT *
 FROM tripdata03
 UNION ALL
 SELECT *
 FROM tripdata04
 UNION ALL
 SELECT *
FROM tripdata05
 UNION ALL
 SELECT *
 FROM tripdata06
 UNION ALL
 SELECT *
 FROM tripdata07
 UNION ALL
 SELECT *
 FROM tripdata08
 UNION ALL
 SELECT *
FROM tripdata09
 UNION ALL
 SELECT *
 FROM tripdata10
 UNION ALL
 SELECT *
 FROM tripdata11
 UNION ALL
 SELECT *
 FROM tripdata12)
 
SELECT *
FROM total
```

A snippet of the merged data is shown below:

 ![image](https://github.com/user-attachments/assets/c319f299-614d-4b92-afd2-41ccf67fe64d)

10.	To create a table that summarizes all data, enter the following query in the query editor and download as CSV (named gen2):
SELECT COUNT(ride_id) no_of_ride, SUM(ride_length) total_ride_time, 
AVG(ride_length) ave_ride_time, MAX(ride_length) max_ride_time, 
month, member_casual, COUNT(rideable_type) bike_type_count, rideable_type, 
COUNT(day_of_week) day_of_week_count, day_of_week
FROM total
GROUP BY month, member_casual, rideable_type,day_of_week

11.	Also to get the average time spent on each ride grouped by membership type and months of the year, enter the following query in the query editor and download as CSV (named avg):
SELECT member_casual, month, AVG(ride_length) avg, SUM(ride_length) sum
FROM total
GROUP BY member_casual, month

12.	Lastly, get the total average time spent on ride through out the year, enter the following query in the query editor:
SELECT AVG(ride_length)
FROM total
Excel
13.	Open and resave the two CSV file as xlsx files.
14.	Put both files into a single excel file but different worksheet 
15.	Create a table in both worksheet
16.	Create two more worksheet, one for pivot tables and the other for a dashboard
 
![image](https://github.com/user-attachments/assets/7a09c96c-b334-4d71-8ca0-ac708cfcab34)

Excel (Pivot Tables)

17.	From gen2 sheet, create the following pivot tables:
•	Calculate the total ride time for members and casual riders by the year. Try rows = month; columns = member_casual; Values =sum of total_ride_time
•	Calculate the total number of rides for members and casual riders by the year. Try rows = month; columns = member_casual; Values =sum of no_of_ride
•	Calculate the share of total ride for members and casual riders. Try rows = member_casual; Values =sum of no_of_ride
•	Calculate the preferred bike for members and casual riders. Try rows = rideable_type; columns = member_casual; Values =sum of no_of_ride 

18.	On avg sheet, create a new column (avg_time), and populate records with 17:18, which is the total average ride time for the year

19.	From avg sheet, create the following pivot table:
•	Calculate the average ride time for members and casual riders through the year compared to the total average ride time. Try rows = month; columns = member_casual; Values = sum of avg, min of avg_time 
Excel (Dashboard)

20.	Use the pivot tables in the Pivot table sheet to create graphs accordingly

21.	Design dashboard accordingly

22.	Add filter for interactivity

### SHARE PHASE
After analyzing the data, A visualization is made to support and present key findings. The visualization below shows how members and casual riders use cyclistic differently. 

![image](https://github.com/user-attachments/assets/ed19085f-dfeb-4f8b-ba66-a0a0c2328ecc)

Link to dashboard [here](https://1drv.ms/x/c/c8d18f7e1a10d8f9/EXRTrSSNmZxLp_NV-nwfNg0BZ1d2V98RFtv9dcuFOVu7Lw?e=VEg1Kl)
 
## OBSERVATIONS AND RECOMMENDATIONS
1.	Casual riders have the least number of rides but at average spends more time on each ride
2.	Peak periods are from around May to October with casual riders taking the lead in ride time
3.	Casual members use electric scooters more than members
4.	There should be a discount for longer ride.
5.	This discount should be within the peak period for members. 
6.	More advert targeted at the new electric scooters
