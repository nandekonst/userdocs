
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
<script type="text/javascript">
                 document.getElementById("authorize").onclick = function(){
                     //Initialize dataOperationsModule
                     let dataModule = jexia.dataOperations();
                     let jexiaClient = jexia.jexiaClient().init({projectID: "<your-project-id>", key: "<your-usernam>", secret: "<your-password"}, dataModule).then((initializedClient) => {
                         dataModule.dataset("posts").select().execute().then((records) => {
                             let data = records;
                             for(let i=0; i < data.length; i++){
                                 document.write("<ul><li>" + data[i].title + "</li></ul>") 
                             }
                             console.log(JSON.stringify(data))
                         }).catch((error) => {      
                             console.log(error)
                         })
                     })
                 }
            </script>


```

## Dataset objects and Query objects

Using an initialized`DataOperationsModule`object, you can instantiate`Dataset`objects like so:

```
[..]
let posts = dataModule.dataset("posts");
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
                    let dataModule = jexia.dataOperations();
                    let jexiaClient = jexia.jexiaClient().init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password"}, dataModule).then((initializedClient) => {
                        dataModule.dataset("posts").select().execute().then((records) => {
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
                    let dataModule = jexia.dataOperations();
                    let jexiaClient = jexia.jexiaClient().init({appUrl: "localhost", key: "anna@example.com", secret: "annie123"}, dataModule).then((initializedClient) => {
                        let posts = dataModule.dataset("posts")
                        let unexecutedQuery = posts.select();
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

```
let simpleCriterion = field("username").isEqualTo("Tom");
let combinedCriteria = simpleCriterion.or(field("username").isEqualTo("Dick"));
```

In order to use these conditions, they need to be added to a query using the`.filter`method

```
[..]
posts.select().filter(field("username").isEqualTo("Harry"));
[..]
```

Multiple`.filter`calls can be chained, but only the last call will be taken into account. If a complex condition needs to be set for filtering, it has to be created in one go \(in-line or not\) and passed as an argument to the`.filter`method.

Filtering conditions can be nested at any level.

```
[..]
let flatFilter = field("first_name").isEqualTo("Tom")
                 .or( field("first_name").isEqualTo("Dick"))
                 .or( field("first_name").isEqualTo("Harry"));

let nestedFilter = field("first_name").isEqualTo("Tom")
                   .or( field("first_name").isEqualTo("Dick")
                        .and( field("middle_name").isEqualTo("Harry")));

let anotherNestedFilter = field("first_name").isEqualTo("Tom")
                   .or( field("first_name").isEqualTo("Dick")
                        .and( field("middle_name").isEqualTo("Harry")
                              .or( field("middle_name").isEqualTo("Larry"))));
[..]
```

Filtering operator list and examples

You can find a complete list of the operators supported for filtering in the API reference document.

### Defining relations

Relations can be added to a query in order to have the query apply not only to the main dataset the query is created from, but also to related records from other datasets.

Retrieving relations:

```
[..]
let posts = dataModule.dataset("posts");
let comments = dataModule.dataset("comments");
posts.select().relation(comments).execute().then( (records) => {
    //objects in the records array will now contain a property called "comments"
    //which will be an array holding the comments related to a particular post
});
[..]
```

### Inserting records

```
[..]
let posts = dataModule.dataset("posts");
posts.insert([ {title: "New Post", content:"content here"}, 
               {title: "Another Post", content:"some more content"} 
]).execute().then( (records) => {
  // you will be able to access the newly inserted records here
  // complete with their generated IDs
}).catch( (error) => {
  // you can see the error info here, if something goes wrong
});
[..]
```

### Deleting records

```
[..]
let posts = dataModule.dataset("posts");
posts.delete().filter(field("title").isEqualTo("test")).execute().then( (records) => {
  // you will be able to access the deleted records here
  // they won't be stored in the DB anymore, but maybe you
  // want to display a visual confirmation of what got deleted
}).catch( (error) => {
  // you can see the error info here, if something goes wrong
});
[..]
```

## Real-time communication

The real-time functionality is added through a separate module. The module needs to be imported, instantiated and initialized along with the client.

### Importing

```
<script src="path/to/jexia-sdk-js/dist/browser-jexia-sdk.min.js></script>
```

### Initializing

The real-time module needs to be passed to the`Client`when initializing the latter. The`Client`accepts a spread parameter to define the modules that need to be initialized.

```
    .init({appUrl: 'localhost', key: 'anna@example.com', secret: 'annie123'}, rtc, doops)
    .then((cli) => {
      console.log(cli);
      const posts = doops.dataset("posts");
      rtc.subscribe('post', posts);
      setTimeout(() => {
        posts.insert([{
          category_id: 1,
          post: "Example 2",
          posted: true,
          title: "Other post 3",
          user_id: 1
        }]).execute().then( (records) => {
          console.log(records);
        }).catch( (error) => {
          console.log(error);
        });
      }, 1000);
    });
```

### Subscribing to events

After a succesful module initialization, the user can start subscribing to events. When a real-time message is pushed from the server, the callback defined when instantiating the real-time module will be called.

```
[..]

const posts = doops.dataset("posts");
rtc.subscribe('post', posts);

[..]
```

### Logging of and cleaning up

The`Client`class exposes a method called`.terminate()`which returns a`Promise`with the terminated`Client`instance. Use this to clear up resources used by the`Client`class and any modules you initialized along with it \(you don't have to pass the modules along, the`Client`will terminate any modules you supplied on initialization.\)

```
[..]
jexia.jexiaClient().terminate().then( (terminatedClient) => {
  // everything has been cleared
}).catch( (err)=>{
  // something went wrong when cleaning up
});
[..]
```

### Full example

Here is a full browser example which displays the data in the browser.

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
                            let data = records;
                            for(let i=0; i < data.length; i++){
                                document.write("<ul><li>" + data[i].title + "</li></ul>") 
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



