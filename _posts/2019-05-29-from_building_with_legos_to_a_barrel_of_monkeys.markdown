---
layout: post
title:      "From building with Legos to...a barrel of monkeys"
date:       2019-05-29 01:32:07 -0400
permalink:  from_building_with_legos_to_a_barrel_of_monkeys
---


This is exactly what programming felt like after taking the leap from writing code in Ruby for 8 months, to now having to code in Javascript.  This was still my feeling despite the fact that the first language I ever started learning in was Javascript almost two years ago.  But after spending real structured learning time with Ruby for so long, it made me fall in love.

The first stark difference that you see between the two is the overall readability.  Now, a lot of this has to do with the fact that Javascript must interface with more external sources such as formulating API calls, and inserting and modifying HTML elements.  

The other big difference for me was modularity.  A typical Ruby application is sectioned off very nicely when following the MVC design framework.

* The Model folder houses a variety of files, with each file being a "Class".  The way classes are structured is another great beauty of Ruby:


 
```
  class User < ActiveRecord::Base
  include Titleize
  include Displayname
  has_secure_password
  has_many :adoptions
  has_many :pets, through: :adoptions
  #validates :phone_number, length: { is: 10 }
  validates_format_of :phone_number, with: /\A(\d{10}|\(?\d{3}\)?[-. ]\d{3}[-.]\d{4})\z/, unless: -> { from_omniauth? }
  validates :name, presence: true
  validates :email, presence: true
  validates :email, uniqueness: true
  before_save :tileize_name
  before_create :tileize_name
```
	
	
	
*All of the class properties are clearly displayed atop the file along with any relationships that it may have to other classes and any validations that will take place before an instance of the class is allowed to be persisted to the database.*


* The Views folder contains all of the user facing views that they will encounter throughout the application, in the form of HTML files.  Where Ruby thrives in this aspect, is all thanks to Rails.  The Rails framework contains an incredible library of "helpers" that require the developer to simply write shorthand code in the view file only to have it generate full lines of HTML in the web client.  


```
<%= form_for @pet, :url => admin_pet_create_path do |f| %>
<%= f.label :name %>
<%= f.text_field :name %>
<br>
<%= f.label :age %>
<%= f.number_field :age %>
<br>
<%= collection_check_boxes :pet, :breed_ids, Breed.all, :id, :name do |b| %>
   <div> <%= b.check_box %><%= b.label { b.text } %></div>
    <% end %>
<br>
<%= f.fields_for :breed_attributes, @pet.breeds.build do |breeds_fields| %>
<br>
<%= f.label "New breed?" %>
<%= breeds_fields.text_field :name %>
<br>
<%= f.submit "Add Pet", id: "new_pet_button" %>
```


*The code above with Rails helpers will generate this HTML below in the browser:*


``` 
<form class="new_pet" id="new_pet" action="/admin/pets" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="✓"><input type="hidden" name="authenticity_token" value="VGNhaIcPH4DafxfJ3HbKnY3xeMa+JXspk3prP/00bf97KS6UU2nIhP6cUnLnjLK27FOhX5LM/1euBOxys2RoAg==">
<label for="pet_name">Name</label>
<input type="text" name="pet[name]" id="pet_name">
<br>
<label for="pet_age">Age</label>
<input type="number" name="pet[age]" id="pet_age">
<br>
<input type="hidden" name="pet[breed_ids][]" value="">
<div> <input type="checkbox" value="1" name="pet[breed_ids][]" id="pet_breed_ids_1"><label for="pet_breed_ids_1">German Shepard</label></div>
```

    <div> <input type="checkbox" value="2" name="pet[breed_ids][]" id="pet_breed_ids_2"><label for="pet_breed_ids_2">Labrador</label></div>

    <div> <input type="checkbox" value="3" name="pet[breed_ids][]" id="pet_breed_ids_3"><label for="pet_breed_ids_3">Shiba Inu</label></div>

    <div> <input type="checkbox" value="4" name="pet[breed_ids][]" id="pet_breed_ids_4"><label for="pet_breed_ids_4">Akita</label></div>

    <div> <input type="checkbox" value="5" name="pet[breed_ids][]" id="pet_breed_ids_5"><label for="pet_breed_ids_5">Beagle</label></div>

    <div> <input type="checkbox" value="6" name="pet[breed_ids][]" id="pet_breed_ids_6"><label for="pet_breed_ids_6">Miniature Pinscher</label></div>

    <div> <input type="checkbox" value="7" name="pet[breed_ids][]" id="pet_breed_ids_7"><label for="pet_breed_ids_7">Huskie</label></div>

    <div> <input type="checkbox" value="8" name="pet[breed_ids][]" id="pet_breed_ids_8"><label for="pet_breed_ids_8">Chihuaha</label></div>

    <div> <input type="checkbox" value="9" name="pet[breed_ids][]" id="pet_breed_ids_9"><label for="pet_breed_ids_9">Terrier</label></div>

    <div> <input type="checkbox" value="10" name="pet[breed_ids][]" id="pet_breed_ids_10"><label for="pet_breed_ids_10">Shi Tzu</label></div>

    <div> <input type="checkbox" value="11" name="pet[breed_ids][]" id="pet_breed_ids_11"><label for="pet_breed_ids_11">French Bulldog</label></div>

    <div> <input type="checkbox" value="12" name="pet[breed_ids][]" id="pet_breed_ids_12"><label for="pet_breed_ids_12">Greyhound</label></div>

    <div> <input type="checkbox" value="13" name="pet[breed_ids][]" id="pet_breed_ids_13"><label for="pet_breed_ids_13">Poodle</label></div>

    <div> <input type="checkbox" value="14" name="pet[breed_ids][]" id="pet_breed_ids_14"><label for="pet_breed_ids_14">Mastiff</label></div>

    <div> <input type="checkbox" value="15" name="pet[breed_ids][]" id="pet_breed_ids_15"><label for="pet_breed_ids_15">Weiner</label></div>

    <div> <input type="checkbox" value="16" name="pet[breed_ids][]" id="pet_breed_ids_16"><label for="pet_breed_ids_16">Schnauzer</label></div>
    <br>
    <br>
    <label for="pet_New breed">New breed?</label>
    <input type="text" name="pet[breed_attributes][name]" id="pet_breed_attributes_name">
    <br>
    <input type="submit" name="commit" value="Add Pet" id="new_pet_button" data-disable-with="Add Pet">
    </form>
`

*The helpers automatically make all of the associations between the classes and format into HTML.  Magic!
*

* Lastly, the Controller which handles all of the routing of the Web App and is responsible for communicating data between Models and Views.


With all this ease and beauty provided by one language, how can one possibly leave?!

Thankfully, the first project after moving on from Ruby is a refactor of the Rails project by adding Javascript functionality.  This was an absolute blessing considering that it eased one of my biggest fears from moving on to a new language, of becoming rusty in Ruby.  

The bulk of this project is absolutely spent writing Javascript (I have 312 lines of Javascript code to prove it!), but there is still a good amount of work that goes into getting the Ruby on Rails backend portion set up.

Before I even wrote one line of new code for this project, I addressed a problem that had plagued each and every one of my last projects: **Scope Creep**.  

To avoid this, I decided to approach the project the same way I approach projects at work, by divvying up every chunk of development into granular tasks and aligning each of those tasks with a particular project requirement.  The result was me constructing my very own Kanban board:

<a href="https://ibb.co/HqWsJrP"><img src="https://i.ibb.co/Pg7nS5W/Screen-Shot-2019-05-15-at-4-36-57-PM.png" alt="Screen-Shot-2019-05-15-at-4-36-57-PM" border="0"></a>

I broke down which tasks fell under Javascript Development and which fell under Ruby development, while then proceeding to align each task with the appropriate project requirement.  

On the Ruby front, I started by coding out Serializer classes for my User, Pet, Breed and Adoption models.  Each Serializer class contained the Models given `has_many` or `belongs_to` associations as well as the attributes I needed to Serialize for the JSON response.

The last Ruby aspect I needed to implement was to configure the appropriate Controller actions as API endpoints.  I set up a total of 10 API endpoints consisting of Index, Create and Show actions.  

`Admin::BreedsController`
* Endpoints for the **Index** and **Show** actions, to display a full Index of all breeds and to display a particular individual breed on the **GET** request from the Javascript function.

`Admin::PetsController`
* Endpoints for the**Index**, **Create** and **Show** actions, to display a full Index of all pets and to display a particular individual pet on the GET request from the Javascript function, as well as to be able to receive a **POST** API call and create a new instance of the Pet class that will in turn send a response to the client that includes all of the data of the newly created instance.

`AdoptionsController`
* Endpoint for the **Create** action, receive a **POST** API call and create a new instance of the Adoption class that will in turn send a response to the client that includes all of the data of the newly created instance.

`PetsController`
* Endpoint for the **Index**, **Mypets**, and **Show** actions, to display a full Index of all pets, display an index of a users pets and to display a particular individual pet on the GET request from the Javascript function.


Moving on to Javascript, my first order of business was to implement Javascript's version of classes.  I decided that I needed a class for the Adoption, Breed and Pet models.  

Utilizing the new ES6 syntax I constructed them as follows:

```
class Adoption {
    constructor(obj) {
        this.id = obj.id;
        this.adoption_date = obj.adoption_date;
        this.user_id = obj.user_id;
        this.pet_id = obj.pet_id;
    };
};

class Breed {
    constructor(obj) {
        this.id = obj.id;
        this.name = obj.name;
        this.pets = obj.pets;
      };
		}
		
		class Pet {
    constructor(obj) {
        this.id = obj.id;
        this.name = obj.name;
        this.age = obj.age;
        this.breeds = obj.breeds;
        this.users = obj.users;
        this.adoptions = obj.adoptions;
    };
		}
```

The new Class and Constructor syntax with ES6 just might be my favorite thing about Javascript in that it's so similar to the `Initialize` method in Ruby classes.


After setting up the classes, I began to implement the functions that would house the API calls to the Rails endpoints.  

I added 7 such functions, each for a particular view in the app:

`adminPetsIndex()`
*To be called on Ready on the admin/pets index page to receive the API response and then render the list of all Pets in the database*

`addNewPet()`
*To be called on submit on the admin/pets/new page to send a POST call and receive the API response and render the newly created Pet by utilizing the `event.preventDefault()` function to stop Submit from the Rails form.*

`adminBreedsIndex()`
*To be called on Ready on the admin/breeds page to receive the API response and then render the list of all Breeds in the database*

`adminBreedsShow(val)`
*To be called from an onClick event attached to each instance of a Breed displayed on the Breed Index page.  This function then takes the value of a breeds ID as an argument and passes that value into the API call and after receiving the API response, saves the data into local storage to be retrieved on the subsequent page load. *

`petsIndex()`
*To be called on Ready on the /pets page API response and then render the list of all Pets in the database that are not owned by a user*

`myPetsIndex()`
*To be called on Ready on the users/:id/pets page.  The function fetches the user_id from a dataset and passes it into the API call to receive all of the pets owned by that user*

`newAdoption()`
*To be called on Submit, utilizing the `event.preventDefault()` function to stop Submit from the Rails form and instead sent a POST call and receive the API response to render the newly created Adoption.  This function also includes a second API call to `$.getJSON(/pets/${petId}.json)` which makes a call to the endpoint in order to allow a new Javascript instance of the Pet class to be created and be able to render that Pets vital information on the page.*


All of these functions were dependent heavily on the Class Prototype functions that I set up.  

The Pet class housed the majority of these functions:
```
ownedStatus() {
        if (this.users.length > 0){
            return "Y"
            } else {
                return `N - <a href='/admin/pets/${this.id}/edit'>Edit Pet</a>`;
            };
    };

    breedFormatter() {
        if (this.breeds.length > 1) {
            let br = []
            for(var i = 0; i < this.breeds.length; i++){
                br.push(this.breeds[i].name);
            };
            return br.join(", ");
            } else {
                return this.breeds[0].name;
            };
    };

    prototypePostHTML() {
        var pBreeds = this.breedFormatter();
        var ownedStatus = this.ownedStatus();
        return (`
            <tr>
                <td>${this.name}</td>
                <td>${this.age}</td>
                <td>${pBreeds}</td>
                <td>${ownedStatus}</td>
            </tr>
        `);
    };

    nonAdminPetIndexHTML() {
            var pBreeds = this.breedFormatter();
            return (`
            <tr>
                <td>${this.name}</td>
                <td>${this.age}</td>
                <td>${pBreeds}</td>
                <td><a href='/pets/${this.id}/adoptions/new'>Adopt?</a></td>
            </tr>
        `);

    };

    myPetsIndexHTML() {
    var pBreeds = this.breedFormatter();
    return (`
    <tr>
        <td>${this.name}</td>
        <td>${this.age}</td>
        <td>${pBreeds}</td>
        <td>${this.adoptions[0].adoption_date}</td>
    </tr>
    `);
    }```
		```
Since the Pet class is effectively used in 3 separate aspects, it required different functions to display the instances across the pages, as the available pet options and pet information varied for each view.



And that's that.  

I started off this project deeply intimidated by the thought of having to write this much Javascript and essentially being back in the novice stage of a language after becoming so fluent in Ruby, but once I was able to conceptually get over the differences between the two, I found myself in a much better place.  I learned to appreciate the fluidness of Javascript engineering, in particular, hoisting, callback methods and manipulating JSON responses.  I also picked up a few new things along the way such as saving to and retrieving from local storage.  As with all of my projects at Flatiron, truly rewarding to finally hit that last commit and be able to navigate bug-free through a complex application of your own creation.
		



