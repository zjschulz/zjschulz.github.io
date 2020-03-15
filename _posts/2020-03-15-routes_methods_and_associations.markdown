---
layout: post
title:      "Routes, Methods, and Associations"
date:       2020-03-15 23:12:57 +0000
permalink:  routes_methods_and_associations
---


Throughout this project, I encountered many scenarios where I needed to confirm the path my routes would take or needed to figure out where I needed my CRUD action methods to redirect or render to. Using the "rails routes" command in my terminal, I was able to do the above easily since I understood the syntax of the routes, the methods they provide, and their association with models (which should have their own associations with other models).

The below is a portion of what generally shows up when "rails routes" command is used in the terminal. The "Prefix Verb" gives us a method, such as "dogs" and it's GET or POST. "URI Pattern" is where we see what the route look like in the url. For example, the new dog action shows up as "localhost/3000/dogs/new". The "Controller Action" shows us which CRUD action method or scope method is being called on in that route.

How do we interpret this? The "Prefix Verb" allows us to use path methods for redirection. For instance, the dogs_path method will redirect us to the dogs' index view. The new_dog_path brings us to the dogs' new view. In my project, I had it coded so that my walks routes were nested within my volunteers routes. Therefore, I could call upon the walks path within my volunteers path. So, in my project, after creating a volunteer, I could redirect a user to create a walk for that specific volunteer using the new_volunteer_walk_path method.

We are able to do the last example do to the "has_many", "has_many_through", and "belongs_to" associations within my models. A volunteer has many walks and a walk belongs to a volunteer. These activerecord methods, once placed in a model, provides us with various methods linking these two models. It also allows us to, like I presented in the previous paragraph, call upon each others routes.

                               Prefix Verb   URI Pattern                                                                              Controller#Action
                                 dogs GET    /dogs(.:format)                                                                          dogs#index
                                      POST   /dogs(.:format)                                                                          dogs#create
                              new_dog GET    /dogs/new(.:format)                                                                      dogs#new
                      volunteer_walks GET    /volunteers/:volunteer_id/walks(.:format)                                                walks#index
                   new_volunteer_walk GET    /volunteers/:volunteer_id/walks/new(.:format)                                            walks#new
                           volunteers GET    /volunteers(.:format)                                                                    volunteers#index
                                      POST   /volunteers(.:format)                                                                    volunteers#create
                        new_volunteer GET    /volunteers/new(.:format)                                                                volunteers#new
                                walks POST   /walks(.:format)                                                                         walks#create
 
