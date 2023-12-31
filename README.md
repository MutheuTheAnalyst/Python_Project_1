# Python_Project_1
## Introduction

- In this project, a **'Tracks Dataset'** obtained **from** the streaming plattform,**Spotify**, is presented.

- The link to the dataset is as given: [link](https://www.kaggle.com/datasets/zaheenhamidani/ultimate-spotify-tracks-db)

- My **aim** is to **perform exploratory data analysis** on the dataset **using the 'Python Programming Language'** on the **Jupyter Notebook IDE** and **draw meaningful insights** in regards to the **performance of different tracks** on the Spotify Plattform.

## Dataset Overview
- I first **imported libraries** that shall be useful in performing my analysis.
  
   - **Code:** import numpy as np,import pandas as pd,import matplotlib.pyplot as plt and import seaborn as sns into my Jupyter notebook.

- I then proceeded to **import the tracks dataset(named it 'df_tracks')** and then **confirmed that it loaded correctly** by running a data overview query.
  
   - **Code 1:** df_tracks=pd.read_csv( ) and  **Code 2:** df_tracks.head( )

- **Checked for null values** across all the columns.Only the **'name column' had null values**,the values summed upto 71.
  
   - **Code:** pd.isnull(df_tracks).sum( )
  
- Obtained information about the dataset.The **dataset has a total of 20 columns and 586672 records**.In addittion, by running the code, I was able to know the **column names** and the **data types** of data values in each column.
  
  -  **Code:** df_tracks.info( )
 
  -  **Output:**

    Column            Non-Null Count   Dtype
 
 0   id                586672 non-null  object 
 
 1   name              586601 non-null  object 
 
 2   popularity        586672 non-null  int64 
 
 3   duration_ms       586672 non-null  int64
 
 4   explicit          586672 non-null  int64 
 
 5   artists           586672 non-null  object 
 
 6   id_artists        586672 non-null  object
 
 7   release_date      586672 non-null  object
 
 8   danceability      586672 non-null  float64
 
 9   energy            586672 non-null  float64
 
 10  key               586672 non-null  int64 
 
 11  loudness          586672 non-null  float64
 
 12  mode              586672 non-null  int64 
 
 13  speechiness       586672 non-null  float64
 
 14  acousticness      586672 non-null  float64
 
 15  instrumentalness  586672 non-null  float64
 
 16  liveness          586672 non-null  float64
 
 17  valence           586672 non-null  float64
 
 18  tempo             586672 non-null  float64
 
 19  time_signature    586672 non-null  int64 
 
dtypes: float64(9), int64(6), object(5)
  
   
## Exploratory Data Analysis
- For starters,I obtained the **descriptive statistics** of the data values in **each column**,i.e;count,mean,std,min,max,25%,50%,75%.

   - **Code:** df_tracks.describe( ).transpose()
  
- Obtained the **bottom 10 songs in terms of popularity**.This is so as to study the characteristics of the songs and figure out the cause of their underperformance on the Spotify plattform.

   - **Code:** sorted_df=df_tracks.sort_values('popularity',ascending=True).head(10)

- Obtained the **top 10 songs with popularity of over 90**.This is so as to study the characteristics of the songs and figure out the cause of their good performance on the Spotify plattform.

    - **Code 1:** most_popular=df_tracks.query('popularity'>90,inplace=False).sort_values('popularity',ascending=False)
 
    - **Code 2:** most_popular[:10]
 
- Obtained the **artist at the 18th position** in the dataset.From running the code,I was able to know that the artist**Victor Boucher held the 18th position**.

   - **Code:** df_tracks[artists].iloc[18]
 
- **Created a new column namely 'duration'** which contains data values from the **'duration_ms' column converted from milliseconds to seconds**.In addittion,I **dropped the duration_ms column**.

   - **Code:** df_tracks["duration"]=df_tracks["duration_ms"].apply(lambda x:round(x/1000))
   
   - **Code 2:** df_tracks.drop("duration_ms",inplace=True,axis=1)
 
   - To confirm that the column has been created successfully,I ran the **code:** df_tracks.duration.head()
 
- **Created a sample dataset(namely:'sample_df')** from the existing dataset.This sample dataset is intented to make the EDA faster and more efficcient.The sample dataset contains 2346 records.

     - **Code:**  sample_df=df_tracks.sample(int(0.004*len(df_tracks))) , print(len(sample_df))

  ## Data Visualization.
  ### 1) Heatmap to display correlation between the dataset variables.

  - The heatmap displays information about the extent of correlation between variables.The variables can either be positively correlated( 0 > x < 1) or negatively correlated(-1 > x < 0).

  - **Code:**
    
    corr_df=df_tracks.drop(["key","mode","explicit"],axis=1).corr(method='pearson')
    
    plt.figure(figsize=(14,6))
    
    heatmap=sns.heatmap(corr_df,annot=True,fmt=".1g",vmin=-1,vmax=1,center=0,cmap="inferno",linewidth=1,linecolor="Black")
    
    heatmap.set_tittle=("Correlation Heatmap between Variables")
    
    heatmap.set_xticklabels(heatmap.get_xticklabels(),rotation=90)


      
 ![image](https://github.com/MutheuTheAnalyst/Python_Project_1/assets/92978069/78dfd761-2b8c-4a1f-ab24-5d7648e2aad0)

 ### 2) Regression Plot to display the correlation between the variables 'Loudness' and 'Energy'.

 - From the visualization,it is clear to see that the two variables are highly positively correlated.

 - **Code:**
 
   plt.figure(figsize=(10,6))

   snsA.regplot(data=sample_df,y="loudness",x="energy",color="c").set(title="Loudness vs Energy Correlation")

![image](https://github.com/MutheuTheAnalyst/Python_Project_1/assets/92978069/9c97f882-7f7b-44d1-a0ef-c71455b47e7b)


### 3) Regression plot to display the correlation between the variables 'Popularity' and 'Acousticness'.

- From the visualization,we can observe that the two variables are negatively correlated.

- **Code:**
  
  plt.figure(figsize=(10,6))
  
  sns.regplot(data=sample_df,y="popularity",x="acousticness",color="b").set(title="Popularity vs Acousticness Correlation") 

 ![image](https://github.com/MutheuTheAnalyst/Python_Project_1/assets/92978069/e179f8a0-a483-4221-90b5-27d1a37c6f3a)

 ### 4) Histogram plot to display the number of songs available per year.

 - From the visualization, we can observe that there was an increasing trend in the songs available from the the year 1980 towards the year 2000.However,by the year 2000, there  was a drastic drop in numbers followed by a steady growth towards the year 2010.

 -  **Code:**

    df_tracks["dates"]=df_tracks.index.get_level_values("release_date")
   
    df_tracks.dates=pd.to_datetime(df_tracks.dates)
   
    years=df_tracks.dates.dt.year

    sns.displot(years,discrete=True,aspect=2,height=5,kind="hist").set(title="Number of songs per year.")

  ![image](https://github.com/MutheuTheAnalyst/Python_Project_1/assets/92978069/7afb6ce0-4be0-40aa-864d-4a4489cf7416)

  ### 5) Line graph to showcase the average duration of songs over the years.

  - From the visualization, we can observe that there was a fluctuating upwards and downward trend in relation to the the duration of songs throughout the time period.However, over the last 20 years(from 2000-2020), it is evident  that there has been a steady decline in the songs' duration.
  
  - **Code:**

    total_dr=df_tracks.duration
    
    sns.set_style(style="whitegrid")
    
    fig_dims=(10,5)
    
    fig,ax=plt.subplots(figsize=fig_dims)
    
    fig=sns.lineplot(x=years,y=total_dr,ax=ax).set(title="Year Vs Duration")
    
    plot.xticks(rotation=90)

![image](https://github.com/MutheuTheAnalyst/Python_Project_1/assets/92978069/246b4719-805b-4c01-94db-25f914cc7dd5)




 

  
  
