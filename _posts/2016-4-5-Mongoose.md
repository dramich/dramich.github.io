---
layout: post
title: Mongoose/MongoDB with Heroku in Mind
---

Setting up a MongoDB using Mongoose is a great way to get a serious backend for
your project running and it doesn't take a lot of time. Actually putting things
into and getting them back out of your Mongo database can be a bit more tricky but
we will leave that for another time.

If you need some help setting up MongoDB [this](http://stackoverflow.com/questions/2404742/how-to-install-mongodb-on-windows "How to install mongoDB on windows?")
will help.

Assuming you already have MongoDB up and running let's start with the basics.
You are going to want to add Mongoose to your project by running the below command.

```javascript
$ npm install mongoose --save
```
Once Mongoose is installed we need to setup the connection to our currently running MongoDB.  

* Require Mongoose in your current file
* Setup the MongoURI (we are setting ours up to either use the data provided
  through the environment on Heroku or our local system)
* Start a connection with the database
* Check for errors or let us know we have a connection
* Export the connection for use in other places

```javascript
var mongoose = require('mongoose');

mongoURI = process.env.MONGOLAB_URI || 'mongodb://localhost/databaseName';

mongoose.connect(mongoURI);

var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  console.log('Mongo Connection Initialized');
});

module.exports = db;
```

And that is it. You should now be up and running with a connection to your MongoDB using Mongoose.
