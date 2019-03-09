---
layout: post
title:      "Off The Rails"
date:       2019-03-09 06:07:05 +0000
permalink:  off_the_rails
---




It’s been a tumultuous road through the rails.  Each facet of the project posed a great challenge.  For the first time I found myself crippled at the projects inception.  The pondering phase took a lot longer than I had hoped as I had bounced back and forth from idea to idea, and even to the possibility of refactoring my Sinatra project with Rails.  I thought I had finally come to an agreement on a project idea involving Star Wars, in which I would create a platform for Jedi Knight’s to keep track of their training and apprentices.  

The application was set to involve two join tables: a Training table that would join the Jedi(User) and a Jedi_ForcePowers table which would join the Jedi and multiple Force Powers.  I progressed a great deal with the app - setting up the database, associations, whiteboarded, set up the routes and even set up all of the models and controllers.

I got to a point however, in which I realized that for my true vision of the app, it would not come to be while simply on Rails.  The ForcePower system  got a little too advanced, in which I was trying to utilize skill levels for each Jedi/Users force power, which would in turn provide any padawan receiving training from them, with a particular skill level boost in their force power area of expertise.  This was going to involve a lot of advanced algorithms and more site interactivity than Rails could provide. 

I decided to simplify.  The biggest issue in all of my portfolio projects has been trying to include too many other features outside of the scope of the requirements.  I was already 2 weeks in since completing the Amusement Park app and thought it was time to get moving on something I knew was 100% going to work.

Before each project I’ve had a clear vision of how it would end up.  Throughout the course of development they have not strayed that far.   So once I finally decided  to work on Pawsitive Outreach I knew what kind of journey it would be.

A platform that would be utilized by an Animal Shelter, which would allow users to browse and commit to adoptions of pets at the current shelter.  I decided to also allow a backdoor admin login flow in addition to the normal user flow.  The admin would be able to login with a set of given credentials and essentially maintain the inventory of pets by inputting them into the system.  

To satisfy the requirements of nested attributes I decided on a few methods:
- The first would be a nested pets/new route under the admin parent route.  Allowing the admin to create new pets. 
- The next would be a nested adoptions/new route under the pets/:id parent route. This would automatically render an adoption form that associated the given pet from the route as well as the current user. 

This project would also feature two join tables:
- A Pet_Breeds table which would associate a pet with a number of breeds.
- An Adoptions table which allowed for the many to many relationship between the User and Pet classes


I had two features that I was forced to trim, one was allowing there to be a “Foster” option that would allow a user to adopt a pet for a weekend or two.  The second would be the option to end adoptions and delete an association between the pet and the user.  Both of these led to tons of issues and even more that i foresaw in the future.  Given that I’d already invested twice the amount of time into the project than originally planned, It was best to proceed with my MVP that was fully functional. 

Despite a few setbacks, the whole process proved to be invaluable as it provided tons of new challenges I was forced to come face to face with and learn from.  I have quite a bit of confidence in my Ruby on Rails skills at this point and cant wait to refactor my favorite project, Concert Scrapbook with Rails and Javascript.  
