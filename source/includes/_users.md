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
    }
  ]
}
```

This endpoint retrieves a paged list of users.

### Request

`GET https://api.attensa.com/users`

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

See the [paging metadata specification](#Paging format) for more information on the `_paging` property

## Create a new user

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "firstName": "test",
       "middleName": "j",
       "lastName": "user",
       "suffix": "sr",
       "emailAddress": "foo@test.com",
       "timeZone": "Europe/Paris",
       "status": "ACTIVE"
     }' \
     https://api.attensa.net/users
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

This endpoint creates a new user.

### Request

`POST https://api.attensa.com/users`

### Response

Status code `201`

### JSON request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
firstName | First name | Yes | String | n/a
middleName | Middle name | No | String | `null`
lastName | Last name | Yes | String | n/a
suffix | Suffix (e.g. JR, SR) | No | String | `null`
emailAddress | Email Address (unique) | Yes | String in valid email format | n/a
timeZone | Supported time zone | Supported time zone string | `null`
status | User's status | Yes | ACTIVE, INVITED or INACTIVE | ACTIVE
