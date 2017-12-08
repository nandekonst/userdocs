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


[Complete SDK functionality](use-the-javascript-sdk-serverside.md)

### Browser-side:






(hello world example with SDK)

## REST API
  * curl (POST, GET, PUT, DEL)
  * postman (POST, GET, PUT, DEL)
  


