# Get started

# Create a project in the Jexia Console

# Create datasets

# Add fields

# Make relations

# Interact with your data

You can wire up the connection between your application and your datasets and start consuming data using the Javascript SDK.

The SDK currently exposes the following features:

* on-demand access to data stored in datasets \(creating, reading, updating, deleting records\)
* real-time notifications for subscribed events
* Authentication and authorization is handled automatically by the SDK, the user only needs to provide credentials once at SDK initialization.

## On-demand data access

The user can execute the following operations on records:

* create
* read
* update
* delete

Executing an operation on a set of records is done through a Query. Depending on their type, Queries give the user access to some \(or all\) of the following options:

* filtering \(only records satisfying a certain condition will be retrieved/affected\)
* sorting \(the records will be sorted by a rule and direction before the action is executed\)
* limiting/offsetting \(only a certain number of records, starting from a certain position in the Dataset will be affected\)
* selecting the fields to be retrieved \(when the user does not want the entire record to be retrieved, only certain columns\)
* relations \(records from related datasets, as instructed, will also be affected by the request\)

All these features are handled server-side.

## Real-time communcation

The user can subscribe to events and will be notified in real time when those events are fired off on the server. Right now the events are only related to actions made on data. Subscription works on a per-dataset \(and schema\), per-action level.

**For example: adding records to the Posts dataset, or deleting records in the Users dataset.**



