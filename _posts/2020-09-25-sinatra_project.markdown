---
layout: post
title:      "Sinatra Project"
date:       2020-09-25 20:15:22 +0000
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

So this is what I ended up doing:

``` @row = []

      params[:planner][:row].each do |item|
        @row << item.strip
      end

      params[:planner][:row].clear

      @table[:row].each do |row|
        params[:planner][:row] << row
      end

      params[:planner][:row] << @row
      @table.update(params[:planner])```
