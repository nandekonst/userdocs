
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

## Importing the SDK in your browser application

In order to use the SDK in your browser application the SDK in the `<head>` section of your html page. In order to get access to the methods of the SDK you need to use the namespace `jexia` when calling a method.

```
<script src="path/to/jexia-sdk-js/dist/browser-jexia-sdk.min.js></script>
```

## Initialization and Authentication

The`jexiaClient()`function will return an instance of the`Client`class. The browser SDK will use the native`fetch`implementation.

## The Module System

The Jexia SDK is built as a set of modules \(or plugins\) structured around a core entity, \(the `Client` class used above\). In order to use a module, you need to :

* initialize it
* pass it to the `Client` when calling the`.init()`method

Probably the most useful module is the Data Operation Module \(`DataOperationsModule`class\). The example below will show how to initialize the SDK using this module. Follow the`dataModule`variable to see how this mechanism works.

Example:

```
<html>
    <head>
        <script src="path/to/jexia-sdk-js/dist/browser-jexia-sdk.min.js
    </head>
       <body>
           <a href="#" id="authorize">Authorize</a>
           <script type="text/javascript">
                document.getElementById("authorize").onclick = function(){
                    //Initialize dataOperationsModule
                    let dom = jexia.dataOperations();
                    let jexiaClient = jexia.jexiaClient().init({appUrl: "localhost", key: "anna@example.com", secret: "annie123"}, dom).then((initializedClient) => {

                        // you have been succesfully logged in!
                        // you can start using the initializedClient variable here

                            }
                        }).catch((error) => {      
                            console.log(error)
                        })
                    })
                }
           </script>
        </body>
</html>
```

## Dataset objects and Query objects

Using an initialized`DataOperationsModule`object, you can instantiate`Dataset`objects like so:

```
[..]
let posts = dom.dataset("posts");
[..]
```

Using a `Dataset` object, you can instantiate a `Query` object depending on the type of query you want to execute.

```
[..]
let selectQuery = posts.select();
let insertQuery = posts.insert( [ post1, post2 ] );
let updateQuery = posts.update( [ title: "Updated title" ] );
let deleteQuery = posts.delete();
[..]
```

Any Query can be executed by calling `.execute()`on it. This results in a `Promise` resolving to a set of records, regardless of the type of query executed.  For select queries, the records returned are the records that the user wants to retrieve. For the other queries, the records returned are the actual records that have been operated on \(modified, added or deleted\).

Each different`Query`type has different support for the query options \(filtering, sorting, etc.\). E.g. you cannot apply filtering to insert queries, as the method isn't defined on the`InsertQuery`object.

### Selecting all records from a dataset

Lets select all records of a dataset. If you watch closely, you will notice that the API is chainable.

```
<html>
    <head>
        <script src="yourpath/dist/js/browser-jexia-sdk.min.js"></script>
    </head>
       <body>
           <a href="#" id="authorize">Authorize</a>
           <script type="text/javascript">
                document.getElementById("authorize").onclick = function(){
                    //Initialize dataOperationsModule
                    let dom = jexia.dataOperations();
                    let jexiaClient = jexia.jexiaClient().init({appUrl: "localhost", key: "anna@example.com", secret: "annie123"}, dom).then((initializedClient) => {
                        dom.dataset("posts").select().execute().then((records) => {
                                //do something with your data
                            }
                            console.log(JSON.stringify(data))
                        }).catch((error) => {      
                            console.log(error)
                        })
                    })
                }
           </script>
        </body>
</html>
```

We can also use temporary variables to point out the different objects and functionality involved when working with records. At the very least, defining dataset variables could come in handy when executing multiple different queries on the same dataset.

```
<html>
    <head>
        <script src="yourpath/dist/js/browser-jexia-sdk.min.js"></script>
    </head>
       <body>
           <a href="#" id="authorize">Authorize</a>
           <script type="text/javascript">
                document.getElementById("authorize").onclick = function(){
                    //Initialize dataOperationsModule
                    let dom = jexia.dataOperations();
                    let jexiaClient = jexia.jexiaClient().init({appUrl: "localhost", key: "anna@example.com", secret: "annie123"}, dom).then((initializedClient) => {
                        let posts = dom.dataset("posts")
                        let unexecutedQuery = dom.select();
                        let executedQueryPromise = unexecutedQuery.execute();
                           executedQueryPromise.then((records) => {
                                //do something with your data
                            }
                            console.log(JSON.stringify(data))
                        }).catch((error) => {      
                            console.log(error)
                        })
                    })
                }
           </script>
        </body>
</html>
```

### Sorting records

To activate sorting, you need to call `.sortAsc()` or`.sortDesc()` on a `Query` object and pass as string the name of the field you want to sort by.

```
[..]
posts.select().sortAsc("id").execute().then( (records) => {
    //operate on your sorted records here
})
[..]
```

### Limit and offset

You can use`.limit`and`.offset`on a`Query`object for these options. They can be used separately or together. Only setting the limit \(to a value X\) will make the query operate on the first X records. Only setting the offset will make the query operate on the last Y records, starting from the offset value.

```
[..]
posts.select().limit(2).offset(5).execute().then( (records) => {
  // records will be an array of 2 records, starting from position 5 in the Dataset
});
[..]
```

### Only retrieving certain fields

You can use the `.fields`method to define what fields you want to retrieve.

```
[..]
posts.select().fields("id", "title").execute().then( (records) => {
  // the individual record objects will only have the two properties defined above
});
[..]
```

### Filtering records

You can use the filtering feature to select what records a certain query will operate on.

In order to define a filter, you need to use the appropriate filtering objects. They can be created using the exposed methods`field`and`combineCriteria`.`combineCriteria`is something very specific that provides another way to create nested logical conditions. You're probably not going to use that much, but it's useful to know that it exists.



