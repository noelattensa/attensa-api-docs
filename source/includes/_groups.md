# Groups

## GET /groups

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     -d term=test \
     https://api.attensa.net/groups
```
> Status code 200 with response as follows:

```json
{
  "_paging": {
    "totalElementCount": 1,
    "pageCount": 1,
    "requestedPageSize": 20,
    "elementCount": 1,
    "page": 0
  },
  "groups": [
    {
      "creatorId": "56161che546097aa51621b47",
      "description": "foo",
      "name": "test",
      "streamCount": 5,
      "userCount": 192,
      "_links": {
          "self": "http://api.attensa.net/groups/55161cf7e4b097aa51621b47"
      }
    }
  ]
}
```

Get a paged list of groups.

### Request

`GET https://api.attensa.net/groups`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20
term | A search term to narrow the list of groups returned | No | String | `null`

### Response

Status code `200`

## GET /groups/{groupId}

```shell
curl -u username:password https://api.attensa.net/groups/{groupId}
```
> Status code 200 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "foo",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 5,
  "userCount": 2,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

This endpoint retrieves information about a specific group

### Request

`GET https://api.attensa.net/groups/{groupsId}`

### Response

Status code `200`

## GET /groups/{groupId}/users

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     -d sort=firstName
     -d sortDirection=ASC
     -d term=test \
     https://api.attensa.net/groups/{groupId}/users
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "totalElementCount": 1,
    "pageCount": 1,
    "requestedPageSize": 20,
    "elementCount": 1,
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
        "self": "http://api.attensa.net/users/546e17fcd4c67da2547f5b61"
      }
    }
  ]
}
```

This endpoint retrieves a paged list of users in a certain group.

### Request

`GET https://api.attensa.com/users`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20
term | A search term to narrow the list of users returned | No | String | `null`
sort | Field to sort the results on | No | `firstName`, `lastName`, `emailAddress`, `status` | emailAddress
sortDirection | Sort ascending or descending | No | ASC or DESC | ASC

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /groups/{groupId}/streams

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     -d term=test \
     https://api.attensa.net/groups/{groupId}/streams
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "totalElementCount": 1,
    "pageCount": 1,
    "requestedPageSize": 20,
    "elementCount": 1,
    "page": 0
  },
  "streams": [{
    "title": "Test Stream 01",
    "groupIsSubscribed": true,
    "description": "Description 01",
    "ownerId": "55414a36e4b0436b6280e668",
    "type": "COLLECTION",
    "emailPostingEnabled": true,
    "openForReading": true,
    "openForPosting": true,
    "streamEmailAddress": "test.stream.01@email.attensa.net",
    "rssEnabled": false,
    "categoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"]
  }]
}
```

This endpoint retrieves a paged list of streams that a group follows.

### Request

`GET https://api.attensa.com/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of streams in each page | No | Integer | 20
term | A search term to narrow the list of streams returned | No | String | `null`

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

<aside class="notice">The stream objects in the stream array will include a groupIsSubscribed property that specifies whether the group is subscribed to the stream's briefing in addition to following it.</aside>

## GET /groups/{groupId}/briefings

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     https://api.attensa.net/groups/{groupId}/briefings
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
        "groupIsSubscribed": true,
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
        "_links": {
            "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61"
        }
      }
    }
  ]
}
```

This endpoint retrives a list of briefings that a user is subscribed to

### Request

`GET https://api.attensa.com/groups/{groupId}/briefings`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of briefings in each page | No | Integer | 20


### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## POST /groups

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "creatorId": "56161che546097aa51621b47"
       "description": "just a test group",
       "name": "test"
     }' \
     https://api.attensa.net/groups
```
> Status code 201 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "just a test group",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 0,
  "userCount": 0,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

Create a new group.

### Request

`POST https://api.attensa.net/groups`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
creatorId | Id of the user that should be marked as creator | Yes | String | n/a
description | Description of the group | Yes | String | n/a
name | Name of the group | Yes | String | n/a

### Response

Status code `201`

## POST /groups/{groupId}/users

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "id": "56161che546097aa51621b47"
     }' \
     https://api.attensa.net/groups/users
```
> Status code 201 with response as follows:

```json
{
  "id": "56161che546097aa51621b47"
}
```

Add a user to a group

### Request

`POST https://api.attensa.net/groups/users`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
id | Id of the user that should be added to the group | Yes | String | n/a

### Response

Status code `201`

## POST /groups/{groupId}/streams

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "streamId": "559bf709e4b008a9a53293c3",
       "subscribeToBriefing": true,
     }' \
     https://api.attensa.net/groups/{groupId}/streams
```
> Status code 204 with empty body

Set a grop to follow a stream and optionally subscribe to it's briefing

### Request

`POST https://api.attensa.net/groups/{groupId}/streams`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
streamId | Id of the stream to follow | Yes | String | n/a
subscribeToBriefing | subscribe the group to the streams briefing | No | Boolean | false

### Response

Status code `204`

## PUT /groups/{groupId}

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X PUT \
     -d '{
       "creatorId": "56161che546097aa51621b47"
       "description": "just a test group",
       "name": "test"
     }' \
     https://api.attensa.net/groups/{groupId}
```
> Status code 200 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "just a test group",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 0,
  "userCount": 0,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

Update an existing group.  Updates are applied in a incremental PATCH-like manner, so the entire group resource does not need to be supplied, only the properties that are changing.

### Request

`PUT https://api.attensa.net/groups`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
creatorId | Id of the user that should be marked as creator | No | String | n/a
description | Description of the group | No | String | n/a
name | Name of the group | No | String | n/a

### Response

Status code `200`

## DELETE /groups/{groupId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/groups/{groupId}
```
> 204 empty body returned on success

Delete an existing group from the system.  All users will be un-followed and un-subscribed from streams they followed or subscribed to via this group.

<aside class="warning">Use this endpoint with care!  There is no way to undo this action from the API</aside>

### Request

`DELETE https://api.attensa.net/groups/{groupId}`

### Response

Status code `204` with empty body

## DELETE /groups/{groupId}/users/{userId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/groups/{groupId}/users/{userId}
```
> 204 empty body returned on success

Remove a user from a group

### Request

`DELETE https://api.attensa.net/groups/{groupId}/users/{userId}`

### Response

Status code `204` with empty body