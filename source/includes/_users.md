# Users

## GET /users

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
    "page": 0
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
        "self": "https://api.attensa.net/users/546e17fcd4c67da2547f5b61"
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

## GET /users/{userId}

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
    "self": "https://api.attensa.net/users/546e17fcd4c67da2547f5b61"
  }
}
```

This endpoint retrieves a specific user.

### Request

`GET https://api.attensa.com/users/{userId}`

### Response

Status code `200`

## GET /users/{userId}/streams

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
      "published": true,
      "streamEmailAddress": "test.stream.01@email.attensa.net",
      "rssEnabled": false,
      "tagIds": ["54da78488ab02386a4658eee"],
      "catgoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
      "itemsCount": 0,
      "followersCount": 0,
      "userIsFollowing": true,
      "userIsFollowingViaGroup": false,
      "userIsSubscribed": true,
      "userIsSubscribedViaGroup": false,
      "_links": {
          "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
          "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
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

## GET /users/{userId}/briefings

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     https://api.attensa.net/users/{userId}/briefings
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
  "_links": {
    "first": "https://api.attensa.net/users/{userId}/briefings?rows=20&page=0",
    "last": "https://api.attensa.net/users/{userId}/briefings?rows=20&page=0"
  },
  "briefings": [
    {
      "subject": "My email subject line!",
      "description": "Some special message used by template.",
      "schedule": {
          "startDate": "2015-07-30",
          "stopDate": "2015-08-31",
          "sendHour": "15",
          "sendMinute": "30",
          "frequency": "WEEKLY",
          "interval": 1,
          "sendDays":["MO","TU", "WE", "TH", "FR"],
          "timeZone": "US/Pacific"
      },
      "templateId": "54b58250e4b0ec83add2661e",
      "stream": {
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
        "published": true,
        "streamEmailAddress": "test.stream.01@email.attensa.net",
        "rssEnabled": false,
        "tagIds": ["54da78488ab02386a4658eee"],
        "catgoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
        "itemsCount": 0,
        "followersCount": 0,
        "userIsFollowing": true,
        "userIsFollowingViaGroup": false,
        "userIsSubscribed": true,
        "userIsSubscribedViaGroup": false,
        "_links": {
          "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
          "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
        }
      }
    }
  ]
}
```

This endpoint retrives a list of briefings that a user is subscribed to

### Request

`GET https://api.attensa.com/users/{userId}/briefings`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20


### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

Four properties are added to the normal stream objects returned in briefings array that specify the user's relationship with the stream:

* userIsFollowing
* userIsFollowingViaGroup
* userIsSubscribed
* userIsSubscribedViaGroup

## POST /users

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
    "self": "https://api.attensa.net/users/546e17fcd4c67da2547f5b61"
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
timeZone | Supported time zone | [Supported time zone string](#time-zones) | `null`
status | User's status | Yes | ACTIVE, INVITED or INACTIVE | ACTIVE

### Response

Status code `201`

## POST /users/{userId}/streams

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "streamId": "546e17fcd4c67da2547f5b61",
       "subscribeToBriefing": true,
     }' \
     https://api.attensa.net/users/{userId}/streams
```

Have a user follow a stream and optionally subscribe to the streams briefing.

### Request

`POST https://api.attensa.com/users/{userId}/streams`

### Request body parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
streamId | The stream for the user to follow | Yes | String | n/a
subscribeToBriefing | Subscribe the user to the briefing | No | Boolean | `false`

### Response

Status code `204` with empty body

## PUT /users/{userId}

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
    "self": "https://api.attensa.net/users/546e17fcd4c67da2547f5b61"
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

## DELETE /user/{userId}

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
