---
title: Mixing Up Your Office March Madness Competition
author: Mark Nielsen
date: '2019-03-14'
slug: mixing-up-march-madness
categories:
  - Programming
tags:
  - shiny
  - NCAAcalcutta
  - iterator
  - r-package
banner: 'banners/NCAA_March_Madness_logo_2016.jpg'
description: ''
images: []
menu: ''
---

March Madness is almost here! Try mixing up your office bracket competition with a Calcutta auction instead. I think the original source of this idea came from a news article similar to [this one](https://www.post-gazette.com/sports/marchmadness/2006/03/13/Calcutta-auction-Brainy-twist-on-traditional-NCAA-pool/stories/200603130129). Of course, you can also make this (mostly) risk free by using points to bid on teams instead of money... our office typically has the biggest loser by the winner lunch.

Here’s how it works:

Get everyone together over lunch for 1 1/2 to 2 hours on Monday to bid on the teams that they want to represent them for the tournament.  Each person will start with 500 or so points (for example) to "purchase" teams at the auction.  Everyone will earn 1 point back for each point their team scores in the NCAA tournament, and the owner of the NCAA tournament championship team will earn 100 bonus points.  The person with the most points after the final will be the winner and gets all the glory. And possibly lunch... :)

I've tried to make this auction process a little easier using an R Shiny app that you can download using the following commands:
```
install.packages('devtools')
devtools::install_github('nielsenmarkus11/NCAAcalcutta')
```

Once you've installed the package you'll need to import the latest bracket data (which will be available this upcoming Sunday) and load this into R. Because that data isn't available yet, I've included example data from 2018.  You'll want to mimic the 2018 csv file to ensure that the app works properly. Once you are ready you can import the teams and start the Calcutta Shiny app.
```
# Input the 2018 teams
teams <- import_teams(system.file("extdata", "ncaa-teams.csv", package = "NCAAcalcutta"))
start_auction(teams, randomize=TRUE)
```
![Shiny App](/img/NCAAcalcutta-example.png)

There you go, you're all ready to get started!

Here are some general guidelines:

* When the timer runs out, the bidding is over
* Only allow bids in 5 point increments
* In the app, each team has a minimum bid,  this rule can be loosened at the end if nobody has points left to spend.

This is one additional rule I made up to make it fair if someone realized they spent too much after the fact:

* If you bid more than you have, you will have 10 points per overspent point deducted from your final score.

I hope you all have as much fun with this as our team does.  Comment below for any additional clarification. And happy bidding!

### FAQ
Q: How do I determine how many points each participant starts with?

A: Typically it works well to (1) take the total points scored in last years tournament, (2) multiply that by 0.8 and (3) divide by the number of participants. You can probably round up to the nearest 25 points and you should be okay.
