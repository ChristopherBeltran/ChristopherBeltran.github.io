---
layout: post
title:      "He who has many, but also belongs and has many through?"
date:       2018-12-20 01:02:08 -0500
permalink:  he_who_has_many_but_also_belongs_and_has_many_through
---


Project time once again but this time around I've been beaming with much more confidence than when entering the depths of the CLI.  Sinatra and ActiveRecord have both become great comrades of mine after going through the SQL bully at the gates.  I knew right away from reading the project spec exactly what I wanted to create and how I would want all these to play together.  Being a lover of music and having frequented far too many shows to remember, I sought out to solve that problem exactly by creating a log of all my concerts I've attended.  Enter the Concert Scrapbook.

The trickiest part about the scrapbook was trying to map out the relationships in my models in accordance with what I wanted to actually allow the user to do.  I knew that I wanted the user to be able to have a basic view of all of the concerts that they've logged, but I also wanted to allow them to dive a little bit deeper and have unique views for each artist they've ever seen and for each venue that they've ever visited.  

In the beginning, I thought I had the relationships down pat.  I would need a User, Concert, Artist and Venue model but also a Concert Artist and Concert Venue along with corresponding join tables.  That resulted in this beautiful mess:
![](https://i.imgur.com/yLedGT9.png)

I went ahead and created all my table migrations for all 6 of these tables.  Once I dove into Tux I realized that I had absolutely overthought the implementation.  I scrapped the repository and proceeded to scrap it twice more, before finally reaching out for some guidance from DJ.  It wasn't until I actually wrote out the issues I was encountering with my relationships, for me to finally have the lightbulb moment.  I immediately went back and scrapped all of the join tables, and simply made the Concert class my class to hold the foreign keys for the artist and venue.  After some thorough testing in Tux, all the original models were now getting along great and the codebase became much more concise and easy to navigate.  

After finally setting up the foundational backend of the application I was ready to jump to the front end.  I had all of my views mapped out already in a whiteboard session, so I was very clear on all of the routes I was going to need.  Implementing the routes proved to be quite a challenging maze but also the most enjoyable.

Being in QA and testing for so long where my purpose was to find the bugs, it was an awesome feeling to be finding AND fixing my own bugs.  I stress tested every single one of my forms to death, while also performing tons of tests for an account holder vs. a non-account holder and came across tons of bugs along the way that I was able to debug and fix myself.

It was a truly rewarding experience to finally record my walkthrough video and watch my app hum along smooth and bug-free.  
