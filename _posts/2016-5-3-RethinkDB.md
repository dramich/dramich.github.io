---
layout: post
title: RethinkDB Changefeeds with thinky.io
---

One of the main draws of RethinkDB is it's real-time streaming of data from the database without having to re-query your data.
Well, what does this mean and how is it useful? Why do I care? If you are asking these questions you are in the right place.

Building modern apps requires data, real-time updates and users want it all to be seamless; no page reloading, waiting for updates,
or lag in the UI. If your app is having to poll your server every so often to grab updates that means there is a lag in your data
being displayed. The user may not notice this half second delay but YOU know it's there.

To fix this issue RethinkDB has an amazing feature called Changefeeds, which also happens to be the main draw of the database.
So what does it do? It allows you to setup a predefined query, say on a specific table, and every time there is a new record added
RethinkDB will automatically send that new document into a feed for you to grab!

Where does thinky.io come into this picture? Simple, it's an ORM that you use on top of RethinkDB. If you are familiar with
mongoose and MongoDB, then you should be right at home using thinky.io.

Let's take a look at a quick example.

```javascript
var Users = thinky.createModel("Users", {
  id: type.string(),
  name: type.string()
});

Users.changes().then((feed) => {
  feed.each((error, doc) => {
    if (error) {
      console.log(error);
    } else {
    console.log('changes feed: ', doc);
    }
  });
}).error((error) => {
  console.log(error);
});
```
In this code we setup a user schema which looks pretty normal. We then setup the change feed listener with Users.changes().
This is going to watch the Users table for new docs and when they get added the feed.each() is going to take that doc and pass it into
the next function. We are just console logging the new doc in this example.

And that's it! You can setup Changefeeds on tables, specific docs, a set of docs, most things RethinkDB will let you use to query can be
chained together and used with the Changefeeds.

Check out [RethinkDB](https://www.rethinkdb.com/) and [thinky.io](https://thinky.io/) for more info.
