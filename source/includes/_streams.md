# Streams

## Get a specific stream

```shell
curl -u username:password https://api.attensa.net/streams/{streamId}
```
> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "title": "Test Stream 01",
  "ownerId": "55414a36e4b0436b6280e668",
  "description" : "Description 01",
  "type": "COLLECTION",
  "source": {
      "search": "search term",
      "uri": "http://slashdot.org/rss",
      "username": "myUserNameForSecuredRSSFeed"
  },
  "emailPostingEnabled": false,
  "openForReading": true,
  "openForPosting": true,
  "streamEmailAddress": "test.stream.01@email.attensa.net",
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
  "itemsCount": 0,
  "followersCount": 0,
  "_links": {
        "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61"
    }
}
```

This endpoint retrieves a specific stream

### Request

`GET https://api.attensa.net/streams/{streamId}`

### Response

Status code `200`

## Create a new stream

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "title": "Test Stream 01",
       "description": "Description 01",
       "ownerId": "55414a36e4b0436b6280e668",
       "type": "RSS",
       "source": {
           "uri": "http://slashdot.org/rss",
           "username": "myUserNameForSecuredRSSFeed",
           "password": "myPasswordForSecuredRSSFeed",
       },
       "emailPostingEnabled": false,
       "openForReading": true,
       "openForPosting": true,
       "rssEnabled": false,
       "categoryIds" : ["55414a36e4b0436b6280e668"]
     }' \
     https://api.attensa.net/streams
```
> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "title": "Test Stream 01",
  "ownerId": "55414a36e4b0436b6280e668",
  "description" : "Description 01",
  "type": "RSS",
  "source": {
      "uri": "http://slashdot.org/rss",
      "username": "myUserNameForSecuredRSSFeed"
  },
  "emailPostingEnabled": false,
  "streamEmailAddress": "test.stream.01@email.attensa.net",
  "openForReading": true,
  "openForPosting": true,
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668"],
  "itemsCount": 0,
  "followersCount": 0,
  "_links": {
        "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61"
    }
}
```

### Request

`POST https://api.attensa.net/streams`

### JSON request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
title | Stream Title | Yes | String | n/a
description | Stream description | No | String | `null`
ownerId | User id of stream owner | Yes | String of valid user id | n/a
type | Stream type | Yes | COLLECTION, RSS | n/a
source:uri | Uri of rss feed. Only supply for type RSS streams | For type RSS | String | `null`
source:username | Basic auth username for secured rss feed. Only supply for type RSS streams. | For secured RSS streams | String | `null`
source:password | Basic auth password for secured rss feed. Only supply for type RSS streams. | For secured RSS streams | String | `null`
emailPostingEnabled | Allow posting to COLLECTION stream via email. | No | Boolean | false
streamEmailAddress | Email address to for stream if emailPosting is enabled. Only set for collection streams | No | Valid email string | `null`
openForReading | Allow all users to read this stream | No | boolean | false
openForPosting | Allow all users to post content to a COLLECTION stream | No | boolean | false
rssEnabled | Allow public access to an RSS feed of this stream | No | boolean | false
categoryIds | Categories to put the stream in | Yes (empy array for no categories) | [String] | []


### Response

Status code `201`

## PUT /streams/{streamId}

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "title": "Test Stream 01",
       "description": "Description 01",
       "ownerId": "55414a36e4b0436b6280e668",
       "source": {
           "uri": "http://slashdot.org/rss",
           "username": "myUserNameForSecuredRSSFeed",
           "password": "myPasswordForSecuredRSSFeed",
       },
       "emailPostingEnabled": false,
       "streamEmailAddress": "test.stream.01@email.attensa.net",
       "openForReading": true,
       "openForPosting": true,
       "rssEnabled": false,
       "categoryIds" : ["55414a36e4b0436b6280e668"]
     }' \
     https://api.attensa.net/streams/{streamId}
```
> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "title": "Test Stream 01",
  "ownerId": "55414a36e4b0436b6280e668",
  "description" : "Description 01",
  "type": "RSS",
  "source": {
      "uri": "http://slashdot.org/rss",
      "username": "myUserNameForSecuredRSSFeed"
  },
  "emailPostingEnabled": false,
  "openForReading": true,
  "openForPosting": true,
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668"],
  "itemsCount": 0,
  "followersCount": 0,
  "_links": {
        "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61"
    }
}
```

Update an existing stream.  Updated are applied in a incremental PATCH-like manner, so the entire stream resource does not need to be supplied, only the properties that are changing.

### Request

`PUT https://api.attensa.net/streams/{streamId}`

### JSON body request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
title | Stream Title | No | String | n/a
description | Stream description | No | String | n/a
ownerId | User id of stream owner | No | String of valid user id | n/a
source:uri | Uri of rss feed. Only supply for type RSS streams | No | String | n/a
source:username | Basic auth username for secured rss feed. Only supply for type RSS streams. | No | String | n/a
source:password | Basic auth password for secured rss feed. Only supply for type RSS streams. | No | String | n/a
emailPostingEnabled | Allow posting to COLLECTION stream via email. | No | Boolean | n/a
streamEmailAddress | Email address to for stream if emailPosting is enabled. Only set for collection streams | No | Valid email string | n/a
openForReading | Allow all users to read this stream | No | Boolean | n/a
openForPosting | Allow all users to post content to a COLLECTION stream | No | Boolean | n/a
rssEnabled | Allow public access to an RSS feed of this stream | No | Boolean | n/a
categoryIds | Categories to put the stream in | No | [String] | n/a

<aside class="notice">Stream type can not be updated.  Once a stream is created it's type is immutable.</aside>
<aside class="notice">All categories can be removed by sending an empty category array (<code>"categories": []</code>)</aside>
<aside class="notice">If updating a secured source, all source fields must be sent (uri, username and password). If no username or password is supplied, but a source uri is, then any existing credentials will be removed.</aside>

### Response

Status code `200`

## DELETE /streams/{streamId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/streams/{streamId}
```
> 204 emtpy body returned on success

Delete an existing stream from the system.  All users will be un-followed and un-subscribed from the stream when it is deleted.

<aside class="warning">Use this endpoint with care!  There is no way to undo this action from the API</aside>

### Request

`DELETE https://api.attensa.net/streams/{streamId}`

### Response

Status code `204` with empty body

## GET /streams/{streamId}/briefing

```shell
curl -u username:password https://api.attensa.net/streams/{streamId}/briefing
```
> Status code 200 with json structured as follows:

```json
{
  "description": "javascript news",
  "templateId": "54eba226e4b050dd8b9c1099",
  "title": "DailyJS",
  "schedule": {
    "frequency": "DAILY",
    "interval": 2,
    "sendHour": 10,
    "sendMinute": 40,
    "startDate": "2015-08-08",
    "timeZone": "US/Pacific"
  },
  "stream": {
    "categoryIds": ["54eba224e4b050dd8b9c1096"],
    "emailPostingEnabled": false,
    "id": "5519ae56e4b0c0419a88bae1",
    "numberOfFollowers": 0,
    "numberOfItems": 111,
    "openForPosting": false,
    "openForReading": true,
    "ownerId": "54da7849e4b02386a4658e5d",
    "rssEnabled": true,
    "source": {
        "uri": "http://feeds.feedburner.com/dailyjs"
    },
    "title": "DailyJS",
    "type": "RSS",
    "_links": {
        "self": "http://localhost:8000/streams/5519ae56e4b0c0419a88bae1"
    }
  }
}
```

Get briefing information for a specific stream

### Request

`GET https://api.attensa.net/streams/{streamId}/briefing`

### Response

Status code `200`
