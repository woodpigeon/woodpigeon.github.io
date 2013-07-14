---
layout: post
title: "Moving from EC2 to Heroku"
date: 2013-06-13 16:32
comments: true
categories: 
- Heroku
- EC2
published: false
---

Like a lot of developers, have been using [Heroku](http://www.heroku.com) for a few years for deploying rails and ruby prototypes and experimental throw away stuff. Its built on Amazon EC. deploying an app is a cinch, and there are great add-ons for integrating services like databases, logging etc. There's not much to dislike except for one big thing (for me) - the cross-Atlantic latency. Because I'm in the UK and Heroku's data centre is in the us-east region, you can add maybe 100-300 ms per traversal.

But since the April this year [Heroku apps can deployed in the Amazon eu-west region](https://blog.heroku.com/archives/2013/4/24/europe-region) in Ireland, which is pretty fantastic.


