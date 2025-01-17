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

### Scatter Plot:
Relationship between the hour of the trip and the day of the month:
data.plot(kind='scatter', x='HOUR', y='DAY', s=32, alpha=0.8)
plt.gca().spines[['top', 'right']].set_visible(False)

### Trip Distance Distribution:
A histogram to analyze trip distances:
data['MILES'].plot.hist()

### Hourly Trip Frequency:
Frequency of trips during different hours of the day:
hours = data['START_DATE'].dt.hour.value_counts()
hours.plot(kind='bar', color='red', figsize=(10, 5))
plt.xlabel('Hours')
plt.ylabel('Frequency')
plt.title('Number of Trips Vs Hours')






