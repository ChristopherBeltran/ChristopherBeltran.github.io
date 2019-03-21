---
layout: post
title:      "ActiveRecord - Building Associations"
date:       2019-03-21 20:03:20 +0000
permalink:  activerecord_-_building_associations
---


One of the great methods that you can utilize with ActiveRecord is the `build` method.  What the `build` method does is automatically associate the two objects that you are calling it on.  Consider the following:

```
class User
has_many :posts


///

class Post
belongs_to :user
```

With these relationships set up we can then set up a method like this:

```
[user_instance].posts.build
```

This will create a new instance of the `Post` class and automatically associate it with our given user instance that we called the method on.

```
Post id: nil, user_id: 1
```

Once the instance is saved we will have created a brand new association between the two classes.  

Another step further would be to just call the `create` method.

```
[user_instance].posts.create(title: "New Post", content: "Yadayadayada")
```

With `create` we'd have to supply the attributes for the second class being called on, in our case the Post class.  If it is provided with those required attributes, it will trigger the SQL automatically and commit the new instance to the database.

```
Post id: 1, user_id: 1, title: "New Post", content: "Yadayadayada"
```


In order to call these types of methods, the initial class (User) must be the class that `has_many` of the second class being called (Post).  
