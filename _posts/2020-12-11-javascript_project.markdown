---
layout: post
title:      "JavaScript Project"
date:       2020-12-11 00:19:49 -0500
permalink:  javascript_project
---


For this project we had to create a single page application. I decided to make another e-commerce site, I found this project really fun as I got to create a responsive frontend. One of the challenges I faced while making this project was the add to cart API. What I decided to go with in the end was a simple add to cart system. There are three models in the backend, One is the Product model, the second is a Cart model and the last is a Cart Item model. The Cart Item model was used as a join table. So whenever a user presses the add to cart button it sends a post request to the Cart Item controller. The request has the product id and the cart that we are trying to add it to. That is how to add a product to a cart. From there in order to display that product, we send a request to the Cart controller and grab all the Cart Items that belong to the user's cart. 
