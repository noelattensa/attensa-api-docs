---
title: Attensa API Reference

toc_footers:
  - <a href='http://attensa.com/contact-us/'>Contact us about getting a developer account</a>

search: true
---

# Introduction

Welcome to the Attensa API!

# Authentication

> To authorize, pass your username and password using basic auth:

```shell
curl -u username:password http://api.attensa.net/endpoint
```

Attensa uses [HTTP basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication).  You can obtain a username and password by contacting us [here](http://attensa.com/contact-us/)

# Users

## Get a specific user

```shell
curl -u adam:password https://api.attensa.net/users/userId
```

> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "firstName": "test",
  "middleName": "j",
  "lastName": "user",
  "suffix": "sr",
  "emailAddress": "foo@test.com",
  "timeZone": "Europe/Paris",
  "status": "ACTIVE",
  "_links": {
    "self": "http://api.attensa.net/users/546e17fcd4c67da2547f5b61"
  }
}
```

This endpoint retrieves a specific user.

### Request

`GET http://api.attensa.com/users/{userId}`

### Response

Status code `200`

<aside class="notice">
* timeZone will be one of the supported time zones specified here
* status will be one of ACTIVE, INVITED or INACTIVE
</aside>

## Get a list of users

```shell
curl -u adam:password https://localhost:8000/users
```

> The above command returns JSON structured like this:

```json
{
  "_paging": {
    "totalElementCount": 42,
    "pageCount": 3,
    "requestedPageSize": 20,
    "elementCount": 20,
    "page": 0,
  },
  "users": [
    {
    "id": "546e17fcd4c67da2547f5b61",
    "firstName": "test",
    "middleName": "j",
    "lastName": "user",
    "suffix": "sr",
    "emailAddress": "foo@test.com",
    "timeZone": "Europe/Paris",
    "status": "ACTIVE",
    "_links": {
      "self": "http://api.attensa.net/users/546e17fcd4c67da2547f5b61"
    }
  ]
}
```

This endpoint retrieves a paged list of users.

### Request

`GET http://api.attensa.com/users`

### Response

Status code `200`

### Query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20
term | A search term to narrow the list of users returned | No | String | `null`
sort | Field to sort the results on | No | firstName, lastName or emailAddress | emailAddress
sortDirection | Sort ascending or descending | No | ASC or DESC | ASC

<aside class="info">See the paging metadata specification for more information on the `_paging` property</aside>

