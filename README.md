# Data Science in Python

Here is a compilation of data science work I have written in Python and worked over the years on.

## Projects

### [TED Talks and Climate Change](https://github.com/Dince-afk/Data_Science/blob/main/1.%20Projects%20and%20Showcases/ted_talks_climate.ipynb)
![Download](https://user-images.githubusercontent.com/68876259/170859279-77ae3739-f236-4454-9539-49471065865a.png)
- In this notebook I have analyzed TED talks that are related to climate change and environmental issues. 
- Questions: How did climate change related topics change over time? How do views and likes for different topics differ? 
- Tools: `NumPy`, `Pandas`, `re`, `Matplotlib`

## Programs

### [YouTube API to Database Automated Pipeline](https://github.com/Dince-afk/Data_Science/blob/main/1.%20Projects%20and%20Showcases/youtube_api_db.ipynb)

```python
API_KEY = "ENTER"
CHANNEL_ID = "ENTER"

df = pd.DataFrame(columns=["video_id","video_title","upload_date","view_count","like_count","favorite_count","comment_count"]) # Create empty df for later appending

df = get_videos(df) # Function fetching data and returning df

host = "ENTER"
user = "ENTER"
password = "ENTER"
database = "ENTER"
mydb = connect_to_db(host, user, password) # Connect to database
mycursor = mydb.cursor() # Create cursor navigator

create_table(mycursor) # Create "videos" table if not yet existing
new_vid_df = update_db(mycursor, df) # Update existing rows and return new rows as df
append_from_df_to_db(mycursor, new_vid_df) # Appending new rows to table
mydb.commit() # Committing all changes
```

- Downloading and processing data from the YouTube API and uploading it to a database.
- Tools: `requests`, `pandas`, `time`, `mysql`

