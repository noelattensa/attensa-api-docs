# Users

## Get a specific user

```shell
curl -u adam:password https://api.attensa.net/users/{userId}
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

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20
term | A search term to narrow the list of users returned | No | String | `null`
sort | Field to sort the results on | No | firstName, lastName or emailAddress | emailAddress
sortDirection | Sort ascending or descending | No | ASC or DESC | ASC

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

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

### Response

Status code `201`

## Update an existing user

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X PUT \
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

This endpoint updates an existing user.

### Request

`PUT https://api.attensa.com/users/{userId}`

### JSON request properties
No fields are required, but at least one must be provided for update. Updates are applied incrementally in a PATCH-like manner, so omitted fields will not be changed.

Parameter | Description | Required | Format
--------- | ----------- | -------- | ------
firstName | First name | No | String
middleName | Middle name | No | String
lastName | Last name | No | String
suffix | Suffix (e.g. JR, SR) | No | String
emailAddress | Email Address (unique) | Yes | String in valid email format
timeZone | Supported time zone | Supported time zone string
status | User's status | Yes | ACTIVE, INVITED or INACTIVE

### Response

Status code `200`

## Delete a user

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/users/{userId}
```

This endpoint deletes an existing user

### Request

`DELETE https://api.attensa.com/users/{userId}`

### Response

Status code `204`, empty body

## Get a list of streams a user follows

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     -d term=test \
     https://api.attensa.net/users/{userId}/streams
```

> The above command returns JSON structured like this:

```json
{
  "_paging": {
    "elementCount": 1,
    "page": 0,
    "pageCount": 1,
    "requestedPageSize": 20,
    "totalElementCount": 1
  },
  "streams": [
    {
      "id": "546e17fcd4c67da2547f5b61",
      "title": "Test Stream 01",
      "ownerId": "55414a36e4b0436b6280e668",
      "description" : "Description 01",
      "type": "RSS",
      "source": {
          "uri": "http://slashdot.org/rss"
      },
      "emailPostingEnabled": false,
      "openForReading": true,
      "openForPosting": false,
      "streamEmailAddress": "test.stream.01@email.attensa.net",
      "rssEnabled": false,
      "catgoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
      "itemsCount": 0,
      "followersCount": 0,
      "userIsFollowing": true,
      "userIsFollowingViaGroup": false,
      "userIsSubscribed": true,
      "userIsSubscribedViaGroup": false,
      "_links": {
            "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61"
        }
    }
  ]
}
```

This endpoint retrives a list of streams that a user is following

### Request

`GET https://api.attensa.com/users/{userId}/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20
term | A search term to narrow the list of streams returned | No | String | `null`


### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

Four properties are added to the normal stream objects returned in the `streams` array that specify the user's relationship with the stream:

* userIsFollowing
* userIsFollowingViaGroup
* userIsSubscribed
* userIsSubscribedViaGroup
