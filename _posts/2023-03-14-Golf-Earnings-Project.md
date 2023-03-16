---
layout: post
title:  "Golf Earnings Project: Data Collection"
author: Cameron Butler
description: Overview of web scraping steps for Golf Earnings Data Project.
image: /assets/images/golf.png
---

# Introduction

Golf is a historic sport with a rich history. In the past few years, golfers on the PGA Tour have been able to make more money than ever thanks to the prize money for winning tournaments. 

During the PGA Tour season, the golfers participate in tournaments each week from Thursday through Sunday. Each day, the golfers play the course, which is always 18 holes long. After Friday, players will be cut from the tournament based off of scores, and the remaining golfers compete for the victory and prize money on Saturday and Sunday. 

The golfer that wins first place wins the most money with runner-ups earning less. Each tournaments prize money is different, but generally the more popular and important tournaments have a larger purse.  

![Figure](https://github.com/cambutler33/my386blog/raw/main/assets/images/JTpga.jpg)

For this project, I use PGA Tour data available from ESPN. In this post, I explain how I scraped the data from ESPN to create the data for the top 50 golfers each year on the PGA Tour for the last 5 full years. 

Please note that this blog is not meant to be a comprehensive guide to pulling the data. It is merely a summary. The complete code and data can be found in the following Github repo:
https://github.com/cambutler33/Golf_Earnings

# A Note on Ethics

I determined that how we collect the data below is aligned with good ethical practices. The data is not private or restricted data. And we do not put a strain on the ESPN site with excessive calls to the website when scraping the data.

# Data Collection

### Step 0: Tools

For this webscraping process, I used the pandas, requests, and BeautifulSoup packages.

### Step 1: Scrape First Year

![Figure](https://github.com/cambutler33/my386blog/raw/main/assets/images/espn.png)

```
# 2022 data
# URL of the page to scrape
url = "https://www.espn.com/golf/stats/player/_/season/2022/"

# Make a GET request to the URL and store the response
response = requests.get(url)

# Parse the HTML content of the page using BeautifulSoup
soup = BeautifulSoup(response.content, 'html.parser')

# Find the table containing the player data
table = soup.find('table', class_='Table Table--align-right')

# Get the table headers
headers = [th.text.strip() for th in table.find_all('th')]

# Initialize a list to store the player data
player_data = []

# Loop through each row in the table (skipping the header row)
for tr in table.find_all('tr')[1:]:
    # Get the data for each column in the row
    tds = tr.find_all('td')
    # Initialize a dictionary to store the player's data
    player = {}
    # Loop through each column and add the data to the dictionary
    for i in range(len(headers)):
        player[headers[i]] = tds[i].text.strip()
    # Add the player's data to the list
    player_data.append(player)
    # Stop the loop after 250 players have been scraped
    if len(player_data) == 250:
        break
df22_1 = pd.DataFrame(player_data)
```

```
# The URL of the page we want to scrape
url = "https://www.espn.com/golf/stats/player/_/season/2022/table/general/sort/amount/dir/desc/"

# Send an HTTP request to the URL
response = requests.get(url)

# Parse the HTML content of the page using BeautifulSoup
soup = BeautifulSoup(response.content, 'html.parser')

# Find the table containing the player data
table = soup.find('table')

# Extract the table headers
headers = []
for th in table.find_all('th'):
    headers.append(th.text.strip())

# Extract the player data
players = []
for tr in table.find_all('tr')[1:]:
    player_data = []
    for td in tr.find_all('td'):
        player_data.append(td.text.strip())
    players.append(player_data)

df22_2 = pd.DataFrame(players)
df22_2.columns = ['Rank', 'Name', 'Age']
```

```
data_2022 = df22_2.join(df22_1)
data_2022
```

### Step 2: Rinse and Repeat 

In order to grab the data for 2021, 2020, 2019, and 2018, all we need to do is the same steps but change the urls. This is possible since the table structure is the same for all the years of interest.

```
url = "https://www.espn.com/golf/stats/player/_/season/2021/"
url = "https://www.espn.com/golf/stats/player/_/season/2021/table/general/sort/amount/dir/desc/"
url = "https://www.espn.com/golf/stats/player/_/season/2020/"
url = "https://www.espn.com/golf/stats/player/_/season/2020/table/general/sort/amount/dir/desc/"
# and so on...
```

### Step 3: Combine the Datasets

Once we have the datasets for each year, we need to combine all 5 into 1 dataframe. We can easily do this thanks to pandas. 

```
dfGolf = pd.concat([data_2022, data_2021, data_2020, data_2019, data_2018], ignore_index=True,axis=0)
```

### Step 4: Drop Columns and Cleaning

After combining the datasets, we need to drop the columns we don't want, ensure that the data in each column is the correct data type, and rename the columns how we want. We accomplish that with the following:

```
dfGolf2 = dfGolf.drop(columns = ['Name', 'Rank', 'CUP', 'Age', 'EVNTS'])
```

```
dfGolf2['EARNINGS'] = dfGolf2['EARNINGS'].str.replace('$','')
dfGolf2['EARNINGS'] = dfGolf2['EARNINGS'].str.replace(',','')

dfGolf3 = dfGolf2.astype({"EARNINGS": int, "RNDS": int, "CUTS":int, "TOP10": int, "WINS": int, "SCORE": float, "DDIS": float, "DACC": float, "GIR": float, 
                          "PUTTS": float, "SAND": float, "BIRDS": float})
```

```
dict = {'EARNINGS':'Earnings for Year',
 'RNDS':'Rounds Played',
 'CUTS':'Cuts Made',
 'TOP10': 'Top 10 Finishes',
 'WINS':'Wins',
 'SCORE':'Average Score',
 'DDIS': 'Average Driving Distance',
 'DACC':'Driving Accuracy Percentage',
 'GIR':'Greens in Regulation Percentage',
 'PUTTS':'Putts Per Hole',
 'SAND':'Save Percentage',
 'BIRDS':'Birdies Per Round'}

 dfGolf6.rename(columns=dict, inplace=True)
```

### Step 5: Output Data to CSV

```
df.to_csv('GolfEarnings.csv', index=False)
```

# Conclusion

![Figure](https://github.com/cambutler33/my386blog/raw/main/assets/images/masters.jpg)

In this post, I showed how to scrape the ESPN site and collect data on the top 50 golfers on the PGA Tour for the last 5 full years. I am particularly interested in what statistics contribute to the most earnings per year on the PGA Tour. In my next post, I will show how exploratory data analysis of this data can help me understand what attributes of one's golf game will help them win the most money on the tour.

Stay tuned for next time!






