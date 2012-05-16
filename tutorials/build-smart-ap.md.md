---
layout: page
title: HOWTO Build a SMART App
tagline: for developers
includenav: smartnav.markdown
---
{% include JB/setup %}

<div id="toc"> </div>

This document is a complete SMART-App-Building walk-through. You should first read the [Main Page](../) 

#ScreenCast

We are re-recording the screencast to catch up with the latest API old [screencast](http://vimeo.com/20113823).


#Setting up your Environment

A SMART app is a web application that is loaded in an IFRAME hosted by a SMART container. That means you need to (a) write a web app, and (b) connect it to a SMART container. 

You can choose any toolkit you want to write a web app: Java Spring, Ruby on Rails, Python/Django, etc. For the purposes of this documentation, we've chosen webpy, a very simple, minimalist Python web framework, which helps us show you the important SMART-related code more quickly. Also, if you want to get going quickly with the more advanced app features, you probably want to stick with Java or Python for now, as those are the two programming languages in which we've built client libraries. That said, if you're comfortable with OAuth and REST, you can use another programming language without fear. 

We also provide you with a SMART EMR hosted at sandbox.smartplatforms.org. We call it the SMART Reference EMR, and we've loaded it with 50 patient records on which you can try out your app. To get going, you'll need to: 

Navigate to the [developers' sandbox] 

If you haven't done so already, create an account, otherwise just log back in 

Select a patient 

Run the app called "My App" 



This will open a SMART app iframe pointing to localhost:8000, which is where your app should be running. If you need an app with a different hostname (say, my_internal_server.net), just e-mail joshua dot mandel at childrens.harvard.edu with a manifest file and we'll set you up! 


##SMART Connect

Writing a purely browser-based app in HTML5 and JavaScript is as easy as including the client-side JavaScript libraries
and making API calls!  Keep in mind that SMART Connect calls can only access data while the end-user remains online,
since authentication depends on that user's existing session with the SMART container. If your app needs to access data
from your web application's backend or while the user is offline, you'll need to make some REST calls as well.

##SMART REST

Apps with server-side requirements, or apps that need offline access to the SMART API, use the REST interface, which
exposes data as resources accessible via HTTP GET, POST, PUT, or DELETE.  To ensure apps are authorized to access the
resources
they request, the SMART container authenticates each REST API call using OAuth, a scheme by which a SMART container or
user may delegate
access to applications.

The delegation takes the form of a token/secret pair, generated by the SMART container and handed off to the application
(with permission!). After tokens are obtained, each HTTP request is signed using the shared secret.

Writing a SMART REST app requires a bit more work than a SMART Connect app, because the app must be able to:

1.  Interact with the SMART container to obtain tokens
2.  Store tokens securely, maintaining appropriate sessions
3.  Select the appropriate token and sign each SMART REST API call

A few words about #1.  The [http://tools.ietf.org/html/rfc5849 OAuth specification] defines a "dance" among three
parties (client app, the server, and the resource owner) enabling the client app to obtain access tokens. SMART REST
apps obtain tokens by a simpler alternative using our JavaScript library, as explained in our tutorials.

To simplify the job of working with SMART REST, we provide client libraries in
[Java](https://github.com/chb/smart_client_java) and [Python](https://github.com/chb/smart_client_python python).

#OK, I'm ready to code

You'll want to follow our HOWTOs in order:

1. [HOWTO Build a SMART App](howto/build_a_smart_app), which focused on SMART Connect.
2. [HOWTO Build a SMART App](howto/build_a_rest_app) - REST API Calls
3. [HOWTO Build SMART Background and Helper Apps](howto/background_and_helper_apps)

For all of these, you can find our code on [SMART source code on github](https://github.com/chb/)