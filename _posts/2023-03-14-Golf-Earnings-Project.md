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

PICTURE HERE

For this project, I use PGA Tour data available from ESPN. In this post, I explain how I scraped the data from ESPN to create the data for the top 50 golfers each year on the PGA Tour for the last 5 full years. 

Complete code and data can be found in the following Github repo:
https://github.com/cambutler33/Golf_Earnings

# A Note on Ethics

I determined that how we collect the data below is aligned with good ethical practices. The data is not private or restricted data. And we do not put a strain on the ESPN site with excessive calls to the website when scraping the data.

# Data Collection

##### Step 0: Tools

pandas, requests, BeautifulSoup

PICTURE HERE

##### Step 1: Scrape First Year

PICTURE HERE OF 2022 Data FROM ESPN 

CODE
```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

##### Step 2: Rinse and Repeat 

Update years in url since table structure is same for all the years of interest

##### Step 3: Combine the Datasets

CODE
```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

##### Step 4: Drop Columns

Cleaning

CODE
```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

##### Step 5: Output Data to CSV

CODE
```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

# Conclusion

PICTURE HERE

In this post, I showed how to scrape the ESPN site and collect data on the top 50 golfers on the PGA Tour for the last 5 full years. I am particularly interested in what statistics contribute to the most earnings per year on the PGA Tour. In my next post, I will show how exploratory data analysis of this data can help me understand what attributes of one's golf game will help them win the most money on the tour.

Stay tuned for next time!






