# Getting started
This guide helps you to set up your Jexia project and to start interact with your data in just a few steps.

## Create a project in the Jexia Dashboard
After you created your account, login to the Jexia Dashboard to create your project. Within a project you can create datasets, add fields to them, set up field validation and make relations between your datasets.

After login you can create a project by clicking the My Projects menu item.

![create_project](/create-project.png "Create Project")


## Create datasets
In order to interact and perform CRUD operations on your data, you need to store the data in a dataset. In order to do so, you need to create the dataset first. Click on your project. Now click the button "create new dataset":

![create_dataset](/create-dataset.png "Create Dataset")


Name your dataset. The name of the dataset is used as endpoint to allow you to communicate with the API.

![name_dataset](/create-dataset2.png "Name Dataset")

## Add fields to your dataset or store your data schemaless
The next step is to add fields to your datasets. However, it is also possible to store your data schemaless. In that case it is not necessary to create fields.

In order to create a field, click the "Add field" button. Name your field and set its datatype. Data can be of type: `String`, `Integer`, `Float`, `Date`, `Datetime`, `Boolean` or `JSON`:

![add_field](/add-field.png "Add Field")


## Copy URL
You can make CRUD operations on your data using the API URL. FOperating on datasets using the SDK only requires your project ID and your user name and password

![copy_url](/copy_url.png "Copy URL")



## Javascript SDK
You can wire up the connection between your application and your datasets and start consuming data using the Javascript SDK. The Javascript SDK can be used server-side and browser-side. 
The SDK currently exposes the following features:

* on-demand access to data stored in datasets (creating, reading, updating, deleting records)
* real-time notifications for subscribed events
* Authentication and authorization is handled automatically by the SDK, the user only needs to provide credentials once at SDK initialization.

### Installation:
Install the Javascript SDK through npm by using:

`npm install jexia-sdk-js --save`


### Server-side:
include the SDK in your node.js application:

`const jexiaSDK = require('jexia-sdk-js/node');`

#### Initialization and Authentication
The`jexiaClient()`function will return an instance of the`Client`class. On Node.JS, you will need to provide a`fetch`standard compliant function as a parameter. You will need to add a compatible dependency to your project. For development of the SDK we've used`node-fetch`.

`const fetch = require("node-fetch");`

In order to authenticate and operate on our datasets we need initialize a `Jexia CLient` and a `DataOperationsModule`.
The Jexia SDK is built as a set of modules \(or plugins\) structured around a core entity \(the`Client`class used above\). In order to use a module you need to:

* initialize it
* pass it to the
  `Client`
  when calling the
  `.init()`
  method

```
const jexiaSDK = require('jexia-sdk-js/node');
const fetch = require('node-fetch');
const jexiaClient = jexiaSDK.jexiaClient;
const dataOperations = jexiaSDK.dataOperations;

//Initialize DataOperationsModule
let dataModule = dataOperations();

//Initialize Client and pass DataOperationsModule to it.
let client = jexiaClient(fetch).init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password"}, dataModule);

```

#### Operate on datasets

The user can execute the following operations on records:

* create `[INSERT]`
* read `[GET]`
* update `[PATCH]`
* delete `[DELETE]`

##### Populate the dataset: `[INSERT]`

```
const jexiaSDK = require('jexia-sdk-js/node');
const fetch = require('node-fetch');
const jexiaClient = jexiaSDK.jexiaClient;
const dataOperations = jexiaSDK.dataOperations;

//Initialize DataOperationsModule
let dataModule = dataOperations();

//Initialize Client and pass DataOperationsModule to it.
let client = jexiaClient(fetch).init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password"}, dataModule);

function insertRecord(jexiaClient){
    jexiaClient.then( (initializedClient) => {
        let postDataset = dataModule.dataset("posts");
        postDataset.insert([{title: "Super awesome post", content:"super awesome content", author:"the author name"}]).execute().then( (records) => {
            console.log("New Record" + records);
            process.exit();
        }).catch( (error) => {
            // there was a problem retrieving the records
            console.log(error);
            process.exit();
        });
    });
}

insertRecord(client);

```

##### Fetch the records `[GET]`:

```
const jexiaSDK = require('jexia-sdk-js/node');
const fetch = require('node-fetch');
const jexiaClient = jexiaSDK.jexiaClient;
const dataOperations = jexiaSDK.dataOperations;

//Initialize DataOperationsModule
let dataModule = dataOperations();

//Initialize Client and pass DataOperationsModule to it.
let client = jexiaClient(fetch).init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password"}, dataModule);

//select Records
function selectRecords(jexiaClient){
    jexiaClient.then( (initializedClient) => {
        let postDataset = dataModule.dataset("posts");
        postDataset.select().execute().then( (records) => {
            console.log(records);
            process.exit();
        }).catch( (error) => {
            // there was a problem retrieving the records
            console.log(error);
            process.exit();
        });
    });
}

selectRecords(client);

```

##### Update the record `[PATCH]`

```
const jexiaSDK = require('jexia-sdk-js/node');
const fetch = require('node-fetch');
const jexiaClient = jexiaSDK.jexiaClient;
const dataOperations = jexiaSDK.dataOperations;

//Initialize DataOperationsModule
let dataModule = dataOperations();

//Initialize Client and pass DataOperationsModule to it.
let client = jexiaClient(fetch).init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password"}, dataModule);

function updateRecord(jexiaClient){
    jexiaClient.then( (initializedClient) => {
        let postDataset = dataModule.dataset("posts");
        postDataset.update({title: "Super awesome post2"}).where(field("title").isEqualTo("Super awesome post")).execute().then( (records) => {
            console.log("Record " + JSON.stringify(records)) ;
            process.exit();
        }).catch( (error) => {
            // there was a problem retrieving the records
            console.log(error);
            process.exit();
        });
    });
}

updateRecord(client)

```

##### Delete the record `[DELETE]`

```
const jexiaSDK = require('jexia-sdk-js/node');
const fetch = require('node-fetch');
const jexiaClient = jexiaSDK.jexiaClient;
const dataOperations = jexiaSDK.dataOperations;

//Initialize DataOperationsModule
let dataModule = dataOperations();

//Initialize Client and pass DataOperationsModule to it.
let client = jexiaClient(fetch).init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password"}, dataModule);

//delete records
function deleteRecord(jexiaClient){
    jexiaClient.then( (initializedClient) => {
        let postDataset = dataModule.dataset("posts");
        postDataset.delete().where(field("title").isEqualTo("Super awesome post2")).execute().then( (records) => {
            console.log("Record " + JSON.stringify(records)) ;
            process.exit();
        }).catch( (error) => {
            // there was a problem retrieving the records
            console.log(error);
            process.exit();
        });
    });
}

deleteRecord(client);

```
##### Listen to Real Time Events
The real-time functionality is added through a separate module. The module needs to be imported, instantiated and initialized along with the client.

```
const realTime = jexiaSDK.realTime;

```
The real-time module needs a websocket client in order to function. 

```
const ws = require('ws');

```

For Node.JS apps, a websocket client needs to be imported and a callback instantiating the websocket client must be passed to the real-time module, as in this example.

```
const jexiaSDK = require('jexia-sdk-js/node');
const fetch = require('node-fetch');
const jexiaClient = jexiaSDK.jexiaClient;
const dataOperations = jexiaSDK.dataOperations;

const ws = require('ws');
const realTime = jexiaSDK.realTime;

let rtc = realTime((messageObject) => {
  console.log("Realtime message received:");
  console.log(messageObject);
}, (url) => {
    return new ws(url, {origin: "http://localhost"});
});

```
The real-time module needs to be passed to the Client when initializing the latter. The Client accepts a spread parameter to define the modules that need to be initialized.

```
[..]
//Initialize Client and pass DataOperationsModule and RTC module to it.
let client = sdk.jexiaClient(fetch).init({projectID: "<your-project-id>", key: "<your-user-name>", secret: "<your-password>"}, dataModule, rtc);
[..]

```
After a succesful module initialization, the user can start subscribing to events. When a real-time message is pushed from the server, the callback defined when instantiating the real-time module will be called.

```
[..]

rtc.subscribe('insert', dataModule.dataset('posts')

[..]

```

The Client class exposes a method called `.terminate()` which returns a `Promise` with the terminated `Client` instance. Use this to clear up resources used by the `Client` class and any modules you initialized along with it (you don't have to pass the modules along, the `Client` will terminate any modules you supplied on initialization.)

```
 jexiaClient.terminate().then( (terminatedClient) => {
   // everything has been cleared
 }).catch( (err) => {
   // something went wrong when cleaning up
 })

```

### Full RTC Example

```
let sdk = require('jexia-sdk-js/node');
let fetch = require('node-fetch');
const realTime = sdk.realTime;
const ws = require('ws');


//Initialize DataOperationsModule
let dataModule = sdk.dataOperations();

//Initialize RTC Module
let rtc = realTime((messageObject) => {
    console.log("Realtime message received:");
    console.log(messageObject);
  }, (url) => {
      return new ws(url, {origin: "http://localhost"});
  });

let jexiaClientInstance = jexiaClient(fetch);

jexiaClientInstance.init({projectID: "<your-project-id>", key: "<your-user-name>", secret: "<your-password>"}, dataModule, rtc).then( () => {
  return rtc.subscribe("insert", dataModule.dataset("posts")).then( () => {
    console.log("Succesfully subscribed to dataset changes");
    return dataModule.dataset("posts").insert([{content: "aNewKeyword"}, {title: "anotherKeyword"}]).execute();
  }).then( (records) => {
    console.log("HTTP response to request query received, shutting down in 5, 4, 3...");
    setTimeout( () => {
      jexiaClientInstance.terminate().then( () => process.exit() );
    }, 5000);
  });
}).catch( (err) => {
  console.log(err.message);
  jexiaClientInstance.terminate().then( () => process.exit() );
});




```


[Complete SDK functionality for serverside use](use-the-javascript-sdk-serverside.md)

### Browser-side:

In order to use the SDK in your browser application the SDK in the <head> section of your html page. In order to get access to the methods of the SDK you need to use the namespace `jexia` when calling a method.
  
  `<script src="path/to/jexia-sdk-js/dist/browser-jexia-sdk.min.js></script>`
  
The `jexiaClient()` function will return an instance of the `Client` class. The browser SDK will use the native `fetch` implementation.

#### Initialization and Authentication

The Jexia SDK is built as a set of modules (or plugins) structured around a core entity, (the `Client` class used above). In order to use a module, you need to :

* initialize it
* pass it to the `Client` when calling the `.init()` method
Probably the most useful module is the Data Operation Module (`DataOperationsModule` class). The example below will show how to initialize the SDK using this module. Follow the `dataModule` variable to see how this mechanism works.

Example:

```
<html>
    <head>
       <script src="node_modules/jexia-sdk-js/browser.js"></script>    
    </head>
    <body>
            <a href="#" id="authorize">Authorize</a>
            <script type="text/javascript">
                 document.getElementById("authorize").onclick = function(){
                     //Initialize dataOperationsModule
                     let dataModule = jexia.dataOperations();
                     let jexiaClient = jexia.jexiaClient().init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password>"}, dataModule).then((initializedClient) => {
                      
                             // you have been succesfully logged in!
                            // you can start using the initializedClient variable here
                    }
            </script>
    </body>
</html>


```
#### Operate on datasets

The user can execute the following operations on records:

* create `[INSERT]`
* read `[GET]`
* update `[PATCH]`
* delete `[DELETE]`

##### Populate the dataset: `[INSERT]`

```
 <script type="text/javascript">
                 document.getElementById("authorize").onclick = function(){
                     //Initialize dataOperationsModule
                     let dataModule = jexia.dataOperations();
                     let jexiaClient = jexia.jexiaClient().init({projectID: "<your-project-id>", key: "<your-user-name>", secret: "your-password"}, dataModule).then((initializedClient) => {
        dataModule.dataset("posts").insert([{title:'The title', content: 'the content'}]).execute().then((records) => {         
                             let data = records;
                   
                             console.log("Inserted..." + JSON.stringify(data))
                         }).catch((error) => {      
                             console.log(error)
                         })
                     })
                 }
            </script>

```

##### Fetch the records `[GET]`:

```
  <a href="#" id="authorize">Authorize</a>
            <script type="text/javascript">
                 document.getElementById("authorize").onclick = function(){
                     //Initialize dataOperationsModule
                     let dataModule = jexia.dataOperations();
                     let jexiaClient = jexia.jexiaClient().init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password>"}, dataModule).then((initializedClient) => {
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

##### Update the record `[PATCH]`

```
    <script type="text/javascript">
                 document.getElementById("authorize").onclick = function(){
                     //Initialize dataOperationsModule
                     let dataModule = jexia.dataOperations();
                     let jexiaClient = jexia.jexiaClient().init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password>"}, dataModule).then((initializedClient) => {
                         dataModule.dataset("posts").update({title: "aNewKeyword2"}).where(field("title").isEqualTo("aNewKeyword")).execute().then((records) => {
                             let data = records;
                            
                             console.log("Updated record" + JSON.stringify(data))
                         }).catch((error) => {      
                             console.log(error)
                         })
                     })
                 }
            </script>

```

##### Delete the record `[DELETE]`

```
    <script type="text/javascript">
                 document.getElementById("authorize").onclick = function(){
                     //Initialize dataOperationsModule
                     let dataModule = jexia.dataOperations();
                     let jexiaClient = jexia.jexiaClient().init({projectID: "<your-project-id>", key: "<your-username>", secret: "<your-password>"}, dataModule).then((initializedClient) => {
      dataModule.dataset("posts").delete().where(field("title").isEqualTo("My post")).execute().then((records) => {
                             let data = records;
                            
                             console.log("Deleted record" + JSON.stringify(data))
                         }).catch((error) => {      
                             console.log(error)
                         })
                     })
                 }
            </script>

```

##### Listen to Real Time Events



```
<script type="text/javascript">
                 document.getElementById("authorize").onclick = function(){
                     //Initialize dataOperationsModule
                     let dataModule = jexia.dataOperations();
                     let rtc = jexia.realTime((messageObject) => {
                         console.log(messageObject)
                     }, (url) => {
                         return new WebSocket(url)
                     });
 </script>


```

The real-time functionality is added through a separate module. The module needs to be imported, instantiated and initialized along with the client.

In the browser the real-time module uses the native [WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket) object of the browser

The real-time module needs a websocket client in order to function. 



### Full RTC Example
The real-time functionality is added through a separate module. The module needs to be imported, instantiated and initialized along with the client.

```
 <script type="text/javascript">
                 document.getElementById("authorize").onclick = function(){
                     //Initialize dataOperationsModule
                     let dataModule = jexia.dataOperations();
                     
                     //Initialize rtc
                     let rtc = jexia.realTime((messageObject) => {
                         console.log(messageObject)
                     }, (url) => {
                         return new WebSocket(url)
                     });
                     
                     
 let jexiaClient = jexia.jexiaClient().init({projectID: "<your-project-id>", key:   "<your-user-name>", secret: "<your-password>"},rtc, dataModule).then((initializedClient) => {
                        console.log(initializedClient);
                        const posts = dataModule.dataset('posts');
                        rtc.subscribe('post', posts);
                        setTimeout(() => {
                            posts.insert([{title: "My realtime post", content: "Content of my realtime post"}]).execute().then( (records) =>{
                                console.log("Inserted records" + JSON.stringify(records))
                            }).catch((error) => {
                                console.log(error)
                            });
                        }, 1000)   
                     });
                 }
            </script>

```


## REST API
  * curl (POST, GET, PUT, DEL)
  * postman (POST, GET, PUT, DEL)
  


