# REST API

Package REST accepts any resources that implement `schema.Schema` interface.

### Accessing API

Client is required to supply authorization token in the headers for each request:

`Authorization: <token>`

Extra headers could be provided:

* `Content-Type`
  * `application/json`
    \(default\) or 
    `application/xml`
* `Accept`
  * `application/json`
    \(default\) or 
    `application/xml`

**Warning: This functionality is not completely implemented and tested. It is used only in purpose of testing.**

#### Content Negotiation \(server and client responsibilities\)

Server implements Restful service \(resource must implement **schema.Schema** interface\). Client and server communicate using JSON/XML messages. Client is allowed to use next HTTP request types:

* **GET**
  * retrieve a representation of a resource
* **POST**
  * create the specified resource
* **PUT**
  * update the full content of the specified resource.
* **DELETE**
  * delete the resource
* **OPTIONS**
  * some info about the communication

_Note: All operations are bulk, it means that we consider request/response as an array of records._

#### Compound Objects

Resources can have relations with other resources. This relations are expressed as compound object. Request with relations \(`GET`, `POST`, `PUT`, `DELETE`\) can process fields with relations:

```
[
    {
        ...,
        "<relation1>": [
        {
            ...,
            "<relation2>": [
                {
                    ...,
                    "<relationN>": [
                        ...
                    ]
                }
            ]
        }
    }
]
```

Relations will be binded to records if this is valid operation according to the resource schema.

ANEMO provides ability to SELECT/INSERT/UPDATE/DELETE related data/records \(with some limitations\):

[![](https://github.com/jexia-com/anemo/raw/v2/rest/images/relations.png "Relations")](https://github.com/jexia-com/anemo/blob/v2/rest/images/relations.png)

As you can see from the table above we prohibit modification of parent resources due to data consistency reasons. There are no limitations for **GET** method, for **HAS\_MANY** and **MANY\_TO\_MANY** relations as well.

**Important:**

* in case of update/delete data with 
  **MANY\_TO\_MANY**
   relations you cannot influence related data \(it works like 
  **attach/detach**
   and has effect only on pivot table\)
* when you update a record with 
  **MANY\_TO\_MANY**
   related data/records use an empty array to detach related records or omit related key to leave relations as is
* updating 
  **MANY\_TO\_MANY**
   relations all related records in pivot table are being deleted and created again, thus if you wish to attach new related record to existing ones you have to provide all the previous IDs \(otherwise all previous relations will be lost\)

#### Fields invisible for ANEMO

There could be system \(invisible\) columns. If you need to hide some logic on DB layer use prefix with underscore \(`_`\). For example: column `_user_id` will be loaded to application shcema but won't be visible and mutable trough the APIs.

### Fetching Resources

Resources can be fetched by identifier using GET request:

`[GET] http[s]://[anemo_ip]:[port]/rest/[resource_name]/[primary_key:OPTIONAL]`

Example:

`[GET] http://localhost:3000/rest/posts`

will return status code `[200] OK` and set of requested records as a response:

```
[
  {
    "id": "9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514",
    "user_id": "f18669ed-0c3b-4aaa-a3e0-f98930d568cb",
    "category_id": "199a7027-781c-48c4-ac82-5cdf22bb8c8c",
    "title": "My first post",
    "post": "I decided to write very good post, so I begin from this start point",
    "posted": true,
    "created_at": "2016-10-27T12:15:31Z",
    "updated_at": "2016-10-27T12:15:31Z"
  },
  {
    "id": "04bca006-cde8-47bc-a8eb-03c982e400de",
    "user_id": "f18669ed-0c3b-4aaa-a3e0-f98930d568cb",
    "category_id": "e837d481-8e35-411b-bc94-e61d84cb927b",
    "title": "My second post",
    "post": "This post will be draft for now. No one should see this.",
    "posted": false,
    "created_at": "2016-10-27T12:15:31Z",
    "updated_at": "2016-10-27T12:15:31Z"
  },
  {
    "id": "a0d140fb-4256-4018-8a26-97f87ad2173f",
    "user_id": "670b4aeb-e7dc-4a14-862f-89f354797abe",
    "category_id": null,
    "title": "How to get started to write a book",
    "post": "Sometime we decide to do something valuable...",
    "posted": true,
    "created_at": "2016-10-27T12:15:31Z",
    "updated_at": "2016-10-27T12:15:31Z"
  },
]
```

or by the primary key:

`[GET] http://localhost:3000/rest/posts/9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514`

```
[
  {
    "id": "9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514",
    "user_id": "f18669ed-0c3b-4aaa-a3e0-f98930d568cb",
    "category_id": "199a7027-781c-48c4-ac82-5cdf22bb8c8c",
    "title": "My first post",
    "post": "I decided to write very good post, so I begin from this start point",
    "posted": true,
    "created_at": "2016-10-27T12:15:31Z",
    "updated_at": "2016-10-27T12:15:31Z"
  }
]
```

### Fetching resources with relations

`[GET] http[s]://[anemo_ip]:[port]/rest/[resource_name]/[primary_key:OPTIONAL]/[relation_1]/[primary_key:OPTIONAL]/.../[relation_N]`

Example:

`[GET] http://localhost:3000/rest/posts/9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514/comments`

```
[
  {
    "id": "9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514",
    "user_id": "f18669ed-0c3b-4aaa-a3e0-f98930d568cb",
    "category_id": "199a7027-781c-48c4-ac82-5cdf22bb8c8c",
    "title": "My first post",
    "post": "I decided to write very good post, so I begin from this start point",
    "posted": true,
    "created_at": "2016-10-27T12:15:31Z",
    "updated_at": "2016-10-27T12:15:31Z",
    "comments": [
      {
        "id": "6df9cbc8-5ced-4411-96b8-25aa83378f29",
        "user_id": "670b4aeb-e7dc-4a14-862f-89f354797abe",
        "post_id": "9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514",
        "comment": "Good start!",
        "created_at": "2016-10-27T12:15:31Z",
        "updated_at": "2016-10-27T12:15:31Z"
      }
    ]
  }
]
```

with headers `Accept: application/xml`

```
<?xml version="1.0" encoding="UTF-8"?>
<posts>
    <record>
        <id>9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514</id>
        <user_id>f18669ed-0c3b-4aaa-a3e0-f98930d568cb</user_id>
        <category_id>199a7027-781c-48c4-ac82-5cdf22bb8c8c</category_id>
        <title>My first post</title>
        <post>I decided to write very good post, so I begin from this start point</post>
        <posted>true</posted>
        <created_at>2016-10-27T12:15:31Z</created_at>
        <updated_at>2016-10-27T12:15:31Z</updated_at>
        <comments>
            <record>
                <id>6df9cbc8-5ced-4411-96b8-25aa83378f29</id>
                <user_id>670b4aeb-e7dc-4a14-862f-89f354797abe</user_id>
                <post_id>9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514</post_id>
                <comment>Good start!</comment>
                <created_at>2016-10-27T12:15:31Z</created_at>
                <updated_at>2016-10-27T12:15:31Z</updated_at>
            </record>
        </comments>
    </record>
</posts>
```

_Note: JSON is default format, so it is not necessary set headers _`Accept`_ and _`Content-Type`_._

### Sorting

Sort field and sort order can be specified by `order` query parameter. It should be an array of json objects with properties `direction` and `fields`.

`[GET] /...?order=[{"direction":"asc|desc","fields":["field_one","field_two","field_N"]}]`

Example:

`[GET] http://localhost:3000/rest/posts?order=[{"direction":"desc","fields":["created_at"]},{"direction":"asc","fields":["title"]}]`

### Limit and Offset

`[GET] /...?range={"offset":<length:int>,"limit":<length:int>}`

Example:

`[GET] http://localhost:3000/rest/posts?range={"offset":10,"limit":5}`

### Fields

* You can specify the list of expected fields and their order:

`[GET] /...?fields=["field_one","field_two","field_N"]`

**Note:** array should contain at least one field, otherwise you'll get something like this:

```
{
    "errors": [
        "Nothing to return: Fields are not specified for query"
    ]
}
```

Example:

`[GET] http://localhost:3000/rest/posts/a0d140fb-4256-4018-8a26-97f87ad2173f?fields=["title","id"]`

Result:

```
[
    {
        "title": "How to get started to write a book",
        "id": "a0d140fb-4256-4018-8a26-97f87ad2173f"
    }
]
```

Getting the value of nested columns \(for JSON/JSONB only\):

`[GET] /...?fields=["field_one","json_field.nested_one","json_field[nested_two]"]`

You can see the difference in syntax from the example above \(`nested_one` and `nested_two`\): declaration of `json_field.nested_column` is equal to `json_field[nested_column]`.

**Note:** The level of nesting is not limited and it is possible to use array indexes as well \(if it is expected that nested value is an array\). For example: `some_field.some_nested.nested_array[0][1]`.

Example:

`[GET] http://localhost:3000/rest/profiles/46a8af84-fa98-4b60-aeb5-073029699973?fields=["id","email","permissions[r]","permissions.w"]`

Result:

```
[
    {
        "id": "46a8af84-fa98-4b60-aeb5-073029699973",
        "email": "first@example.com",
        "permissions.r": true,
        "permissions.w": true
    }
]
```

### Filtering

The result can be filtered by query conditions:

`[GET] /...?cond=[{"type":"<OPTIONAL:and|or>","field":"<REQUIRED>","operator":"<REQUIRED>","value":<OPTIONAL>,"values":[<OPTIONAL>]}]`

`"type"` - is an optional param. Could have values: `and` \(by default\), `or`.

`"field"`, `"operator"` and `"value"` \(or `"values"`\) should be url encoded to avoid of passing restricted symbols.

Allowed operators are:

* Equality operators\( `>`, `<`, `=`, `!=`, `>=`,`<=` \)

* Comparison with NULL \( `is null`, `is not null` \) - value\[s\] should be omitted - `...&cond[{"field":"some_field","operator":"is_null"}]` or `...&cond[{"field":"some_field","operator":"is_not_null"}]`

* Range operators \( `between`\) - range filtering, numbers and dates only

* Array operators \( `in`, `not_in` \) - filters from array of values. Applicable for text and for numbers as well

* Simple pattern matching \( `like` \)

* Regex operators \( `regexp`\) - regexp filtering.

Examples:

* find any post that has `category_id` or its ID equals `1`or `2`: `[GET] http://localhost:3000/rest/posts?cond=[{"field":"category_id","operator":"is_not_null"},{"type":"or","field":"id","operator":"in","values":["9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514","04bca006-cde8-47bc-a8eb-03c982e400de"]}]`
* find any profile where firstname starts with letter "A" and age &gt;`21`: `[GET] http://localhost:3000/rest/profiles?cond=[{"field":"firstname","operator":"regexp","value":"^M"},{"field":"age","operator":">","value":21}]`

### Create records

Create resource\(s\) \(Supports related fields\).

`[POST] http[s]://[anemo_ip]:[port]/rest/[resource_name]`

Example \(creating post with related comment using XML codec\):

`[POST] http://localhost:3000/rest/posts`

`Content-Type: application/xml`

```
<?xml version="1.0" encoding="UTF-8"?>
<posts>
    <record>
        <user_id>9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514</user_id>
        <title>Posted with XML</title>
        <post>XML is fast, cool and simple :)</post>
        <posted>true</posted>
        <comments>
            <record>
                <user_id>9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514</user_id>
                <comment>Yes! It is true!</comment>
            </record>
        </comments>
    </record>
</posts>
```

### Update records

Update full content. All required fields should be provided.

`[PUT] http[s]://[anemo_ip]:[port]/rest/[resource_name]`

`Content-Type: application/json[PUT] http://localhost:3000/rest/posts`

```
[
  {
    "id": "PUT_HERE_POST_ID",
    "title": "Updated with JSON",
    "post": "JSON is better :)",
    "comments": [
      {
        "id": "PUT_HERE_RELATED_COMMENT_ID",
        "comment": "Yes! I like JSON!"
      }
    ]
  }
]
```

```

```

### Delete records

`[DELETE] http[s]://[anemo_ip]:[port]/rest/[resource_name]/[primary_key:OPTIONAL]`

Examples:

* single delete by primary key

`[DELETE] http://localhost:3000/rest/posts/9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514`

* bulk delete

`[DELETE] http://localhost:3000/rest/posts`

```
[
  {
    "id": "04bca006-cde8-47bc-a8eb-03c982e400de"
  },
  {
    "id": "a0d140fb-4256-4018-8a26-97f87ad2173f"
  }
]
```

### Call stored procedures

In order to call remote procedures registered resource should implement **schema.Schema** interface and have registered action available by `Actions.Get(anemohttp.CALL)`.

Use `rest_info` described at the top of this document to obtain extended information about input and output arguments \(their names, types and returning values\).

_Note: If you are using ANEMO inside vagrant instance there should be preset of SQL functions for testing RPC module. Or you can create them manually. They are located in postgres folder _`anemo/schema/postgres/sql/sample_functions.sql`_._

Remote functions are called with `GET` method **ONLY**.

`[POST] http[s]://[anemo_ip]:[port]/rest/[procedure_name]?args={"arg_1":val_1,"arg_2":"val_2",...,"arg_N":val_N}&cond=...`

Examples:

#### Void functions

`[GET] http://localhost:3000/rest/test_void`

result:

```
[
  {
    "test_void": null
  }
]
```

#### Functions on base types

* get the sum of two integers:

`[GET] http://localhost:3000/rest/test_sum?args={"a":7,"b":8}`

result:

```
[
  {
    "test_sum": 15
  }
]
```

```

```

* join substrings

`[GET] http://localhost:3000/rest/test_text?args={"first":"Java","second":"Script"}`

result:

```
[
  {
    "test_text": "JavaScript"
  }
]
```

get current date and time

`[GET] http://localhost:3000/rest/test_date`

result:

```
[
  {
    "test_date": "2017-03-23T12:51:45.876741Z"
  }
]
```

functions returning value of table type \(for example

`[GET] http://localhost:3000/rest/search_single_post?args={"pattern":"first"}&fields=["id","title","post"]`

the result of remote procedure call is a single record from table posts \(found by posts.title\):

```
[
  {
    "id": "9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514",
    "title": "My first post",
    "post": "I decided to write very good post, so I begin from this start point"
  }
]
```

It is also possible to call functions returning a set of custom type values, or even apply relations to the result of function call:

`[GET] http://localhost:3000/rest/search_post/comments?args={"pattern":"My%25post"}`

In the example above we applied relation `comments` to the RPC result and got a set of posts matching the provided pattern.

```
[
  {
    "id": "9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514",
    "user_id": "f18669ed-0c3b-4aaa-a3e0-f98930d568cb",
    "category_id": "199a7027-781c-48c4-ac82-5cdf22bb8c8c",
    "title": "My first post",
    "post": "I decided to write very good post, so I begin from this start point",
    "posted": true,
    "created_at": "2017-01-23T11:03:01.608336Z",
    "updated_at": "2017-01-23T11:03:01.608336Z",
    "comments": [
      {
        "id": "6df9cbc8-5ced-4411-96b8-25aa83378f29",
        "user_id": "670b4aeb-e7dc-4a14-862f-89f354797abe",
        "post_id": "9e2eabf5-8a2b-4ffa-bb9f-566ab1e2b514",
        "comment": "Good start!",
        "created_at": "2017-01-23T11:03:01.608336Z",
        "updated_at": "2017-01-23T11:03:01.608336Z"
      }
    ]
  },
  {
    "id": "04bca006-cde8-47bc-a8eb-03c982e400de",
    "user_id": "f18669ed-0c3b-4aaa-a3e0-f98930d568cb",
    "category_id": "e837d481-8e35-411b-bc94-e61d84cb927b",
    "title": "My second post",
    "post": "This post will be draft for now. No one should see this.",
    "posted": false,
    "created_at": "2017-01-23T11:03:01.608336Z",
    "updated_at": "2017-01-23T11:03:01.608336Z",
    "comments": []
  }
]
```



