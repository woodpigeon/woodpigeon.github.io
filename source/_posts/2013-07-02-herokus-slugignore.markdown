---
layout: post
title: "Heroku's .slugignore"
date: 2013-07-02 23:27
comments: true
categories: Heroku
published: true
---



Keeping your Heroku slug size down is a good idea if you have web dynos you want to auto-scale, or you are starting a lot of worker dynos.  According to Heroku, a small slug is more nimble (imagine!) because it allows new dynos to be initialised and spun up more quickly.

Recently reading [Heroku: Up and Running](http://shop.oreilly.com/product/0636920027409.do) - a usefully concise and no-nonsense book - I found among the gems there something that I seem to have missed - the [.slugignore](https://devcenter.heroku.com/articles/slug-compiler#ignoring-files-with-slugignore) file. Similar in concept to a .gitignore, once added to your project folder you can use it to specify which folders and files Heroku should exclude when compiling your slug. (Those files and folders still remain in the Heroku git remote repo, they are just excluded from the deployed code base).

Armed with this new knowledge and dizzy with anticipation, I added a .slugignore to an existing Rails app, excluded all tests and docs, and pushed to Heroku. My slug downsized from 38.5 MB to ...38.5 MB. Some rounding in the reporting of this figure by Heroku has obscured the fact the change in slug size is, well, quite small. 

The conclusion is pretty obvious and I should have seen it coming: you need to be able to exclude some pretty weighty files before seeing a significant reduction in your slug size; after all, your code is pretty insignificant next to all those gem dependencies Heroku shoehorns into your slug.

While I think I'll include a .slugignore in new Heroku apps - as a reminder to be vigilant for large, non-essential files and folders - I think better slug-slimming mileage is had by scrutinising the Gemfile for debug and test gems that are creeping unnoticed into production, and using [groups](http://bundler.io/v1.3/groups.html) to filter these out.

Something to watch, and the book hints at this, is that an aggressive .slugignore could trip you up during deployment. If for example you choose to globally exclude *.pdf, but then you decide to add a user-downloadable pdf document, your pdf will not get deployed. That could be a pretty confusing issue if the existence or meaning of the .slugignore has dropped off the edge of your memory!