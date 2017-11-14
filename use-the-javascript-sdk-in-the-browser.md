
---

# Use the Javascript SDK in the browser

In order to communicate with your data in your Javascript application, you can use the Javascript SDK. This guide will tell you how to use the SDK in the browser .

The SDK currently exposes the following features:

* on-demand access to data stored in DataSets \(creating, reading, updating, deleting records\)
* real-time notifications for subscribed events
* Authentication and authorization is handled automatically by the SDK, the user only needs to provide credentials once at SDK initialization.

The SDK is currently focused on consuming data. Managing the data schema \(creating Datasets, adding columns to Datasets, etc.\) is out of scope for now.

## Code samples

Please keep in mind that this quick start guide uses Javascript 2017 syntax.

The examples are made with a simple data schema in mind: think a basic social media platform where`users`can write`posts`and/or`comments`to`posts`. A`post`can be related to any number of`comments`, while each`post`and each`comment`has a`user`as author.



