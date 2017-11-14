# Use the Javascript SDK Serverside:

In order to communicate with your data in your Javascript application, you can use the Javascript SDK. This guide will tell you how to use the SDK serverside \(nodejs\) . In order to use your data serverside you need to have Nodejs installed.

The SDK currently exposes the following features:

* on-demand access to data stored in DataSets \(creating, reading, updating, deleting records\)
* real-time notifications for subscribed events
* Authentication and authorization is handled automatically by the SDK, the user only needs to provide credentials once at SDK initialization.

The SDK is currently focused on consuming data. Managing the data schema \(creating Datasets, adding columns to Datasets, etc.\) is out of scope for now.

## Code Samples {#code-samples}

Please keep in mind that this quick start guide uses Javascript 2017 syntax.

The examples are made with a simple data schema in mind: think a basic social media platform where`users`can write`posts`and/or`comments`to`posts`. A`post`can be related to any number of`comments`, while each`post`and each`comment`has a`user`as author.

## Importing the SDK into your node project

You can install the SDK through NPM:

`npm install jexia-sdk-js --save`

Now include the SDK in your project:

`var sdk = require('jexia-sdk-js/node');`

## Initialization and Authentication

The`jexiaClient()`function will return an instance of the`Client`class. On Node.JS, you will need to provide a`fetch`standard compliant function as a parameter. You will need to add a compatible dependency to your project. For development of the SDK we've used`node-fetch`

```
sdk = require('jexia-sdk-js/node');
fetch = require("node-fetch");

let initializedClientPromise = sdk.jexiaClient(fetch).init({appUrl: "your Jexia App URL", key: "username", secret: "password"});
initializedClientPromise.then( (initializedClient) => {
  // you have been succesfully logged in!
  // you can start using the initializedClient variable here
}).catch( (error) => {
  // uh-oh, there was a problem logging in, check the error.message for more info
});
```

## The Module system

The Jexia SDK is built as a set of modules \(or plugins\) structured around a core entity \(the`Client`class used above\). In order to use a module you need to:

* initialize it
* pass it to the
  `Client`
  when calling the
  `.init()`
  method

Probably the most useful module is the Data Operation Module \(`DataOperationsModule`class\). The example below will show how to initialize the SDK using this module. Follow the`dataModule`variable to see how this mechanism works.

```
sdk = require('jexia-sdk-js/node');
fetch = require("node-fetch");

let dataModule = sdk.dataOperations();

let initializedClientPromise = sdk.jexiaClient(fetch).init({appUrl: "your Jexia App URL", key: "username", secret: "password"}, dataModule);
initializedClientPromise.then( (initializedClient) => {
  // you have been succesfully logged in!
  // you can start using the dataModule variable to operate on records here
}).catch( (error) => {
  // uh-oh, there was a problem logging in, check the error.message for more info
});
```

## Dataset objects and Query objects

Using an initialized `DataOperationModule` object, you can instantiate `Dataset` objects like so:

```
[..]
let posts = dataModule.dataset("posts");
[..]
```

Using a `Dataset` object, you can instantiate a `Query` object, depending on the type of query you want to execute.

```
[..]
let selectQuery = postsDataset.select();
let insertQuery = postsDataset.insert( [ post1, post2 ] );
let updateQuery = postsDataset.update( [ title: "Updated title" ] );
let deleteQuery = postsDataset.delete();
[..]
```

Any`Query`can be executed by calling`.execute()`on it. This results in a`Promise`resolving to a set of records, regardless of the type of`Query`executed. For select queries, the records returned are the records that the user wants to retrieve. For the other queries, the records returned are the actual records that have been operated on \(modified, added or deleted\).

Each different`Query`type has different support for the query options \(filtering, sorting, etc.\). E.g. you cannot apply filtering to insert queries, as the method isn't defined on the`InsertQuery`object.

### Selecting all records from a dataset

Using all the temporary variables in this example is for demonstration purposes, mostly to point out the different objects and functionality involved when working with records.

```
[..]
sdk.jexiaClient(fetch).init({appUrl: "your Jexia App URL", key: "username", secret: "password"}, dataModule).then( (initializedClient) => {
  let posts = dataModule.dataset("posts");
  let unexecutedQuery = postsDataset.select();
  let executedQueryPromise = unexecutedQuery.execute();
  executedQueryPromise.then( (records) => {
    // you can start iterating through the posts here
  }).catch( (error) => {
    // there was a problem retrieving the records
  });
});
[..]
```

If you watch closely, you will see that the API is chainable, so you can write it in a much less verbose way:

```
[..]
sdk.jexiaClient(fetch).init({appUrl: "your Jexia App URL", key: "username", secret: "password"}, dataModule).then( (initializedClient) => {
  dataModule.dataset("posts").select().execute().then( (records) => {
    // you can start iterating through the posts here
  }).catch( (error) => {
    // there was a problem retrieving the records
  });
});
[..]
```



