---
layout: post
title:      "From fantasy to real life CLI"
date:       2018-09-30 06:15:17 +0000
permalink:  from_fantasy_to_real_life_cli
---

The time has come and I have finally hit my last github commit (for now) on my CLI Portfolio Project.  This has taken much longer than I had anticipated, about a month or so, due to life happening.  After finally being able to commit solid weekend time to the project I have powered through to completion.

My original idea was to scrape fantasy football projections for each position of QB, RB, WR and TE.  Then to compile the players to be displayed in two different views, an overall view with all players combined and sorted by their respective weekly projected points, and then a second view by position.  The user would be given the option at the main menu to choose which view they wanted to see.  

However, once I went in and scraped all the data for each position I ran into issues in sorting the data through player objects.  I had a ton of scraper methods as it was,  since the page had to pull from different URLs for each position, and I did not want to make a separate class for each position.

I condensed the app into only displaying the QB position.  All scraper methods were pulling from the one URL of the qb page and then creating player objects off of the scraping.  

My CLI now would consist of two screens, one that automatically displays the list of players along with their projections, and now presenting the user with the option to select a player to proceed to the next screen.

The next screen would be the player profile screen that allows the user to view that selected players detailed stats, schedule and news.

Prior to making the decision to condense the project, I had toyed with the idea of scrapping and falling back to another page I had in mind that was much more easily formatted.

But I decided to carry on and had a ton of fun utilizing the various scraping methods that were not just simple, cut and dry.  

Prior to getting started, the idea of constructing my very own project from a blank IDE was absolutely terrifying and crippling.  But now after a successful creation, the excitment I feel now is amazing, and I can't wait to keep on iterating on this project in the future, as well as take on my remaining projects.
