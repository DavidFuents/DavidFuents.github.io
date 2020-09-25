---
layout: post
title:      "Sinatra Project"
date:       2020-09-25 16:15:23 -0400
permalink:  sinatra_project
---


For this project I made an application where you could make a planner/schedule.  I struggled a few times while making this. I made it so that the user creates a table first then it takes then to the editing page where they can add rows and that is when I had I trouble. In the Planners table schema I have a row and I wanted that to be an empty array and have other arrays nested inside and every one of those arrays would be a row. 

``` [[This would be row 1], [This would be row 2]] ```

So I created the object and the row did have an empty array as its value but everytime I tried to nest an array it would just make it equal to that one array. 

```<Planner:0x00007fda706aa610 id: 2, title: "test", heading: ["test", " test"], row: [], user_id: "1", created_at: 2020-09-25 20:08:52 UTC, updated_at: 2020-09-25 20:08:52 UTC>```

That would turn into:

```<Planner:0x00007fda706aa610 id: 2, title: "test", heading: ["test", " test"], row: ["heading"], user_id: "1", created_at: 2020-09-25 20:08:52 UTC, updated_at: 2020-09-25 20:08:52 UTC>```

But it should look like this:

```<Planner:0x00007fda706aa610 id: 2, title: "test", heading: ["test", " test"], row: [["heading"]], user_id: "1", created_at: 2020-09-25 20:08:52 UTC, updated_at: 2020-09-25 20:08:52 UTC>```

This is what I ended up doing:

```
@row = []

      params[:planner][:row].each do |item|
        @row << item.strip
      end

      params[:planner][:row].clear

      @table[:row].each do |row|
        params[:planner][:row] << row
      end

      params[:planner][:row] << @row
      @table.update(params[:planner])
```

I have a row instance variable equal to an empty array and then an iteration that grabs the params which looks like this: 

``` {"planner"=>{"row"=>["Hello", "Hello"]}, "id"=>"2"}```

So that iteration goes to the row key which has an array as its value then grabs each thing in it and adds it to our @row. Then we clear the value of row in the params. After that we want to grab whatever rows already exist inside our table object if any and add it into our params so that those load before our new row we made. Finally we add our @row array back into the params which now looks like:

```{"planner"=>{"row"=>[["Hello", "Hello"]]}, "id"=>"2"}``` 

We are adding it back to the params because params is a hash and when you use the #update method it only takes in a hash. So now when we update our Planner object it looks like this:

```#<Planner:0x00007fda706aa610 id: 2, title: "test", heading: ["test", " test"], row: [["Hello", "Hello"]], user_id: "1", created_at: 2020-09-25 20:08:52 UTC, updated_at: 2020-09-25 20:26:19 UTC>``` 

Which is what I wanted a nested array. So now when we want to display the planner we can just iterate through each heading and row. 

This project was really fun to make and there are a few things I want to add to it at a later time but for now I am happy with the way it came out. 

You can check it out here: https://sinatra-planners.herokuapp.com/
