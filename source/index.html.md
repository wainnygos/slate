---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - http

toc_footers:
  - <a href='https://app.swaggerhub.com/apis-docs/globaloffice/juvonno/2.0.1#/'>Swaggerhub's API Reference</a>

includes:
  - errors

search: true
---

# Getting Started
## Introduction

Juvonno API is a collection of RESTful endpoints, which communicate directly with our back-end Business Objects, thus allowing users to Create, Read, Update & Delete (CRUD) the corresponding resources. 

Juvonno API has strict validations and will throw detailed messages upon encountering any errors, thus enabling developers with better integration to our Juvonno App. 

<aside class="warning">
This guide is currently in development.
</aside>

## API Reference

This document will serve as a guideline & an introduction to our Juvonno API & our business logic.

For detailed API Document of all of our available Endpoints, please use this [reference here in Swaggerhub](https://app.swaggerhub.com/apis-docs/globaloffice/juvonno/2.0.1). 

## What is a REST API?

API stands for "Application Programming Interface". It's a set of rules that enables various programs to talk to each other, regardless of the programming languages they were written in.

The programs talk to each other through a set of predefined URLs which can be accessed via HTTP Protocol.

These URLs represent various **resources**. A Resource represents a **Juvonno Business Object**, such as an **Appointment**, a **Customer**, or a **Staff Member**, etc. Resources will be returned in JSON format.

We utilize various HTTP Methods to perform different operations on a resource:

    - GET: to retrieve a resource (or sometimes a list of resources)
    - POST: to create a new resource 
    - PUT: to update an existing resource
    - DELETE: to delete an existing resource    

## Authentication

Juvonno uses API keys to allow access to the API. You can register a new API key under your own profile in your Juvonno App.

> Always append your api key using the query parameter "api_key" to your HTTP Request:

```shell
curl -X POST "https://tenant-id.juvonno.com/
api/{RESOURCES}?api_key={YOUR_API_KEY}"
```

```http
POST "https://tenant-id.juvonno.com/api/{RESOURCES}?api_key={YOUR_API_KEY}"
```

API key must be included in all API requests to the server as a *query parameter* called **"api_key"** that looks like the following:

`https://tenant-id.juvonno.com/api/{RESOURCES}?api_key=fhOkwr12kfslsdqwe8`

<aside class="notice">
You must replace <code>fhOkwr12kfslsdqwe8</code> with your personal API key.
</aside>


# Juvonno Resources

Each Resource represents an actual Juvonno Business Object, which can be accessed through a collection of URLs.

For example, /api/customers is the URL responsible for all operations on the "Customer Resource", which in turn is a "Customer Object" in our backend server.

Each object / resource will always have a unique **Juvonno ID**. It is up to users to choose to store our IDs into their application.  

> An example Customer Resource:

```json
{
  "customer": {
    "id": 21,
    "num": {
      "chart": "CHART1234"
    },
    "first_name": "John",
    "last_name": "Doe"
  }
}
```
Sometimes we also allow an additional field which users can use to match up against their own IDs in their system. 
For example, the Customer Resource on the right has a **Juvonno ID** of **21** and an additional identifier **chart > num** of **"CHART1234"** (which can represent the Customer's ID in your system).

It is not always the case that we provide an additional mapping field. One example is the "Appointment" Resource. "Appointment" does not have a "number" or a "name". The only way to distinguish between unique appointments in Juvonno is based on theirs Juvonno ID.
Hence in some cases it relies totally on the Juvonno ID in order for a resource to be able to get retrieved or modified. Therefore, though it is not mandatory, but we do **recommend storing this ID field into your own system**.


# CRUD Operations

We follow standard RESTful CRUD operations. There will be a corresponding   
  `/api/ { RESOURCES - NAME }`   
collection of CRUD operations per Juvonno Object.
<aside class="notice">
CRUD stands for "Create", "Retrieve", "Update" and "Delete"
</aside>

## Create a new Resource

Always use **POST** to create a new resource.

`POST https://tenant-id.juvonno.com/api/{RESOURCES}/`

> Create a new Customer: 

```http
POST https://tenant-id.juvonno.com/api/customers?api_key={YOUR_API_KEY}
```

```shell 
cURL -X POST "https://tenant-id.juvonno.com/api/customers
?api_key={YOUR_API_KEY}"
```

> Example Request Body

```json
{
  "chart_num": "CHART1234",
  "first_name": "John",
  "last_name": "Doe"
}
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.

### Request Body
- application/json
- application/x-www-form-urlencoded


## Retrieve an existing Resource

Always use **GET** to retrieve a resource.

`GET https://tenant-id.juvonno.com/api/{RESOURCES}/{RESOURCE_JUVONNO_ID}`

> Get a customer who has a Juvonno ID of 21: 

```http
GET https://tenant-id.juvonno.com/api/customers/21?api_key={YOUR_API_KEY}
```

```shell 
cURL -X GET "https://tenant-id.juvonno.com/api/customers/21
?api_key={YOUR_API_KEY}"
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.


## Update an existing Resource

Always use **PUT** to update an existing resource.

`PUT https://tenant-id.juvonno.com/api/{RESOURCES}/{RESOURCE_JUVONNO_ID}`

> Update a customer who has a Juvonno ID of 21 with new phone number: 

```http
PUT https://tenant-id.juvonno.com/api/customers/21?api_key={YOUR_API_KEY}
```

```shell 
cURL -X PUT "https://tenant-id.juvonno.com/api/customers/21
?api_key={YOUR_API_KEY}"
```

> Request Body

```json
{
  "phone": "1-431-123-1234"
}
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.

### Request Body
- application/json
- application/x-www-form-urlencoded


## Delete an existing Resource

Always use **DELETE** to delete a resource.

`DELETE https://tenant-id.juvonno.com/api/{RESOURCES}/{RESOURCE_JUVONNO_ID}`

> Delete a customer who has a Juvonno ID of 21: 

```http
DELETE https://tenant-id.juvonno.com/api/customers/21?api_key={YOUR_API_KEY}
```

```shell 
cURL -X DELETE "https://tenant-id.juvonno.com/api/customers/21
?api_key={YOUR_API_KEY}"
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.

## Flexible Parameters

Sometimes an object can be accessed using different identifiers, Juvonno API provides the users with the flexibility of using other identifiers besides our main **"Juvonno ID"** to perform operations on the resource.

**Example Scenario:**

You want to create a new Staff and assign your staff to a clinic location called "Brandon Clinic".

A Clinic is represented by a "Branch Resource" in our API. A Branch can be identified by either its:

- Branch's Juvonno ID
- Branch's code
- Branch's name

In the request body, you can supply either parameter "branch_id", "branch_code" or "branch_name". Juvonno will try to map the branch to the staff based on the parameter your provided. Only one parameter needs to be supplied, although you can supply as many as you wish.

In case you have supplied more than one parameter (for example “branch_id” and “branch_name”), and if Juvonno has found a match with the first parameter, it will ignore and won’t map the second parameter provided. Mapping priority is in this exact order:  

`Branch_id  > Branch_code > Branch_name`

If your application has two branches with the same name “Brandon Clinic”, Juvonno API will return an Error with a detailed message asking you to supply a unique "branch_name" or use "branch_id" (Juvonno ID) instead. 

If your application has no branches with the name “Brandon Clinic”, Juvonno API will return an Error telling you that it was unable to find any record with such name. 


# Customers

**Endpoint:**

`/api/customers`

A Customer represents a "Patient". You can create a new customer, retrieve or modify an existing customer using its **Juvonno ID** or its **Chart Num**. 

Only **Juvonno ID** is treated as a unique identifier in our system. If you're querying using **Chart Num**, you must supply a unique existing number or else the program will throw corresponding error codes. 

## Create a new Customer

### HTTP Request

`POST https://tenant-id.juvonno.com/api/customers`

> Create a new Customer: 

```http
POST https://tenant-id.juvonno.com/api/customers?api_key={YOUR_API_KEY}
```

```shell 
cURL -X POST "https://tenant-id.juvonno.com/api/customers
?api_key={YOUR_API_KEY}"
```

> Example Request Body

```json
{
  "chart_num": "CHART1234",
  "first_name": "John",
  "last_name": "Doe",
  "date_of_birth": "1989-12-01",
  "gender": "male"   
}
```

> Example Response:

```json
{
  "customer": {
    "id": 1,
    "num": {
      "chart": "CHART1234"     
    },
    "first_name": "John",
    "last_name": "Doe",
    "gender": "male",
    "date_of_birth": "1989-12-01",
    "status": "active"                 
  }
}
```

This endpoint creates a new customer.

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.

### Request Body

- application/json
- application/x-www-form-urlencoded

Parameter | Required | Description
--------- | -------- | -----------
first_name | Y | Customer's first name
last_name | Y | Customer's last name
date_of_birth | Y | Customer's DOB
gender | Y | Must be one of "male", "female", "private" or "unknown"
chart_num | N | This can be used to match against your own customer's ID
preferred_language | N | Must be one of "english" or "french"
status | N | Must be one of "active", "inactive", "discharged" or "deleted"
branch_id | N | You can use either "branch_id", "branch_code" or "branch_name" 
branch_code | N | You can use either "branch_id", "branch_code" or "branch_name" 
branch_name | N | You can use either "branch_id", "branch_code" or "branch_name" 


## Retrieve a Customer using Juvonno ID

### HTTP Request

`GET https://tenant-id.juvonno.com/api/customers/{customerId}`

> Retrieve a customer who has a Juvonno ID of 21: 

```http
GET https://tenant-id.juvonno.com/api/customers/21?api_key={YOUR_API_KEY}
```

```shell 
cURL -X GET "https://tenant-id.juvonno.com/api/customers/21
?api_key={YOUR_API_KEY}"
```

> Example Response:

```json
{
  "customer": {
    "id": 21,
    "num": {
      "chart": "CHART1234"     
    },
    "first_name": "John",
    "last_name": "Doe",
    "gender": "male",
    "date_of_birth": "1989-12-01",
    "status": "active"                 
  }
}
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.


### URL Parameters

Parameter | Description
--------- | -----------
customerID | The Juvonno ID of the customer to be retrieved


## Retrieve a Customer using Chart Num

### HTTP Request

`GET https://tenant-id.juvonno.com/api/customers/chart/{number}`

> Retrieve a customer who has a Chart Num of "CHART1234": 

```http
GET https://tenant-id.juvonno.com/api/customers/chart/CHART1234?api_key={YOUR_API_KEY}
```

```shell 
cURL -X GET "https://tenant-id.juvonno.com/api/customers/chart/CHART1234
?api_key={YOUR_API_KEY}"
```

> Example Response:

```json
{
  "customer": {
    "id": 21,
    "num": {
      "chart": "CHART1234"     
    },
    "first_name": "John",
    "last_name": "Doe",
    "gender": "male",
    "date_of_birth": "1989-12-01",
    "status": "active"                 
  }
}
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.


### URL Parameters

Parameter | Description
--------- | -----------
number | The chart number of the customer to be retrieved
