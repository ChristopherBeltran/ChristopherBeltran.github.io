---
layout: post
title:      "From fantasy to real life CLI"
date:       2018-09-30 02:15:17 -0400
permalink:  from_fantasy_to_real_life_cli
---

The time has come and I have finally hit my last Github commit (for now) on my CLI Portfolio Project.  After this project has been looming over me for about two months now, it’s quite a surreal feeling to hit that submit button.  The project has come a long way since it’s inception.  A seemingly simple idea for an application that consisted of 3 screens, evolved into an out of control beast, teetered on the brink of destruction, then finally settled still at the concise build I have today.

Before getting started, as I wrapped up the last sections of the OO module and worked through the Music Library CLI and Student Scraper labs, the fear and uncertainty had intensified quite a bit.  Spending the last 2 months working through labs in which there were clear-cut instructions for most of the methods that needed to be implemented, along with desired results, had me stuck in an “imposter syndrome” mindset as I looked over the CLI project requirements.  Being simply provided the destination, rather than the routes to get there, seemed like quite a daunting task.  

I took a day or two to decompress and to brainstorm some ideas on what exactly I wanted to build.  Before I even started the program I had been bursting with ideas for a number of apps I wanted to attempt to build and experiment with.  I flushed everything out and tried to determine a user flow for each, and what would actually be attainable at this point in my engineering career, with regards to the project requirements as well.  I narrowed down to sites from two areas that I’m passionate about, sports and art.  With one ambitious idea that I wasn’t 100% sure would work...while also having one safe fallback idea which would absolutely fulfill the project requirements.  The latter was set to be a interface that provided the user with a list of art galleries within a given location provided by the user.  I had scoped out the layout of the site and found that the necessary elements to scrape were all conveniently formatted in one class or div.  I saw through that project lifecycle immediately and how it would play out.  Then I moved on to my first idea, which was to scrape a fantasy football statistical site.  Which was everything the art source was not… Deeply nested divs and tables while the required data was located on multiple pages.

 I decided to pursue the football project.  What won me over, was the idea of the challenge and really finding out if I’m cut out for this, while also seeing the ways in which the application can be expanded in the future.  Before I started wireframing and setting up project requirements I took a few days to read over gem documentation, review other projects and watch some of the recorded study groups.  The study groups were an awesome resource and truly got me comfortable enough to take the first step out the door.  

When I began the initial project framework,  I intended to scrape fantasy football projections for each position of QB, RB, WR, and TE.  Then to compile the players to be displayed in two different views, an overall view with all players combined and sorted by their respective weekly projected points, and then the second view, which would be by each position.  The user would be given the option at the main menu to choose which view they wanted to see.  


However, once I dove in and scraped all the data for each position I ran into issues with sorting the data through player objects.  I had a ton of scraper methods as it was since the page had to pull from different URLs for each position.  I toyed with the idea of just making it a Player class in general, that encompassed Player initialization as well as scraping methods.  I started by pulling all of the data and forming into hashes, as I saw similarities in what I hoped to accomplish in my project with the Student Scraper lab I had just completed.  

I compiled the data with the following code, in which I scraped all the player names and stats into a hash nested in the `@@all` array

```
class Scraper

@@all =[]

  
  
  def self.qb_scraper
    @qb_doc = Nokogiri::HTML(open("https://www.fantasypros.com/nfl/projections/qb.php"))
    player_label = @qb_doc.css(".player-label")
    player_label.css(".player-name").take(20).each do |player_name|
      player = Player.new
      player.name = player_name.text
    end
  end
    end

  def self.qb_points_scraper
  points_columns = [14,25,36,47,58,69,80,91,102,113,124,135,146,157,168,179,190,201,212,223]
    @@all.zip(points_columns).each do |player, proj|
      player[:projection] = @qb_doc.css("td")[proj].text
    end 
  end

  def self.rb_scraper
  @rb_doc = Nokogiri::HTML(open("https://www.fantasypros.com/nfl/projections/rb.php"))
    player_label = @rb_doc.css(".player-label")
    player_label.css(".player-name").take(30).each do |player_name|
    @rb_hash = {
    :name => player_name.text
    }
    @@all << @rb_hash
    end
  end

  def self.rb_points_scraper
  points_columns = [12,21,30,39,48,57,66,75,84,93,102,111,120,129,138,147,156,165,174,183,192,201,210,219,228,237,246,255,264,273]
     @@all[20..49].zip(points_columns).each do |player, proj|
       player[:projection] = @rb_doc.css("td")[proj].text
       end 
  end
  
  def self.wr_scraper
  @wr_doc = Nokogiri::HTML(open("https://www.fantasypros.com/nfl/projections/wr.php"))
    player_label = @wr_doc.css(".player-label")
    player_label.css(".player-name").take(30).each do |player_name|
    @wr_hash = {
    :name => player_name.text
    }
    @@all << @wr_hash
    end
  end

  def self.wr_points_scraper
  points_columns = [12,21,30,39,48,57,66,75,84,93,102,111,120,129,138,147,156,165,174,183,192,201,210,219,228,237,246,255,264,273]
     @@all[50..79].zip(points_columns).each do |player, proj|
       player[:projection] = @wr_doc.css("td")[proj].text
       end 
  end
  
  def self.te_scraper
  @te_doc = Nokogiri::HTML(open("https://www.fantasypros.com/nfl/projections/te.php"))
    player_label = @te_doc.css(".player-label")
    player_label.css(".player-name").take(15).each do |player_name|
    @te_hash = {
    :name => player_name.text
    }
    @@all << @te_hash
    end
  end

  def self.te_points_scraper
  points_columns = [8,14,20,26,32,38,44,50,56,62,68,74,80,86,92]
     @@all[80..94].zip(points_columns).each do |player, proj|
       player[:projection] = @te_doc.css("td")[proj].text
       end 
  end
  
  def self.profile_scraper(player)
    @doc = Nokogiri::HTML(open("https://www.fantasypros.com/nfl/players/#{player}.php"))
    @profile_hash = {}
    @profile_hash[:week] = @doc.css(".outlook").css("h4").text
    @profile_hash[:next_game] = @doc.css(".outlook").css(".next-game").text.strip.gsub("\n",'')
    @profile_hash[:news] = @doc.css(".content").css("p").first.text
    stat_names = []
    @doc.css(".all-stats").css("th").each do |stat|
      stat_names << stat.text
    @profile_hash[:stat_categories] = stat_names
    stat_contents = []
    @doc.css(".all-stats").css("td").each do |stat|
      stat_contents << stat.text
    @profile_hash[:stat_totals] = stat_contents
      end 
    end
    @profile_hash
  end 

```


I found myself getting lost in a forest of hashes.  With no clear way on how I was going to set all this data into object form. This was the darkest point of the project as I was unsure how to proceed, or if I would even be able to at all.  Ringing in my head, was Etan warning me about the most common mistakes that he had heard of students making during this project, in which they get so caught up in trying to make the most amazing app imaginable.  

After browsing through the Learn Magazine and tracking down a few students' Github repos, as well as the WorldsBestRestaurants repo, it finally hit me how I could salvage the project.

Rather than piling information into hashes and then sorting it later, I decided to eliminate the hash concept and instead initialize the data as objects upon their initial scraping.  I did not see an easy way to break up every player from all these different positional URLs into their own object, so I decided to scrap the remaining positions and only focus on one position, the quarterback.  It was the only way I saw myself being able to fulfill all the project requirements and deliver a functioning application, with the idea of being able to potentially implement the remaining positions further down the road.  

My CLI now would consist of two screens, one that automatically displays the list of scraped quarterbacks along with their projections, and now presenting the user with the option to select a player to proceed to the next screen and view a detailed player specific page.  This next flow would be the player profile screen that allows the user to view that selected players detailed stats, schedule and news.  

The amount of relief I felt as I finally ran the program and navigated through with no bugs, was incredible.  Being able to reflect on it now, I absolutely loved the journey and truly getting a taste of the highs and lows of programming.  I've always been an advocate of finding solace in the tiny victories, and this experience truly put those philosophies to the test, along with my coding knowledge/skillset as well as my overall problem solving ability.  I'm excited to see how much further I can push this application, as well as what the next four projects will bring out of me.  Until then, so long and thanks for all the fish! 



