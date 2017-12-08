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

## Copy URL
You can operate on your data using the API URL:


## Javascript SDK
With the Javascript SDK you can perform CRUD operations on your data within your application. The Javascript SDK can be used server-side and browser-side. 

### Installation:
Install the Javascript SDK through npm by using:

`npm install jexia-sdk-js --save`



### Server-side:


### Browser-side:




In this example we will populate our dataset and fetch the data afterwards using a simple node.js script. 

For more detailed information about the functionality of the SDK please read ""

(hello world example with SDK)

## REST API
  * curl (POST, GET, PUT, DEL)
  * postman (POST, GET, PUT, DEL)
  


