I aim to utilize data visualization to analyze and present data from NYPD shooting incidents while addressing the following questions:

Why is this task being pursued? (Goal) 
a. To demonstrate trends in NYPD shooting incidents, determining whether these incidents are increasing or decreasing over time.
b. To identify which city has the highest number of shootings.
c. To analyze the times of day and days of the week when incidents are most frequent.

How is the task conducted? (Means) 
a. Users should be able to navigate through the data.
b. Users should be able to rearrange data outputs.
c. Users should be able to compare different data outputs.

What does the task seek to learn about the data? (Characteristics) 
a. Seasonal patterns in NYPD shootings.
b. The number of incidents that resulted in fatalities.
c. Trends in NYPD shootings.
d. Locations where shooting incidents occurred.

Where does the task operate? (Target data) 
a. The data will be sourced from "NYPD_shooting_Incident_Data__Historic_.csv" https://data.cityofnewyork.us/api/views/833y-fsy8/rows.csv?accessType=DOWNLOAD"

When is the task performed? (Workflow) 
a. Not limited

Who is executing the task? (Roles) 
a. The task will be conducted by students and instructors in the Master of Science in Data Science program at the University of Colorado Boulder, as well as members of the public.

#### Import required libraries and read the dataset file


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
df = pd.read_csv("NYPD_data.csv")
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>INCIDENT_KEY</th>
      <th>OCCUR_DATE</th>
      <th>OCCUR_TIME</th>
      <th>BORO</th>
      <th>LOC_OF_OCCUR_DESC</th>
      <th>PRECINCT</th>
      <th>JURISDICTION_CODE</th>
      <th>LOC_CLASSFCTN_DESC</th>
      <th>LOCATION_DESC</th>
      <th>STATISTICAL_MURDER_FLAG</th>
      <th>...</th>
      <th>PERP_SEX</th>
      <th>PERP_RACE</th>
      <th>VIC_AGE_GROUP</th>
      <th>VIC_SEX</th>
      <th>VIC_RACE</th>
      <th>X_COORD_CD</th>
      <th>Y_COORD_CD</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Lon_Lat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>231974218</td>
      <td>08/09/2021</td>
      <td>01:06:00</td>
      <td>BRONX</td>
      <td>NaN</td>
      <td>40</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>False</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18-24</td>
      <td>M</td>
      <td>BLACK</td>
      <td>1.006343e+06</td>
      <td>234270.000000</td>
      <td>40.809673</td>
      <td>-73.920193</td>
      <td>POINT (-73.92019278899994 40.80967347200004)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>177934247</td>
      <td>04/07/2018</td>
      <td>19:48:00</td>
      <td>BROOKLYN</td>
      <td>NaN</td>
      <td>79</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>True</td>
      <td>...</td>
      <td>M</td>
      <td>WHITE HISPANIC</td>
      <td>25-44</td>
      <td>M</td>
      <td>BLACK</td>
      <td>1.000083e+06</td>
      <td>189064.671875</td>
      <td>40.685610</td>
      <td>-73.942913</td>
      <td>POINT (-73.94291302299996 40.685609672000055)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>255028563</td>
      <td>12/02/2022</td>
      <td>22:57:00</td>
      <td>BRONX</td>
      <td>OUTSIDE</td>
      <td>47</td>
      <td>0.0</td>
      <td>STREET</td>
      <td>GROCERY/BODEGA</td>
      <td>False</td>
      <td>...</td>
      <td>(null)</td>
      <td>(null)</td>
      <td>25-44</td>
      <td>M</td>
      <td>BLACK</td>
      <td>1.020691e+06</td>
      <td>257125.000000</td>
      <td>40.872349</td>
      <td>-73.868233</td>
      <td>POINT (-73.868233 40.872349)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>25384540</td>
      <td>11/19/2006</td>
      <td>01:50:00</td>
      <td>BROOKLYN</td>
      <td>NaN</td>
      <td>66</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>PVT HOUSE</td>
      <td>True</td>
      <td>...</td>
      <td>U</td>
      <td>UNKNOWN</td>
      <td>18-24</td>
      <td>M</td>
      <td>BLACK</td>
      <td>9.851073e+05</td>
      <td>173349.796875</td>
      <td>40.642490</td>
      <td>-73.996912</td>
      <td>POINT (-73.99691224999998 40.642489932000046)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>72616285</td>
      <td>05/09/2010</td>
      <td>01:58:00</td>
      <td>BRONX</td>
      <td>NaN</td>
      <td>46</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>MULTI DWELL - APT BUILD</td>
      <td>True</td>
      <td>...</td>
      <td>M</td>
      <td>BLACK</td>
      <td>&lt;18</td>
      <td>F</td>
      <td>BLACK</td>
      <td>1.009854e+06</td>
      <td>247502.562500</td>
      <td>40.845984</td>
      <td>-73.907461</td>
      <td>POINT (-73.90746098599993 40.84598358900007)</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 28562 entries, 0 to 28561
    Data columns (total 21 columns):
     #   Column                   Non-Null Count  Dtype  
    ---  ------                   --------------  -----  
     0   INCIDENT_KEY             28562 non-null  int64  
     1   OCCUR_DATE               28562 non-null  object 
     2   OCCUR_TIME               28562 non-null  object 
     3   BORO                     28562 non-null  object 
     4   LOC_OF_OCCUR_DESC        2966 non-null   object 
     5   PRECINCT                 28562 non-null  int64  
     6   JURISDICTION_CODE        28560 non-null  float64
     7   LOC_CLASSFCTN_DESC       2966 non-null   object 
     8   LOCATION_DESC            13585 non-null  object 
     9   STATISTICAL_MURDER_FLAG  28562 non-null  bool   
     10  PERP_AGE_GROUP           19218 non-null  object 
     11  PERP_SEX                 19252 non-null  object 
     12  PERP_RACE                19252 non-null  object 
     13  VIC_AGE_GROUP            28562 non-null  object 
     14  VIC_SEX                  28562 non-null  object 
     15  VIC_RACE                 28562 non-null  object 
     16  X_COORD_CD               28562 non-null  float64
     17  Y_COORD_CD               28562 non-null  float64
     18  Latitude                 28503 non-null  float64
     19  Longitude                28503 non-null  float64
     20  Lon_Lat                  28503 non-null  object 
    dtypes: bool(1), float64(5), int64(2), object(13)
    memory usage: 4.4+ MB


## Data Clean-up

1. Missing data (Nulls)
2. Data Types
3. Inconsistent values
4. Duplicates
5. Outliers


```python
df.isnull().sum()
```




    INCIDENT_KEY                   0
    OCCUR_DATE                     0
    OCCUR_TIME                     0
    BORO                           0
    LOC_OF_OCCUR_DESC          25596
    PRECINCT                       0
    JURISDICTION_CODE              2
    LOC_CLASSFCTN_DESC         25596
    LOCATION_DESC              14977
    STATISTICAL_MURDER_FLAG        0
    PERP_AGE_GROUP              9344
    PERP_SEX                    9310
    PERP_RACE                   9310
    VIC_AGE_GROUP                  0
    VIC_SEX                        0
    VIC_RACE                       0
    X_COORD_CD                     0
    Y_COORD_CD                     0
    Latitude                      59
    Longitude                     59
    Lon_Lat                       59
    dtype: int64



#### 1. Missing Data (Nulls)


```python
# Dropping the entire columns that are missing values and I am not interested in my analysis
df = df.drop(columns = ['LOC_OF_OCCUR_DESC','LOC_CLASSFCTN_DESC','PERP_AGE_GROUP','PERP_SEX','PERP_RACE','Lon_Lat','LOCATION_DESC'])
```


```python
# Dropping Rows with missing values
df = df.dropna(subset = ['Latitude'])
df = df.dropna(subset = ['JURISDICTION_CODE'])
```

#### 2. Data Types


```python
# Converting OCCUR_Date and time to proper date and time format as well as BORO and STATISTICAL_MURDER_FLAG to categorical formats

df['OCCUR_DATE'] = pd.to_datetime(df['OCCUR_DATE'], errors = 'coerce')
df['OCCUR_TIME'] = pd.to_datetime(df['OCCUR_TIME'], format = '%H:%M:%S', errors = 'coerce').dt.time
df['BORO'] = df['BORO'].astype('category')
df['STATISTICAL_MURDER_FLAG'] = df['STATISTICAL_MURDER_FLAG'].astype('category')

df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 28501 entries, 0 to 28561
    Data columns (total 14 columns):
     #   Column                   Non-Null Count  Dtype         
    ---  ------                   --------------  -----         
     0   INCIDENT_KEY             28501 non-null  int64         
     1   OCCUR_DATE               28501 non-null  datetime64[ns]
     2   OCCUR_TIME               28501 non-null  object        
     3   BORO                     28501 non-null  category      
     4   PRECINCT                 28501 non-null  int64         
     5   JURISDICTION_CODE        28501 non-null  float64       
     6   STATISTICAL_MURDER_FLAG  28501 non-null  category      
     7   VIC_AGE_GROUP            28501 non-null  object        
     8   VIC_SEX                  28501 non-null  object        
     9   VIC_RACE                 28501 non-null  object        
     10  X_COORD_CD               28501 non-null  float64       
     11  Y_COORD_CD               28501 non-null  float64       
     12  Latitude                 28501 non-null  float64       
     13  Longitude                28501 non-null  float64       
    dtypes: category(2), datetime64[ns](1), float64(5), int64(2), object(4)
    memory usage: 2.9+ MB


#### 3. Inconsistant Values


```python
# Checking the consistancy of categorical data types

print(df['BORO'].unique())
print(df['STATISTICAL_MURDER_FLAG'].unique())
print(df['VIC_AGE_GROUP'].unique())
print(df['VIC_SEX'].unique())
print(df['VIC_RACE'].unique())
```

    ['BRONX', 'BROOKLYN', 'MANHATTAN', 'QUEENS', 'STATEN ISLAND']
    Categories (5, object): ['BRONX', 'BROOKLYN', 'MANHATTAN', 'QUEENS', 'STATEN ISLAND']
    [False, True]
    Categories (2, bool): [False, True]
    ['18-24' '25-44' '<18' '45-64' '65+' 'UNKNOWN' '1022']
    ['M' 'F' 'U']
    ['BLACK' 'WHITE HISPANIC' 'BLACK HISPANIC' 'ASIAN / PACIFIC ISLANDER'
     'WHITE' 'UNKNOWN' 'AMERICAN INDIAN/ALASKAN NATIVE']



```python
df['VIC_SEX'] = df['VIC_SEX'].replace({'M': 'Male', 'F':'Female', 'U': 'Unknown'})
```


```python
# Check if any coordinates are out of bounds

#print(df[(df['Latitude'] < -90) | (df['Latitude'] > 90) |
 #   (df['Longitude'] < -180) | (df['Longitude'] > 180)])
```

#### 4. Duplicates


```python
df['INCIDENT_KEY'].duplicated().sum()
```




    6152




```python
# Check for duplicate rows

df = df.drop_duplicates(subset = ['INCIDENT_KEY'], keep = 'first')
```


```python
#df = df.drop_duplicates()
```

<h1 style="color:red">The purpose of using data visualization:</h1>

In this project, I am using data visualization for <b><p style="color:red"> Two main reasons:</p> </b>
- To explore the data I am working with and extract key information for my analysis, and 
- To present my findings through storytelling.

# Exploratory Data Analysis (EDA)

#### Descriptive statistics

Getting a sense of the distribution and central tendencies of the numerical columns


```python
# Summary statistics

summary_stats = df.describe()

# display the summary statistics
print(summary_stats)
```

           INCIDENT_KEY                     OCCUR_DATE      PRECINCT  \
    count  2.234900e+04                          22349  22349.000000   
    mean   1.274007e+08  2014-06-10 17:58:39.781645568     65.947201   
    min    9.953245e+06            2006-01-01 00:00:00      1.000000   
    25%    6.612572e+07            2009-09-24 00:00:00     44.000000   
    50%    9.305331e+07            2013-10-11 00:00:00     69.000000   
    75%    2.015739e+08            2019-08-23 00:00:00     81.000000   
    max    2.797581e+08            2023-12-29 00:00:00    123.000000   
    std    7.742855e+07                            NaN     27.209352   
    
           JURISDICTION_CODE    X_COORD_CD     Y_COORD_CD      Latitude  \
    count       22349.000000  2.234900e+04   22349.000000  22349.000000   
    mean            0.333751  1.009424e+06  207616.134981     40.736487   
    min             0.000000  9.149281e+05  125756.718750     40.511586   
    25%             0.000000  1.000001e+06  182712.109375     40.668137   
    50%             0.000000  1.007628e+06  193873.562500     40.698697   
    75%             0.000000  1.016824e+06  239162.921875     40.823090   
    max             2.000000  1.066815e+06  271127.687500     40.910818   
    std             0.743974  1.839076e+04   31773.161144      0.087216   
    
              Longitude  
    count  22349.000000  
    mean     -73.909151  
    min      -74.249303  
    25%      -73.943173  
    50%      -73.915703  
    75%      -73.882355  
    max      -73.702046  
    std        0.066316  


#### Visual distributions of data


```python
df[['Latitude', 'Longitude', 'PRECINCT']].hist(bins = 20, figsize = (12, 8))
plt.suptitle('Histogram of Latitude, Longitude, and PRECINCT')
plt.show
```




    <function matplotlib.pyplot.show(close=None, block=None)>




    
![png](output_25_1.png)
    


### Exploratory Data Analysis of Geographic and Precinct Distribution:

The initial analysis of the dataset reveals distinct patterns in the geographic distribution of incidents. The latitude values for incidents are predominantly concentrated between <span style="color:blue">40.50 and 40.90</span>, with the most frequent occurrences near <span style="color:blue"> 40.65 and 40.80</span>. This bimodal distribution suggests two primary clusters of incidents within these latitudinal bands, potentially pointing to specific areas or neighborhoods with higher crime rates or incidents.

The longitude values, ranging between <span style="color:blue"> -74.0 and -73.7 </span>, show a peak around -73.90, indicating that incidents are geographically concentrated within specific longitudinal areas. This concentration likely corresponds to urban areas, as the longitude range falls within the coordinates for New York City and its surrounding regions.

When analyzing the PRECINCT data, the distribution of incidents is uneven, with higher frequencies observed in precincts numbered <span style="color:blue">30-50 and 60-80</span>. This could reflect the geographical size and population density of these precincts or indicate that they are more heavily monitored or reported on. The lower frequency in precincts with higher numbers (above 100) may suggest either a less dense population in those areas or lower reporting rates.

I will explore the details further by creating visualizations for the categorical data.



#### Visualizing Categorical Data


```python


# Countplot for 'BORO'
plt.figure(figsize = (8, 6))
sns.countplot(x = 'BORO', data = df)
plt.title('Frequency of Incidents by BORO')
plt.show()

# Countplot for 'VIC_SEX'
plt.figure(figsize = (8, 6))
sns.countplot(x = 'VIC_SEX', data = df)
plt.title('Frequency of Incidents by Victim Sex')
plt.show()

# Countplot for 'VIC_RACE'
plt.figure(figsize = (8, 6))
sns.countplot(x = 'VIC_RACE', data = df)
plt.title('Frequency of Incidents by Victim Race')
plt.xticks(rotation = 45)
plt.show()
```


    
![png](output_28_0.png)
    



    
![png](output_28_1.png)
    



    
![png](output_28_2.png)
    


1. <span style="color:darkred">Black males</span> comprise more than 75% of all victims.
2. Most shootings occur in <span style="color:darkred">Brooklyn</span>, followed by the Bronx, while Staten Island has the fewest incidents.

### 1. Geospatial Mapping




```python
# Scotter plot of latitude vs. Longitude

plt.figure(figsize = (10, 6))
plt.scatter(df['Longitude'], df['Latitude'], alpha = 0.5, s=10)
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.title('Geospatial Distribution of Incidents')
plt.show()
```


    
![png](output_31_0.png)
    



```python
# Hexbin plot for better visualization of dense areas

plt.figure(figsize = (10, 6))
plt.hexbin(df['Longitude'], df['Latitude'], gridsize = 50, cmap = 'YlOrRd')
plt.colorbar(label = 'Incident Density')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.title('Heatmap of Incident Density')
plt.show()
```


    
![png](output_32_0.png)
    


### 2. Precinct Analysis


```python
# Countplot for PRECINCT distribution

plt.figure(figsize = (12, 6))
sns.countplot(x = 'PRECINCT', data=df, palette = 'Set2', hue = False, legend = False, order =  df['PRECINCT'].value_counts().index)
plt.title('Frequency of Incidents by Precinct')
plt.xlabel('Precinct')
plt.ylabel('Number of Incidents')
plt.xticks(rotation = 90) # Rotate x-axis label 90 degree for better readability
plt.show()
```


    
![png](output_34_0.png)
    



```python
# Top 10 Precinct

top_precincts = df['PRECINCT'].value_counts().head(10)

plt.figure(figsize = (10, 6))
top_precincts.plot(kind = 'bar', color = 'lightgrey')
plt.title('Top 10 Precinct with Most Incidents')
plt.xlabel('Precinct')
plt.ylabel('Number of Incidents')
plt.show()
```


    
![png](output_35_0.png)
    


### 3. Time-based Analysis

#### Frequency of Incidents Over Time (By Year)


```python
# Extract year from OCCUR_DATE

df['Year'] = df['OCCUR_DATE'].dt.year

# Group by Year and count the number of incidents
incidents_per_year = df.groupby('Year').size()

# Plot the frequency of incidents by Year
plt.figure(figsize = (10, 6))
incidents_per_year.plot(kind = 'bar', color = 'lightgray')
plt.title('Incidents Frequency by Year')
plt.xlabel('Year')
plt.ylabel('Number of Incidents')
plt.show()
```


    
![png](output_38_0.png)
    


#### Frequency of Incidents Over time (By Month)


```python
# Extract month from OCCUR_DATE

df['Month'] = df['OCCUR_DATE'].dt.month

# Group by month and count the number of incidents
incidents_per_month = df.groupby('Month').size()

# plot the frequency of incidents by Month
plt.figure(figsize = (10, 6))
incidents_per_month.plot(kind = 'bar', color = 'lightsteelblue')
plt.title('Incidens Frequesncy by Month')
plt.xlabel('Month')
plt.ylabel('Number of Incidents')
plt.xticks(rotation = 0)
plt.show()
```


    
![png](output_40_0.png)
    


#### Frequency of Incidents Ovet Time (By Day)


```python
# Extract day of the week (0 = Monday, 6 = Sunday)
df['DayOfWeek'] = df['OCCUR_DATE'].dt.dayofweek

# Group by day of the week and count the number of incidents
incidents_per_day = df.groupby('DayOfWeek').size()

# Plot thge frequency of incidents by day of the week
plt.figure(figsize = (10, 6))
incidents_per_day.plot(kind = 'bar', color = 'gray')
plt.title('Incidents Frequency by Day of Week')
plt.xlabel('Day of the Week')
plt.ylabel('Number of Incidents')
plt.xticks(ticks = range(7), labels = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'])
plt.show()
```


    
![png](output_42_0.png)
    


The seasonality pattern indicates that most shootings occur in <span style="color:darkred">June, July, and August</span>, particularly on weekends.

# Storytelling


### Incidents Trend over time


```python
# # Group by year and count incidents
incidents_by_year = df['Year'].value_counts().sort_index()
plt.figure(figsize = (10, 7))

# line chart
plt.plot(incidents_by_year.index, incidents_by_year.values, marker = 'o', linestyle = '-', color = 'steelblue')

# Convert year index to 2-digit format for x-axis labels
two_digit_years = [str(year) [-2:] for year in incidents_by_year.index]
plt.xticks(ticks = incidents_by_year.index, labels = two_digit_years)

# Add a Storytelling title at the top (outside the plot area)
plt.suptitle("Sharp drop followed by a pandemic-era Spike: A 17-year look at NYC incidents Trends",
            fontsize = 12, fontweight = 'bold', x = 0.0, ha = 'left')

plt.title("Incidents steadily declined until 2018, \nthen surged during 2021-2021 before dropping again.", 
          fontsize = 11, loc = 'left', pad = 20)

# Axis labels
plt.xlabel('Year')
plt.ylabel('Number of Incidents')

# Styling: Clear background, remover top/right borders
plt.gca().set_facecolor('white')
plt.gca().spines['top'].set_visible(False)
plt.gca().spines['right'].set_visible(False)

# Grid only along Y for readibility
plt.grid(axis = 'y', linestyle = '--', alpha = 0.5)


plt.tight_layout()
plt.show()

```


    
![png](output_45_0.png)
    


### Comparative analysis of incidents resulted in fatal vs. non-fatal.


```python
# Group by Year and STATISTICAL_MURDER_FLAG, then count
murder_trends = df.groupby(['Year', 'STATISTICAL_MURDER_FLAG'], observed = True).size().unstack()

# plotting
plt.figure(figsize = (10, 7))

# Two digit years label
two_digit_years = [str(y)[-2:] for y in murder_trends.index]
plt.xticks(ticks = murder_trends.index, labels = two_digit_years)

# Plot both lines
plt.plot(murder_trends.index, murder_trends[True], marker = 'o', linestyle = '-', color = 'crimson')
plt.plot(murder_trends.index, murder_trends[False], marker = 'o', linestyle = '-', color = 'steelblue')

# Add direct labels at the end of the lines
plt.text(murder_trends.index[-1] + 0.2,
         murder_trends[True].iloc[-1],
         'Fatal Incidents',
         color = 'crimson',
         va = 'center',
         fontsize = 9)

plt.text(murder_trends.index[-1] + 0.2,
         murder_trends[False].iloc[-1],
         'Non-Fatal Incidents',
         color = 'steelblue',
         va = 'center',
         fontsize = 9)

# Titles (left-aligned)
plt.suptitle("How Fatal Are the NYC Incidents Over Time? (2006-2023)",
             fontsize = 12, fontweight = 'bold', x=0.0, ha = 'left')
plt.title("While non-fatal incidents dominate, fatal incidents show distenct trend worth watching.",
          fontsize = 11, loc = 'left', pad = 20)

# Labels and Styling
plt.xlabel('Year')
plt.ylabel('Number of Incidents')
plt.grid(axis = 'y', linestyle = '--', alpha = 0.5)

# Clean background and borders
ax = plt.gca()
ax.set_facecolor('white')
ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)

plt.tight_layout()
plt.show()

```


    
![png](output_47_0.png)
    


### Compareson analysis BORO and Fatal Incidents over time



```python
# Filter to Fatal Incidents Only
fatal_data = df[df['STATISTICAL_MURDER_FLAG'] == True]

# Group by Year and BORO
fatal_by_year_boro = fatal_data.groupby(['Year', 'BORO'], observed = True).size().unstack()

# Plot
plt.figure(figsize = (11, 7))

# 2-digit year labels
two_digit_years = [str(y)[-2:] for y in fatal_by_year_boro.index]
plt.xticks(ticks=fatal_by_year_boro.index, labels=two_digit_years, rotation=0)

# Set the focus Boro with highest number of Incidents
focus_boro = 'BROOKLYN'

# Loop to plot each line
for boro in fatal_by_year_boro.columns:
    if boro == focus_boro:
        plt.plot(fatal_by_year_boro.index, fatal_by_year_boro[boro],
                 marker = 'o', linestyle = '-', linewidth = 2.5, color = 'crimson', zorder = 3)
    else:
        plt.plot(fatal_by_year_boro.index, fatal_by_year_boro[boro],
                 marker = 'o', linestyle = '-', linewidth = 1.2, color = 'lightgray', zorder = 1)

# Add direct labels
# Add direct labels to the end of each line
for boro in fatal_by_year_boro.columns:
    y_val = fatal_by_year_boro[boro].iloc[-1]
    plt.text(fatal_by_year_boro.index[-1] + 0.2, y_val, boro, fontsize = 9,
             color = plt.gca().lines[fatal_by_year_boro.columns.get_loc(boro)].get_color())


# Titles (left-aligned)
plt.suptitle("Brooklyn Leads in Fatal Incidents Over Time (2006-2023)",
             fontsize = 12, fontweight = 'bold', x = 0.0, ha = 'left')
plt.title("While all borough show fluctuations, Brooklyn consistently reports the highest fatality numbers.",
          fontsize = 11, loc = 'left', pad = 20)

# Labels and styling
plt.xlabel('Year')
plt.ylabel('Number of Fatal Incidents')
plt.grid(axis = 'y',  linestyle = '--', alpha = 0.4)

# Clean visuals
ax = plt.gca()
ax.set_facecolor('white')
ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)

plt.tight_layout()
plt.show()

```


    
![png](output_49_0.png)
    


# Interactive Data Visualization


```python
import plotly.graph_objects as go

# Filter for fatal incidents
fatal_data = df[df['STATISTICAL_MURDER_FLAG'] == True]

# Group by year and BORO
fatal_by_year_boro = fatal_data.groupby(['Year', 'BORO'], observed = True).size().unstack()


default_boro = 'BRONX'  # or whichever you want highlighted first

boro_list = fatal_by_year_boro.columns.tolist()
years = fatal_by_year_boro.index.tolist()

fig = go.Figure()
highlight_traces = {}
muted_traces = {}

for i, boro in enumerate(boro_list):
    # Muted trace (always visible)
    fig.add_trace(go.Scatter(
        x=years,
        y=fatal_by_year_boro[boro],
        mode='lines+markers',
        name=boro,
        line=dict(color='lightgray', width=1),
        marker=dict(size=5),
        showlegend=True
    ))

for i, boro in enumerate(boro_list):
    # Highlighted trace (only one visible at a time)
    trace_index = len(boro_list) + i  # because muted traces come first
    highlight_traces[boro] = trace_index

    fig.add_trace(go.Scatter(
        x=years,
        y=fatal_by_year_boro[boro],
        mode='lines+markers+text',
        name=f"{boro} (highlight)",
        line=dict(color='crimson', width=3),
        marker=dict(size=6),
        text=[boro if j == len(years)-1 else '' for j in range(len(years))],
        textposition='middle right',
        showlegend=False,
        visible=(boro == default_boro)
    ))

buttons = []

for boro in boro_list:
    # 5 muted traces = always visible
    # 5 highlight traces = all False except selected
    vis = [True]*len(boro_list) + [False]*len(boro_list)
    vis[highlight_traces[boro]] = True  # only show selected highlight

    buttons.append(dict(
        label=boro,
        method='update',
        args=[
            {'visible': vis},
            {'title': f'Fatal Incidents in {boro} (2006–2023)'}
        ]
    ))



fig.update_layout(
    width=1100,
    height=600,
    title=f'Fatal Incidents in {default_boro} (2006–2023)',
    xaxis_title='Year',
    yaxis_title='Number of Fatal Incidents',
    plot_bgcolor='white',
    font=dict(size=12),
    updatemenus=[dict(
        buttons=buttons,
        direction='down',
        x=0.0,
        xanchor='left',
        y=1.2,
        yanchor='top'
    )],
    margin=dict(t=180),
    hovermode='x unified'
)

```


<div>                            <div id="b9c53780-fae2-4c5d-b43f-e94912d87838" class="plotly-graph-div" style="height:600px; width:1100px;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("b9c53780-fae2-4c5d-b43f-e94912d87838")) {                    Plotly.newPlot(                        "b9c53780-fae2-4c5d-b43f-e94912d87838",                        [{"line":{"color":"lightgray","width":1},"marker":{"size":5},"mode":"lines+markers","name":"BRONX","showlegend":true,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[91,71,66,67,68,84,56,44,48,45,48,34,42,33,52,89,73,53],"type":"scatter"},{"line":{"color":"lightgray","width":1},"marker":{"size":5},"mode":"lines+markers","name":"BROOKLYN","showlegend":true,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[131,133,114,118,134,101,92,76,65,89,87,49,54,48,113,88,77,62],"type":"scatter"},{"line":{"color":"lightgray","width":1},"marker":{"size":5},"mode":"lines+markers","name":"MANHATTAN","showlegend":true,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[37,33,30,23,33,27,17,16,19,19,18,13,11,23,36,41,37,34],"type":"scatter"},{"line":{"color":"lightgray","width":1},"marker":{"size":5},"mode":"lines+markers","name":"QUEENS","showlegend":true,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[43,34,49,35,43,42,40,22,24,33,22,21,30,22,37,51,38,19],"type":"scatter"},{"line":{"color":"lightgray","width":1},"marker":{"size":5},"mode":"lines+markers","name":"STATEN ISLAND","showlegend":true,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[7,7,10,9,6,7,4,2,9,10,4,7,3,5,14,11,6,7],"type":"scatter"},{"line":{"color":"crimson","width":3},"marker":{"size":6},"mode":"lines+markers+text","name":"BRONX (highlight)","showlegend":false,"text":["","","","","","","","","","","","","","","","","","BRONX"],"textposition":"middle right","visible":true,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[91,71,66,67,68,84,56,44,48,45,48,34,42,33,52,89,73,53],"type":"scatter"},{"line":{"color":"crimson","width":3},"marker":{"size":6},"mode":"lines+markers+text","name":"BROOKLYN (highlight)","showlegend":false,"text":["","","","","","","","","","","","","","","","","","BROOKLYN"],"textposition":"middle right","visible":false,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[131,133,114,118,134,101,92,76,65,89,87,49,54,48,113,88,77,62],"type":"scatter"},{"line":{"color":"crimson","width":3},"marker":{"size":6},"mode":"lines+markers+text","name":"MANHATTAN (highlight)","showlegend":false,"text":["","","","","","","","","","","","","","","","","","MANHATTAN"],"textposition":"middle right","visible":false,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[37,33,30,23,33,27,17,16,19,19,18,13,11,23,36,41,37,34],"type":"scatter"},{"line":{"color":"crimson","width":3},"marker":{"size":6},"mode":"lines+markers+text","name":"QUEENS (highlight)","showlegend":false,"text":["","","","","","","","","","","","","","","","","","QUEENS"],"textposition":"middle right","visible":false,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[43,34,49,35,43,42,40,22,24,33,22,21,30,22,37,51,38,19],"type":"scatter"},{"line":{"color":"crimson","width":3},"marker":{"size":6},"mode":"lines+markers+text","name":"STATEN ISLAND (highlight)","showlegend":false,"text":["","","","","","","","","","","","","","","","","","STATEN ISLAND"],"textposition":"middle right","visible":false,"x":[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020,2021,2022,2023],"y":[7,7,10,9,6,7,4,2,9,10,4,7,3,5,14,11,6,7],"type":"scatter"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"font":{"size":12},"margin":{"t":180},"width":1100,"height":600,"title":{"text":"Fatal Incidents in BRONX (2006\u20132023)"},"xaxis":{"title":{"text":"Year"}},"yaxis":{"title":{"text":"Number of Fatal Incidents"}},"plot_bgcolor":"white","updatemenus":[{"buttons":[{"args":[{"visible":[true,true,true,true,true,true,false,false,false,false]},{"title":"Fatal Incidents in BRONX (2006\u20132023)"}],"label":"BRONX","method":"update"},{"args":[{"visible":[true,true,true,true,true,false,true,false,false,false]},{"title":"Fatal Incidents in BROOKLYN (2006\u20132023)"}],"label":"BROOKLYN","method":"update"},{"args":[{"visible":[true,true,true,true,true,false,false,true,false,false]},{"title":"Fatal Incidents in MANHATTAN (2006\u20132023)"}],"label":"MANHATTAN","method":"update"},{"args":[{"visible":[true,true,true,true,true,false,false,false,true,false]},{"title":"Fatal Incidents in QUEENS (2006\u20132023)"}],"label":"QUEENS","method":"update"},{"args":[{"visible":[true,true,true,true,true,false,false,false,false,true]},{"title":"Fatal Incidents in STATEN ISLAND (2006\u20132023)"}],"label":"STATEN ISLAND","method":"update"}],"direction":"down","x":0.0,"xanchor":"left","y":1.2,"yanchor":"top"}],"hovermode":"x unified"},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('b9c53780-fae2-4c5d-b43f-e94912d87838');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


## End


```python

```


```python

```
