---
layout: post
title:      "CLI Project"
date:       2020-08-25 20:51:17 +0000
permalink:  cli_project
---


For this project I decided to go with the Spotify Search API. I definitely underestimated how hard it would be to use this API. For this API you have to have the user sign in to spotify then you get a link back that you can use to get an Access token and Refresh token. These are needed to use their APIs(they have about 5 different ones). There are four different ways to get an access token and they all require different things with some you don't get a refresh token but with others you do. I chose to go with the first one which is the [Authorization Code Flow](https://developer.spotify.com/documentation/general/guides/authorization-guide/#authorization-code-flow) in my application I asked the user to sign in, after they put in there username and password it asks them if it theres first time using the app. If it is their first time then they get authorized and then we get back a code. If it is not their first time we don't need to get the user authorized we just get the code back. I really struggled at this part because I had no idea how I would be able to get a user authorized through command line. I decided to do a little research and found out I needed a redirect url in order to have the user sign in through there but the problem is my app isn't online. So I decided to have a local server as my redirect url and I found out how to make one with a simple python command `python3 -m http.server`. Now I have a redirect url but no way for the user to sign in still. I got the idea to use a headless browser but I wasn't sure if it would work with ruby. After some research it turns out there's already a gem called [`Ferrum`](https://github.com/rubycdp/ferrum) that can control a headless browser. Now that I have the local server and a headless browser I was able to take the user's username and password and had ferrum enter the username and password and get the code back. 

From there I had to get the Access token and Refresh token, in the API docs it said I had to post the code using `application/x-www-form-urlencoded` encode which I had no idea what that meant. So I decided to try the other three methods to get an Access token. They all came to a dead end, I had gone through a whole day without getting nowhere. I was ready to switch to another API but I decided to give the first method one more try, did some research and found out how to post the code to the Spotify API. 

      ```request_token = HTTParty.post("https://accounts.spotify.com/api/token", {
                            body: "grant_type=authorization_code&#{code}&redirect_uri=http://localhost:8000=",
														headers: {
														       
                            }})```
										
I also had to encode the Client ID and Client Secret with a base64 encode and that is already built into ruby so I just had to `require "base64"`. As you can see in the code above there is a body and a header, the body contains the query parameters that it required and the header `"Content-Type"` specifies that it should be in a url form when it is posted. The `"Authorization"` was also required for this method of getting an Access token. 

Now we have an Access token! At this point I was very excited that I was able to figure it out and glad I didn't give up but this was still not even the start of the actual project. The rest of the projects was way smoother, although I did have a few bugs here and there I asked for help and fixed them. This project was really fun to me even though I struggled at first I am glad I didn't give up. 

If you would like to use it on your own computer you can find it here: https://github.com/DavidFuents/CLI-Application
