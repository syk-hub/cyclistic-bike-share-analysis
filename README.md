## Cyclistic Bike-Share: Analyzing User Behavior to Drive Membership Growth
   
![Alt Text](https://github.com/syk-hub/cyclistic-bike-share-analysis/blob/main/black%20bike%20logo.jpg)

## Project Overview
***
This project analyzes Cyclistic bike-share data using the R programming language, with RStudio as the development environment. The analysis involves data cleaning, visualization, and statistical summaries, all performed with the `tidyverse` package. As a capstone project for the Google Data Analytics Certification, it explores factors that influence the demand for rental bikes using [City Bike Data](https://divvy-tripdata.s3.amazonaws.com/index.html). The goal of this analysis is to understand how casual riders and annual members use Cyclistic bike-share services differently. The marketing team believes that increasing the number of annual memberships is critical to the company’s long-term success. By analyzing user behavior, this project aims to inform a marketing strategy focused on converting casual riders into annual members.

The Cyclistic bike-share data is publicly available through Motivate International Inc. subject to the [Divvy Bikes Data License Agreement](https://www.divvybikes.com/data-license-agreement). The dataset is provided in .CSV format and organized into yearly and quarterly zip files. For this project, I focused on the quarterly data from Q2 2019 to Q1 2020, which can be found [here](https://divvy-tripdata.s3.amazonaws.com/index.html):

* Q2 2019 Data
* Q3 2019 Data
* Q4 2019 Data
* Q1 2020 Data

After downloading and unzipping the files, the data was combined and cleaned for further analysis.

Key findings from the analysis reveal that casual riders primarily use Cyclistic bikes on weekends for leisure, while annual members use them more frequently during weekdays for commuting. This behavior suggests opportunities to target casual riders with incentives to encourage more regular usage through annual memberships.

# Detailed Explanation of the Analysis Process
***
The analysis process began with **data cleaning** to ensure consistency across the dataset, followed by the calculation of key metrics like ride length and the categorization of users by type (casual or annual members).

### Data Cleaning

The data was sourced quarterly and needed to be combined into a single dataframe. The first step was renaming columns to ensure consistency across different quarters, as the column names varied slightly between files. The `rename()` function was used to standardize the column names to match the most recent year’s naming convention.

Next, I converted relevant columns to consistent data types using the `mutate()` function. This ensured that variables like dates and times were properly formatted for further analysis. After these steps, I combined the four quarterly datasets—Q2 2019, Q3 2019, Q4 2019, and Q1 2020—into a single dataframe called `all_trips`. You can download the cleaned dataset [here](https://drive.google.com/file/d/1H9Bvr2zZhjfVP-UOqrym7kramMNVriTN/view?usp=drive_link).



### Data Manipulation

Once the data was cleaned and combined, I moved on to data manipulation. This involved:

* **Removing irrelevant columns**: Columns that were not needed for the analysis or were discontinued after 2020 were dropped from the dataframe.

* **Recoding user types**: The `member_casual` field originally contained four categories, which I recoded into two—casual and annual—using the `recode()` function.

* **Extracting date components**: From the `started_at` column, I extracted important time components (month, year, day, and day of the week) by reformatting the column using the `format()` function.

* **Calculating ride length**: A new column, `ride_length`, was created to calculate the duration of each ride in seconds. This was done by subtracting the start time (`started_at`) from the end time (`ended_at`). The `ride_length` column was then converted to a numeric data type for further calculations.

* **Removing invalid values**: I filtered out invalid or erroneous data, such as negative ride lengths or missing station names, to ensure the dataset was ready for accurate analysis.

For full details on the data cleaning and transformation process, as well as the complete code, please refer to the attached R Markdown file [here](https://github.com/syk-hub/cyclistic-bike-share-analysis/blob/main/Cyclistic%20Project%20R%20markdown%20V2.Rmd).


# Exploratory Data Analysis
***
Exploratory Data Analysis (EDA) was conducted to uncover trends and patterns in how casual and annual members use the bike-sharing service. The primary focus was on analyzing ride length, usage patterns by day of the week, and differences between user types.

### Descriptive Analysis of Ride Length

We began by performing descriptive analysis on the `ride_length` variable using the `aggregate()` function to calculate summary statistics such as the average ride length for each user type. This helped to identify key differences between casual riders and members.

### Analyzing Ride Length by Day of the Week

To further investigate usage patterns, we extended the analysis by calculating the average ride length for each day of the week, separated by user type (casual or annual member). This was done by applying the `aggregate()` function to group the data by day of the week. The day-of-week data was then rearranged into a logical order (Sunday to Saturday) using the `ordered()` function for better readability.

### Ridership by Type and Weekday

Next, we analyzed the ridership data to compare the number of rides and the average ride duration for casual and annual members across different weekdays. By performing a series of data manipulations and aggregations on the `all_trips_v2` dataset, we calculated:

* The total number of rides for each combination of user type and weekday.
The average ride duration for each combination, allowing us to identify peak usage days and longer ride times for casual riders.

* The final step was to reorder the days of the week in a logical sequence (Sunday to Saturday) using the `ordered()` function, ensuring that the output was easy to interpret and analyze.

For complete code and further details on the EDA process, please refer to the attached R Markdown file [here](https://github.com/syk-hub/cyclistic-bike-share-analysis/blob/main/Cyclistic%20Project%20R%20markdown%20V2.Rmd).

# Key Insights and Visualizations
***
This section presents visualizations using `ggplot2` to highlight key findings regarding the behavior of casual riders and annual members.

* **Casual riders** tend to use bikes mainly on weekends, while **annual members** ride more often during weekdays.

* **Ride lengths** for casual riders are significantly longer than those of annual members.

* Weekends show a spike in casual rider activity, particularly in the afternoons.


The following plots summarize these insights:

1. Total number of rides for each member type by day of the week.
   ![Alt Text](https://github.com/syk-hub/cyclistic-bike-share-analysis/blob/main/total%20no%20rides%20for%20mem%20type%20by%20day%20of%20the%20week.png)
  
3. Average ride length for each member type by day of the week. 
   ![Alt Text](https://github.com/syk-hub/cyclistic-bike-share-analysis/blob/main/avg%20no%20rides%20for%20mem%20type%20by%20day%20of%20the%20week.png)
   
5. Median ride length for each member type by day of the week. 
   ![Alt Text](https://github.com/syk-hub/cyclistic-bike-share-analysis/blob/main/median%20ride%20length%20for%20mem%20type%20by%20day%20of%20the%20week.png)
   
7. Average ride length for each member type by month.
   ![Alt Text](https://github.com/syk-hub/cyclistic-bike-share-analysis/blob/main/avg%20ride%20length%20for%20mem%20type%20by%20month.png)

# Summary
***
Historical bike data from April 2019 to March 2020 reveals distinct patterns in how casual and annual members use Cyclistic bikes. Key findings include:

* **Weekend Usage**: Both groups prefer weekends for longer rides, especially casual riders, showing a U-shaped trend across the week.

* **Ride Consistency**: Annual members have shorter but more consistent ride lengths across the week, while casual riders exhibit greater variation.

* **Frequency**: Annual members take more rides overall, especially on weekdays, while casual riders prefer weekends.

* **Seasonal Trends**: The busiest months are July, August, and September, aligning with warmer weather and increased outdoor activity.



