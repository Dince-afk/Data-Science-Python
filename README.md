# Data Science in Python

Here is a compilation of data science work I have written in Python and worked over the years on. Please feel free to use, share and add to any tools.  

# Projects


## [Machine Learning - Jupyter Notebook Template](https://github.com/Dince-afk/Data-Science-Python/blob/main/0.%20Templates/2_machine_learning_template.ipynb)
- I love keeping my jupyter notebook files clean and consistent. I therefore use custom templates for various tasks. Here is my template for machine learning projects.
- Notebook includes: 
    - importing libraries and data
    - exploring the dataset: data types, missing values, metrics, visualizations.
    - preprocessing: dropping columns, imputing missing values, encoding categorical values, feature scaling.
    - splitting train and test data
- Packages: `NumPy`, `Pandas`, `Matplotlib`, `sklearn`


## [TED Talks and Climate Change](https://github.com/Dince-afk/Data_Science/blob/main/1.%20Projects%20and%20Showcases/ted_talks_climate.ipynb)
![Download](https://user-images.githubusercontent.com/68876259/170859279-77ae3739-f236-4454-9539-49471065865a.png)
- In this notebook I have analyzed TED talks that are related to climate change and environmental issues. 
- Questions: How did climate change related topics change over time? How do views and likes for different topics differ? 
- Packages: `NumPy`, `Pandas`, `re`, `Matplotlib`

---

# Tools


## [YouTube API to Database Automated Pipeline](https://github.com/Dince-afk/Data-Science-Python/blob/main/1.%20Projects%20and%20Showcases/youtube_api_db.ipynb)

- Downloading and processing data from the YouTube API and uploading it to a database.
- Packages: `requests`, `pandas`, `time`, `mysql`

```python
API_KEY = "ENTER"
CHANNEL_ID = "ENTER"

# Get video data from YouTube
df = get_videos(df)

# Connect to database
host = "ENTER"
user = "ENTER"
password = "ENTER"
database = "ENTER"
mydb = connect_to_db(host, user, password)

# Create cursor for navigating database
mycursor = mydb.cursor()

# Create table if not yet existing
create_table(mycursor)

# Update existing rows and return new rows as df
new_vid_df = update_db(mycursor, df)

# Appending new rows to table
append_from_df_to_db(mycursor, new_vid_df) 

# Commit all changes
mydb.commit() 
```

---

## [Get Twitter Data with Help from Tweepy and Pandas](https://github.com/Dince-afk/Data-Science-Python/blob/main/1.%20Projects%20and%20Showcases/tweepy_pandas_data.ipynb)

- This program allows you to get data from recent tweets, transform it into a nice pandas DataFrame and write it to your hard drive.
- Packages: `requests`, `json`, `pandas`, `tweepy` 

**Results in:**
```
<class 'pandas.core.frame.DataFrame'>
Int64Index: 30 entries, 0 to 29
Data columns (total 12 columns):
 #   Column                        Non-Null Count  Dtype 
---  ------                        --------------  ----- 
 0   id                            30 non-null     object
 1   created_at                    30 non-null     object
 2   author_id                     30 non-null     object
 3   lang                          30 non-null     object
 4   text                          30 non-null     object
 5   source                        30 non-null     object
 6   public_metrics.retweet_count  30 non-null     int64 
 7   public_metrics.reply_count    30 non-null     int64 
 8   public_metrics.like_count     30 non-null     int64 
 9   public_metrics.quote_count    30 non-null     int64 
 10  name                          30 non-null     object
 11  username                      30 non-null     object
dtypes: int64(4), object(8)
memory usage: 3.0+ KB

```

---

## [Fetch County Value for Longitude/Latitude with OpenStreetMap API](https://github.com/Dince-afk/Data-Science-Python/blob/main/1.%20Projects%20and%20Showcases/get_county.ipynb)

- This program allows you to get the county (or else state, country, country code) for any given longitude and latitude values. Works on big dataframes. In my case I've had 17,000 rows and it took me around two hours for completion.
- Packages: `requests`, `pandas`, `time`, `mysql`, `json`, `functools`, `tqdm`, `missingno`

```python
# Caching, i.e. using past request results with the same lat and long values, is required by API provider
@cache 
def bar(lat, long):
    url = "https://nominatim.openstreetmap.org/reverse?format=geojson&lat=" +str(lat)+"&lon="+str(long)
    try:
        response = requests.get(url).json()
        response = response["features"][0]["properties"]
        county = response["address"]["county"]
        return county
    except:
        return None # In case the API call returns an error -> return None

def foo(row):
    return bar(row["latitude"], row["longitude"])
    
# Provide progress overview
tqdm.pandas() 
df["county"] = df.progress_apply(foo, axis=1)
```
