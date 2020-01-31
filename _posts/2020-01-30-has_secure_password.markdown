---
layout: post
title:      "has_secure_password"
date:       2020-01-31 02:08:48 +0000
permalink:  has_secure_password
---


The "has_secure_password" instance method adds methods to your class that are used to authenticate against a brypt password. It also adds two fields to our model, in which I call password_confirmation (used to authenticate your passwords) and password (password_confirmation's associated reader method). This makes it easier to create forms where you need to enter a password. This also adds validations to your class, which can be called upon via the built-in "athenticate" method. When the authenticate method is called upon, it check for validity by screening the password. It has the ability to screen for missing or inaccurate password or other sign in attribute such as an email or username field (all depending on what columns you've put in your db migration table used for Users.

We use the has_secure_password as to protect our passwords from encryption and theft. We do this by not storing the password, but by storing the password's hashes instead. A hash is a number computed by feeding a string to a hash function, per Learn.co. Using our has_secure_password method, we save these hashes in a password_digest column. Let me reiterate, we do not store the password itself. Also, bcrypt assist with protecting our password by salting and hashing our passwords. Salting is when we prepend a random string to the password hash. This makes life difficult for hackers who can run thousands of random passwords through your system to attempt to break in. Once a password is salted and hashed, has_secure_password lets you authenticate the user against that salted and hashed password.

To apply this to my application, I must first add the brypt gem to my Gemfile. Next, I'll add the "has_secure_password" method to my User model. Now, my migration for my user model has to be changes as I have "password" as one of my columns. This needs to change to "password_digest". Next, I will add the "authenticate" method to my login and sign up post/get methods in my controllers. Or I can add the authenticate method in one of my helper methods, which will in turn be added to my login and sign up post/get methods in my controllers.

