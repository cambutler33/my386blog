---
layout: post
title:  "Golf Earnings Project- Part 3: Data Story"
author: Cameron Butler
description: Culmination of PGA Tour Golf Earnings Data Project
image: /assets/images/golf3.png
---

# Recap

For a little context regarding this project, professional golfers are able to make more money on the PGA Tour than ever before. A golfer's season earnings are dependent on their success-- win more (of the more popular tournaments) and make more money. Throughout this project, I wanted to see what factors contribute most to golfers winning the most money during a season on the PGA Tour. Examples of attributes that were considered were driving distance, driving accuracy, putts per hole, birdies per round, etc. 

In parts 1 and 2, I showed how to both [scrape and compile the data](https://cambutler33.github.io/my386blog/2023/03/14/Golf-Earnings-Project.html), and I [performed an exploratory data analysis](https://cambutler33.github.io/my386blog/2023/03/29/Golf-Earnings-EDA.html), respectively. I looked at the top 50 golfers for the past 5 complete years on the PGA Tour for this project. The data [came from ESPN](https://www.espn.com/golf/stats/player/_/season/2022).

# Findings

![Figure](https://raw.githubusercontent.com/cambutler33/my386blog/main/assets/images/DataStory.png)

After performing an analysis on the scraped dataset, I found that besides wins, the variable that has the highest correlation with earnings per year is birdies per round. If a golfer can consistently get birdies, then they have a shot at earning a large amount of money throughout the year.

This may be surprising that birdies per round are more highly correlated with earnings per year than driving distance/accuracy. But as our data tells us, get birdies and get paid.

(Note: a birdie is when you shoot 1-under par on a given hole. In other words, that is a good hole and golfers want the most birdies as possible.)

# Repo Link

The complete code and data can be found in this [Github repo](https://github.com/cambutler33/Golf_Earnings).
