---
layout: post
title:      "User Interface With JavaScript/Rails Applications"
date:       2020-05-11 22:00:23 +0000
permalink:  user_interface_with_javascript_rails_applications
---


Though at first it may seem intimidating, integrating a user interface with JavaScript as your frontend and Rails as your backend for an application is not quite so different as if you had used just Rails as your application program. The main difference is knowing how to communicate the session cookie information between both frontend and backend.

As we know from working with Rails, when a user interface is used, we are saving that user's session cookie in conjuction with the user's id. Per https://www.techopedia.com/definition/4910/session-cookie, "A session cookie contains information that is stored in a temporary memory location and then subsequently deleted after the session is completed or the web browser is closed. This cookie stores information that the user has inputted and tracks the movements of the user within the website." However, when working with a different frontend language, like JavaScript, we need to tell that frontend what the session information is and allow that information to be passed back and forth in order to properly save that user info.

As far as the controllers in Rails goes, the logic and format for our sign up, log in, and log out actions remains mostly the same. Assuming we are using a form for signing up and logging in, the logic will take that inputted data, verify it against any validations we have set up in our user model in Rails, and return something. For the login in, if validated, we want to return a positive json response indicating that we have a log in status and probably want to return the logged in user's info as well. If not validated, assume a status indicating so. For logout we'll return a json response with a status stating that we are logged out. Signing up follows a similar pattern of checking the validations and returning a json response depending on what occurs.

We need to set up our Application controller as such to create the sessions cookie token that we will be using going forward upon log in requests:
```
class ApplicationController < ActionController::API
    include ActionController::Cookies
    include ActionController::RequestForgeryProtection
    protect_from_forgery with: :exception
    before_action :set_csrf_cookie
    skip_before_action :verify_authenticity_token

    private

    def set_csrf_cookie
        cookies["CSRF-TOKEN"] = form_authenticity_token
    end
end
```

For our backend, we also need to set up our initializers so that we may avoid cross-origin sharing issues.
Set up your cors.rb as such:
```
 Rails.application.config.middleware.insert_before 0, Rack::Cors do
   allow do
     origins 'http://localhost:8000'
     resource '*',
       headers: :any,
       methods: [:get, :post, :put, :patch, :delete, :options, :head],
       credentials: true
   end
 end
 Rails.application.config.action_controller.forgery_protection_origin_check = false
```
 
Also, create afile in your initializers folder called session_store.rb and set it up like this:
```
if Rails.env == "production"
    Rails.application.config.session_store :cookie_store, key: "_yardsale", domain: "file:///C:/Users/zjsch/yardsale/yardsale-frontend/index.html"
else
    Rails.application.config.session_store :cookie_store, key: "_yardsale"
end
```

As for the frontend, the biggest point to remember is to include a certain phrase when doing your fetch requests to the Rails backend. It is the withCredentials: true portion in the second argument of the fetch function.
```
fetch(`http://localhost:3000/sessions`, {
            method: 'POST',
            headers: {
                'Content-type': 'application/json',
                'Accept': 'application/json',
                "X-CSRF-Token": this.getCookie("CSRF-TOKEN")
            },
            body: JSON.stringify({
                email: form.email.value,
                password: form.password.value,
            }),
            withCredentials: true
        })
```

You will also notice that in the headers portion of the code we set our cookie token. This is derived from a function added to the frontend to decode our cookie:
```
getCookie(cname) {
        var name = cname + "=";
        var decodedCookie = decodeURIComponent(document.cookie);
        var ca = decodedCookie.split(';');
        for(var i = 0; i <ca.length; i++) {
          var c = ca[i];
          while (c.charAt(0) == ' ') {
            c = c.substring(1);
          }
          if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
          }
        }
        return "";
    }
```

These are generally what is required to properly set up a system to communicate the session cookie info between your backend and frontend when using Rails and JavaScript. Depending on the coder's preferences, the syntax, design, layout, etc. may differ slightly.
