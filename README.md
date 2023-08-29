# Python_Project_1
## Introduction

- In this project, a **'Tracks Dataset'** obtained **from** the streaming plattform,**Spotify**, is presented.

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
 
- Created a new column namely 'duration' which contains data values from the 'duration_ms' column converted from milliseconds to seconds.In addittion,I dropped the duration_ms column.

   - **Code:** df_tracks["duration"]=df_tracks["duration_ms"].apply(lambda x:round(x/1000))
   
   - **Code 2:** df_tracks.drop("duration_ms",inplace=True,axis=1)
 
   - To confirm that the column has been created successfully,I run the **code:** df_tracks.duration.head()
 
- Created a sample dataset(namely:'sample_df') from the existing dataset.This sample dataset is intented to make the EDA faster and more efficcient.The sample dataset contains 2346 records.

     - **Code:**  sample_df=df_tracks.sample(int(0.004*len(df_tracks))) , print(len(sample_df))

  
 
  
  
