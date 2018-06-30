---
layout: post
title:      "Trust The Process"
date:       2018-06-29 21:48:22 -0400
permalink:  trust_the_process
---


I'm coming up on my 1-month mark in the Web Development immersive, and already I've found myself all over the emotional spectrum.  After spending extensive time with Javascript prior to the program, I've been able to absorb a lot of the Ruby concepts in stride.  However, there have been two occasions thus far in which I've found myself in terminal purgatory.

Loop iteration being my first downfall, I ended up spending majority of my Saturday trying to figure out how to loop over and declare the winning combination in the tic-tac-toe game.  Each method I attempted was failing on me, and not extracting all 3 placements of the winning combination.  Let the facedesking begin.

I won’t dare paste the initial code that I started out with, because I just can’t bring myself to lay eyes on it again...but this is the loop I finally ended up with.

```
WIN_COMBINATIONS.each do |combos|
  win_index_1 = combos[0]
  win_index_2 = combos[1]
  win_index_3 = combos[2]

  position_1 = board[win_index_1]
  position_2 = board[win_index_2]
  position_3 = board[win_index_3]

  if position_1 == "X" && position_2 == "X" && position_3 == "X" || position_1 == "O" && position_2 == "O" && position_3 == "O"
    return combos
```


Up until this point, I was only iterating over single arrays that consisted of a few elements.  But not until after I disgustingly hardcoded the combinations did I finally break through and find that I was able to extract each element individually through each array index, and in turn verifying those index placements on the board.  

At times like these, I become much too determined, to a fault.  In which I feel like I’ve come so far and put in so much effort on my own, that I have to just suck it up and make it work, as opposed to just asking for help. But now in retrospect, when I think about all the hours I lost spinning my wheels, plus the time I spent later to go back and refactor the code, it’s quite maddening.  This is going to be key for me to overcome as I try to stay the course with the schedule I’ve laid out for myself.  

Loops used to terrify me, and now I find myself fascinated by them and their efficiency.  Since starting the program, that has become a persistent thought of mine, is how can I be the most efficient?  With having to balance my time so carefully these days, it's forced me to take an analytical approach out of my codebase and start applying it to my day to day schedule.  

After not being in school for almost 10 years now, it's been a process to essentially learn how to learn again.  The pre-course work through Coursera and the Bootcamp prep, definitely help set me up with a framework of how I was going to go about scheduling my weeks, when my optimal working hours were, and when I need to take a step back to decompress.  

A few things I like to utilize when I reach a roadblock:

A) Change of scenery, be it simply moving to another couch or chair, or taking a stroll with my pup around the block, that can sometimes be enough to etch-a-sketch the mind and get you barreling ahead again.  During my time at WeWork Playa Vista, I found myself utilizing every floor of the facility, including the balcony. 

B) Old fashioned pen & paper.  It felt strange at first, to physically be writing out functions when the terminal was supposed to be my canvas, but the little nuances I found to be extremely helpful to me.  Be it from drawing arrows back and forth between a function and a method with notes to the side, or actually drawing out in wireframe fashion, how this concept was set to play out.  

C) Verbalize.  This is why I'm finding myself working at home more.  I'd rather not be the nut of the place out in public who's in the corner muttering jibberish at his computer, with an occasional cursing eruption.  But from numerous sources, I've learned that this is going to be essential to really have everything sink in.  My first screen share was absolutely terrifying.  Having someone in my coding sanctuary actually looking through my work and questioning why each line was the way it was.  After the screen share, and speaking with Etan, I've found myself speaking through all my lines of code, and explaining to myself what exactly is happening, beyond the syntax.  


I'm definitely not where I want to be yet as far as my learning process, but I have a ton of great influences guiding me in the right direction.  It helps quite a bit seeing the student community chiming in on the Slack channels about all their past challenges and throwing advice at noobs like me.  One of my biggest issues is trying to get into more of a tunnel vision mindset.  Which can be hard sometimes, when I'm seeing others finishing up their Sinatra or React projects, while also being exposed to tons of other frameworks during my natural web browsing.  It's a downfall of many developers that I've read continuously, and I'm training myself to just keep my eyes on my next step and stay the course.  
