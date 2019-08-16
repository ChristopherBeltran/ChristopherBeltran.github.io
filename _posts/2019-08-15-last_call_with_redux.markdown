---
layout: post
title:      "Last Call With Redux"
date:       2019-08-16 00:08:25 +0000
permalink:  last_call_with_redux
---


For my final project with Flatiron, I was able to finally get to work on an app idea I've had for over a year now.  I chose to make a news app called Stash.  It essentially mirrors a recent product release called [Pocket](https://getpocket.com/), in that it is meant to be an all-in-one reading + sharing news app.  The user will be able to browser current news articles and save their favorites to their "Stash".  All news articles are pulled from [News API](https://newsapi.org/).

On the surface, the app can be broken down into two areas: The Stream and The Stash.

The Stream contains a list of articles that are pulled from the users selected news sources that get chosen upon account creation.  From the stream, the user will be able to save any article to their stash or to view the full article in a new browser tab.

The Stash contains a list of articles that the user has saved and also contains the ability to view the full article as well as to remove the article from their stash.

All 3rd party News API interaction is handled on the backend for security purposes.  This includes a rake task that runs once to get the sources set up in the DB, as well as a request to the News API that retrieves the articles to populate the users stream.

For styling I decided to go with [Material Kit React](https://demos.creative-tim.com/material-kit-react/#/).  

Even at the conclusion of the program, I found myself learning tons of new things throughout the project.

* Read the documentation!  I had a few mishaps with initially setting up my DB schema without first reading through the News API thoroughly to determine what attributes I would need to be supporting.
* How to set up and run rake tasks.
* Routing all external API requests through the backend API.
* When to utilize stateless components and when state is required.
* At what point in the React/Redux state flow to other async actions need to be dispatched to ensure the best user experience

This is just the MVP of this app.  New features and enhancements will be made including:
* Ability to add an article to the stash by simply pasting a URL
* Ability to share the list of articles from your stash to a friend via unique URL that is generated
* Ability to edit profile and add/remove news sources from stream

So check back in here [Stash App](https://github.com/ChristopherBeltran/stash-app-client)
