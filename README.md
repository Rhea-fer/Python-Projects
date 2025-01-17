# Uber Trips Analysis Project
## Introduction
This project analyzes Uber trip data to extract meaningful insights and visualize patterns such as trip frequencies, purposes, distances, and seasonal variations. It demonstrates data preprocessing, feature extraction, and visualization using Python.

## Dataset Cleaning
The dataset cleaning process involves handling missing values, formatting date columns, and removing inconsistencies. Below are the steps taken to clean and prepare the dataset:

### 1.Loading the Dataset:
The dataset was loaded using pd.read_csv() to start the analysis.

### 2.Checking for Missing Values:
data.isnull().any()
data.isnull().sum()
Identified columns with missing values and quantified the extent of missing data.

### 3.Removing Missing Data:
Rows with missing values were dropped to ensure data integrity:
data = data.dropna()
data.isnull().sum()

### 4.Stripping Column Names:
Ensured column names were free from leading/trailing whitespaces for consistent access:
data.rename(columns=lambda x: x.strip(), inplace=True)

### 5.Converting Dates:
START_DATE and END_DATE columns were converted to datetime format to facilitate time-based analysis:
data['START_DATE'] = pd.to_datetime(data['START_DATE'], errors='coerce', format="%m/%d/%Y %H:%M")
data['END_DATE'] = pd.to_datetime(data['END_DATE'], errors='coerce', format="%m/%d/%Y %H")

## Feature Extraction
New features were derived from the START_DATE column to enable time-based analysis:

### Extracting Components:
Hour, Day, Day of the Week, Month, and Weekday:
![image](https://github.com/user-attachments/assets/0245806c-3e00-481c-bb10-37c6239ec702)

## Data Visualization
Several visualizations were created to explore and analyze the data:

### How many hours do people travel in a day?
Relationship between the hour of the trip and the day of the month:
data.plot(kind='scatter', x='HOUR', y='DAY', s=32, alpha=0.8)
plt.gca().spines[['top', 'right']].set_visible(False)

### How long do people travel with Uber?
A histogram to analyze trip distances:
data['MILES'].plot.hist()

### What is the frquency of trips according to hours?
Frequency of trips during different hours of the day:
hours = data['START_DATE'].dt.hour.value_counts()
hours.plot(kind='bar', color='red', figsize=(10, 5))
plt.xlabel('Hours')
plt.ylabel('Frequency')
plt.title('Number of Trips Vs Hours')

### What is the Purpose Of Trips?
Distribution of trip purposes using a bar chart:
data['PURPOSE'].value_counts().plot(kind='bar', figsize=(10, 5), color='brown')

### Which Day Has the Highest Number of Trips?
The pie chart below shows the percentage distribution of Uber trips across different days of the week. 
It helps identify which day has the highest number of trips.
weekday_counts = data['WEEKDAY'].value_counts()
weekday_counts.plot(kind='pie', figsize=(8, 8), autopct='%1.1f%%', startangle=90, colors=sns.color_palette("pastel"))
plt.title('Percentage of Trips by Day of the Week', fontsize=14)
plt.ylabel('')  # Remove default ylabel
plt.show()

### What is Hourly Trip Frequencies by Day of the Week?
This heatmap visualizes the frequency of Uber trips across different hours of the day (`HOUR`) and days of the week (`DAY_OF_WEEK`). It shows which hours and days have the highest trip frequencies.
heatmap_data = data.pivot_table(index='DAY_OF_WEEK', columns='HOUR', aggfunc='size', fill_value=0)
sns.heatmap(heatmap_data, cmap='coolwarm', annot=False)
plt.title('Hourly Trip Frequency by Day of the Week')
plt.xlabel('Hour of Day')
plt.ylabel('Days of Week')
plt.show()

### Where do people start their Trips from?
The starting points of trips are visualized with a bar chart:
data['START'].value_counts().plot(kind='bar', figsize=(25, 10), color='blue')
This shows where Uber riders most frequently start their trips.

### What are Trips over a period of time?
This line plot visualizes the trend of trips over time, showing how the number of trips changes from day to day:
data['START_DATE'].dt.date.value_counts().sort_index().plot(kind='line', figsize=(12, 6), color='green')
plt.title('Trend of Trips Over Time')
plt.xlabel('Date')
plt.ylabel('Number of Trips')
plt.grid(True)
It helps track how the trip frequency evolves over the entire dataset period.

### What Are The Trips In The Month?
This visualization shows the number of trips taken each month using a bar chart:
data['MONTH'].value_counts().plot(kind='bar', figsize=(10, 5), color='black')
plt.ylabel('Number of Trips')
This helps identify trends in trips across different months.

### What Is the Seasonal Trend Observed in the Trips?
This analysis categorizes trips based on seasons (Winter, Spring, Summer, and Rainy) to observe any seasonal variations in Uber activity.
def get_season(month):
    if month in [12, 1, 2]:
        return 'Winter'
    elif month in [3, 4, 5]:
        return 'Spring'
    elif month in [6, 7, 8]:
        return 'Summer'
    else:
        return 'Rainy'

data['SEASON'] = data['MONTH'].apply(get_season)
data['SEASON'].value_counts().plot(kind='bar', color='teal', figsize=(8, 5))
plt.title('Number of Trips by Season')
plt.xlabel('Season')
plt.ylabel('Number of Trips')
plt.show()

# Conclusion
Through this project, we were able to:
#### Clean and preprocess the Uber dataset.
#### Extract valuable features such as hour, day, month, season, etc.
#### Generate a variety of visualizations to explore trends in Uber trip data like:

### Hourly Trip Analysis
1.Peak Hours: The busiest hours for Uber trips are typically during the morning (e.g., 7–9 AM) and evening (e.g., 5–8 PM) rush hours.

2.Off-Peak Hours: Fewer trips occur during late-night hours (e.g., 1–5 AM), except on weekends, which might have higher activity due to leisure travel.

### Monthly Trends
1.Summer months have higher trips due to vacations.

2.December might see spikes due to holiday celebrations.

### Purpose of Trips
1.Business trips might dominate weekdays.

2.Social trips could spike on weekends.

This analysis can be further extended to predict future Uber demand or evaluate trip frequency patterns for business insights.









