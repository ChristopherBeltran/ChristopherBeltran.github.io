---
layout: post
title:      "Class It Up"
date:       2018-07-17 20:46:05 -0400
permalink:  class_it_up
---


The way I view Classes, is as a set of blueprints that will allow us to plug and play in the future.  A class can also be viewed as a factory, that consists of an assembly line, all working together to churn out a product.  In the world of Ruby, the assembly line processes are referred to as methods, while the product being churned out is our object.

Each object is manufactured through these methods, with attributes and behaviors added to it along the way.  I'm going to give a high level overview of what the process would look like to add an expansion team to Major League Baseball, by plugging into a class.

* I'll start off by creating the class **Team**

```
class Team
end 
``` 

* Next, I want to think about the necessary properties that I want a team to be equipped with upon creation... We want to know the team name and the town they play in.  They're going to need some players though...So we'll have to equip it with a roster as well...

We can start by utilizing a Constructor method, which will apply all of these properties to our new team upon creation.

```
def initialize(team_name, hometown)
@team_name = team_name
@hometown = hometown
@roster = {}
end
```

So we allowed two arguments to be passed in when utilizing the method, for **team_name** & **hometown**, this will look something like this when called upon: `cyclists = Team.new("Cyclists", "Portland")`.  And with that, we now have a new team created called the Portland Cyclists, with a new roster hash that is waiting to be filled with players.  Taking a look inside the Constructor method, we applied instance variables with the @ symbol, to be assigned to the arguments that were passed in.  By assigning these instance variables, we now have the ability to access them outside of the Constructor method.

But since teams occassionally do relocate, we'll want to be able to modify the **team_name** & **hometown** instance variables later.  So what we can do is implement a  setter and getter method.

```
def team_name=(team_name)
@team_name = team_name
end 

def team_name
@team_name
end

def hometown=(hometown)
@hometown = hometown
end

def hometown
@hometown
end

```

That's a lot of extra code that we can actually trim down by utilizing a macro.  

```
attr_accessor :team_name, :hometown
```

Implementing the **attr_accessor** macro with the instance variables, takes the place of both the setter and getter methods we had previously wrote.  Each of the methods can also be individually set with the **attr_writer** & **attr_reader** methods.  These can be set individually if you had further specific behaviors you wanted to implement to your setter or getter methods.


* Now we'll try and fill our new team with some players.  Again we must think of the properties we'd like to apply to these guys.  We'll go with the basics, Name and Position. Before writing the add_player method we'll need to add **:name, :position** to our attribute accessor in order to operate on them within the method. 

```
def add_player(name, position)
if roster.include?(position)
    roster[position] << name
    else 
    roster[position] = []
    roster[position] << name
    end 
    end 
end 
```

The first step in the method is to implement a check via an If statement, to verify if there is already an existing key value pair for the player's position and name.  If there is an existing key, we choose to utilize the push method via **<<** and add the value of the players name, to the key being the position.  So when we want to add more players of the same position, they will be added through this step.  Otherwise, for new position, the If statement will evaluate to false, and then proceed to the Else statement, in which we create a new Key for the players position, and then add their name value to that key.

At this point we can being operating on the Class through the CLI using dot notation.

```
cyclists = Team.new("Cyclists", "Portland")
```

Should return something like this:

```
#<Team:0x00005606dca10610 @team_name="Cyclists", @hometown="Portland", @roster={}>
```

So our new team the Portland Cyclists has now been created and employs an empty roster that we can begin adding to.

```
cyclists.add_player("Art Vandelay","Pitcher")
cyclists.add_player("Jules Winfield","First Base")
cyclists.add_player("Benny Rodriguez","Pitcher")
```

Now when we call upon the teams roster, the hash should begin to take shape:

```
cyclists.roster

{"Pitcher"=>["Art Vandelay", "Benny Rodriguez"], "First Base"=>["Jules Winfield"]}
```



This is pretty much as far as I've gotten in the Object Orientation module and wanted to flesh all of this out in words as I try to master the concepts leading up the final Ruby projects this month. Farewell and happy coding.

