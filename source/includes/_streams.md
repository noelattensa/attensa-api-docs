# Streams

## Stream Types

Attensa supports the following stream types

Type | Description | Can create | Can search
--------- | ----------- | -------- | ------ | -------
ATTENSA_SEARCH | Composed based on a search of items in other streams in Attensa | Yes | Yes
BING_SEARCH | Bing search results for either web or news search | Yes | Yes
CLINICALTRIALS_SEARCH | Content from clinicaltrials.gov | Yes | Yes
COLLECTION | A combination stream composed of items from other streams | Yes | Yes
FACTIVA_SELECT_HTTP | Content from a Factiva Select feed | No | Yes
PUBMED_SEARCH | Content from PubMed | Yes | Yes
RSS | Content from an RSS feed | Yes | Yes
TWITTER_SEARCH | Content based on a twitter search | Yes | Yes

## GET /streams

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d published=true \
     -d rows=20 \
     -d term=test \
     -d type=COLLECTION \
     https://api.attensa.net/streams
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
  "_links": {
    "first": "https://api.attensa.net/streams?rows=20&page=0&term=test&type=COLLECTION&published=true",
    "last": "https://api.attensa.net/streams?rows=20&page=0&term=test&type=COLLECTION&published=true"
  },
  "streams": [{
    "id": "546e17fcd4c67da2547f5b61",
    "title": "Test Stream 01",
    "groupIsSubscribed": true,
    "description": "Description 01",
    "ownerId": "55414a36e4b0436b6280e668",
    "type": "COLLECTION",
    "emailPostingEnabled": true,
    "openForReading": true,
    "openForPosting": true,
    "published": true,
    "streamEmailAddress": "test.stream.01@email.attensa.net",
    "rssEnabled": false,
    "categoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
    "tagIds": ["54da78488ab02386a4658eee"],
    "substreams": [
      {
          "id": "559c1972e4b008b9a5329478",
          "title": "Hi, I am a substream!",
          "type": "RSS"
      }
    ],
    "_links": {
      "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
      "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
    }
  }]
}
```

Get a paged list of streams.

### Request

`GET https://api.attensa.com/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
published | Filter stream list to published or unpublished streams. Omit for all streams. | No | Boolean | `null`
rows | Number of streams in each page | No | Integer | 20
source.search | Term used for search based stream types (TWITTER_SEARCH, etc) | No | String | `null`
source.uri | Uri of RSS feed for RSS streams | No | String | `null`
term | A search term to narrow the list of streams returned | No | String | `null`
type | Filter results to a specific stream type | No | [searchable stream type](#stream-types) | `null`

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /streams/{streamId}

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
  "published": true,
  "streamEmailAddress": "test.stream.01@email.attensa.net",
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
  "itemsCount": 0,
  "followersCount": 0,
  "tagIds": ["54da78488ab02386a4658eee"],
  "substreams": [
    {
        "id": "559c1972e4b008b9a5329478",
        "title": "Hi, I am a substream!",
        "type": "RSS"
    }
  ],
  "_links": {
    "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
    "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
  }
}
```

This endpoint retrieves a specific stream

### Request

`GET https://api.attensa.net/streams/{streamId}`

### Response

Status code `200`

## GET /streams/{streamId}/briefing

```shell
curl -u username:password https://api.attensa.net/streams/{streamId}/briefing
```
> Status code 200 with json structured as follows:

```json
{
  "description": "javascript news",
  "templateId": "54eba226e4b050dd8b9c1099",
  "subject": "DailyJS",
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
    "followersCount": 0,
    "itemsCount": 111,
    "openForPosting": false,
    "openForReading": true,
    "ownerId": "54da7849e4b02386a4658e5d",
    "published": true,
    "rssEnabled": true,
    "source": {
        "uri": "http://feeds.feedburner.com/dailyjs"
    },
    "tagIds": ["54da78488ab02386a4658eee"],
    "title": "DailyJS",
    "type": "RSS",
    "_links": {
      "self": "https://api.attensa.net/streams/5519ae56e4b0c0419a88bae1",
      "owner": "https://api.attensa.net/users/54da7849e4b02386a4658e5d"
    }
  }
}
```

Get briefing information for a specific stream

### Request

`GET https://api.attensa.net/streams/{streamId}/briefing`

### Response

Status code `200`

## GET /streams/{streamId}/users

```shell
curl -u username:password https://api.attensa.net/streams/{streamId}/users
```
> Status code 200 with json structured as follows:

```json
{
  "_links": {
    "first": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/users?page=0",
    "last": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/users?page=1",
    "next": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/users?page=1"
  },
  "_paging": {
    "elementCount": 20,
    "page": 0,
    "pageCount": 2,
    "requestedPageSize": 20,
    "totalElementCount": 34
  },
  "users": [
    {
      "_links": {
        "self": "https://pi.attensa.net/users/5421903ae4b0fd12d843a219"
      },
      "emailAddress": "test@attensa.com",
      "firstName": "Adam",
      "id": "5421903ae4b0fd12d843a219",
      "lastName": "Test",
      "middleName": "J",
      "status": "ACTIVE",
      "suffix": "SR",
      "timeZone": "US/Pacific",
      "userIsFollowing": false,
      "userIsFollowingViaGroup": true,
      "userIsSubscribed": false,
      "userIsSubscribedViaGroup": false
    }
  ]
}
```

Get users that are following/subscribed to a specific stream

### Request

`GET https://api.attensa.net/streams/{streamId}/users`

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

## POST /streams

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
           "password": "myPasswordForSecuredRSSFeed"
       },
       "emailPostingEnabled": false,
       "openForReading": true,
       "rssEnabled": false,
       "tagIds": ["54da78488ab02386a4658eee"],
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
  "published": true,
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668"],
  "tagIds": ["54da78488ab02386a4658eee"],
  "itemsCount": 0,
  "followersCount": 0,
  "_links": {
    "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
    "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
  }
}
```

Create a new stream

### Request

`POST https://api.attensa.net/streams`

### JSON request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
title | Stream Title | Yes | String | n/a
description | Stream description | No | String | `null`
ownerId | User id of stream owner | Yes | String of valid user id | n/a
type | Stream type | Yes | [creatable stream type](#stream-types) | n/a
source:search | Search term. Only supply for ATTENSA_SEARCH, PUBMED_SEARCH or TWITTER_SEARCH streams | For type ATTENSA_SEARCH, PUBMED_SEARCH, TWITTER_SEARCH | String | `null`
source:uri | Uri of rss feed. Only supply for type RSS streams | For type RSS | String | `null`
source:type | Specify web or news search for BING_SEARCH streams | For type BING_SEARCH | `WEB` or `NEWS` | n/a
source:username | Basic auth username for secured rss feed. Only supply for type RSS streams. | For secured RSS streams | String | `null`
source:password | Basic auth password for secured rss feed. Only supply for type RSS streams. | For secured RSS streams | String | `null`
emailPostingEnabled | Allow posting to COLLECTION stream via email. | No | Boolean | false
streamEmailAddress | Email address to for stream if emailPosting is enabled. Only set for collection streams | No | Valid email string | `null`
openForReading | Allow all users to read this stream | No | boolean | false
openForPosting | Allow all users to post content to a COLLECTION stream | No | boolean | false
published | Publish the stream for users in your account to discover | No | boolean | false
rssEnabled | Allow public access to an RSS feed of this stream | No | boolean | false
tagIds | Stream tag IDs to tag the stream | No | [String] | []
categoryIds | Categories to put the stream in | Yes (empty array for no categories) | [String] | []


### Response

Status code `201`

## POST /streams/{streamId}/streams

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "streamId": "5519ae56e4b0c0419a88bae1"
     }' \
     https://api.attensa.net/streams/{streamId}/streams
```
> 303 redirect returned pointing to parent stream resource

Add a substream to a COLLECTION stream.

### Request

`POST https://api.attensa.net/streams/{streamId}/streams`

### JSON request body parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
streamId | The streamId of the child stream to be added | Yes | String | n/a

### Response

Status code `303` with `Location` header set to the url of the parent COLLECTION stream

## POST /streams/{streamId}/items

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "author": "John Doe",
       "description": "Description 01",
       "sourceUrl": "http://google.com",
       "title": "Test item 01"
     }' \
     https://api.attensa.net/streams/{streamId}/items
```
> Status code 202 with response as follows:

```json
"Item successfully queued"
```

Post an item to a COLLECTION stream.

### Request

`POST https://api.attensa.net/streams/{streamId}/items`

### JSON request body parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
author | The author name of the item | No | String | `null`
description | The body of the item. | Yes | String | n/a
sourceUrl | Url of the item to link to | No | String | `null`
title | Item title | Yes | String | n/a

### Response

Status code `202`

<aside class="notice">Item creation is asynchronous.  While items are typically created whithin a few seconds, there is no guaranteed time frame for when a posted item will be available. </aside>

## POST /streams/{streamId}/briefing

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "subject": "briefing subject",
       "description": "test description here",
       "schedule": {
         "startDate": 2015-06-07,
         "stopDate": 2015-10-11,
         "sendHour": 15,
         "sendMinute": 30,
         "frequency": "WEEKLY"
         "interval": 2,
         "sendDays": ["MO", "TU", "WE", "TH", "FR"],
         "timeZone": "US/Pacific"
       },
       "templateId" : 54eba226e4b050dd8b9c1099
     }' \
     https://api.attensa.net/streams/{streamId}/briefing
```
> Above request schedules a briefing to send every other week on weekdays only.  Returns 200 structured as follows:

```json
{
  "description": "test description here",
  "subject": "briefing subject",
  "templateId": "54eba226e4b050dd8b9c1099",
  "schedule": {
    "startDate": 2015-06-07,
    "stopDate": 2015-10-11,
    "sendHour": 15,
    "sendMinute": 30,
    "frequency": "WEEKLY",
    "interval": 2,
    "sendDays": ["MO", "TU", "WE", "TH", "FR"],
    "timeZone": "US/Pacific"
  },
  "stream": {
    "categoryIds": ["54eba224e4b050dd8b9c1096"],
    "emailPostingEnabled": false,
    "id": "5519ae56e4b0c0419a88bae1",
    "followersCount": 0,
    "itemsCount": 111,
    "openForPosting": false,
    "openForReading": true,
    "ownerId": "54da7849e4b02386a4658e5d",
    "published": true,
    "rssEnabled": true,
    "source": {
        "uri": "http://feeds.feedburner.com/dailyjs"
    },
    "tagIds": ["54da78488ab02386a4658eee"],
    "title": "DailyJS",
    "type": "RSS",
    "_links": {
      "self": "https://api.attensa.net/streams/5519ae56e4b0c0419a88bae1",
      "owner": "https://api.attensa.net/users/54da7849e4b02386a4658e5d"
    }
  }
}
```

Create a briefing and schedule for an existing stream

### Request

`POST https://api.attensa.net/streams/{streamId}/briefing`

### JSON body request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
description | Long description of the briefing | No | String | `null`
subject | Subject line used for sending briefing email | Yes | String | n/a
templateId | Email template to use | No | String of valid template id | id of default template
schedule:startDate | Day to start sending the briefing | Yes | `YYYY-MM-DD` | n/a
schedule:stopDate | Day to stop sending the briefing. Omit to never stop. | No | `YYYY-MM-DD` | `null`
schedule:sendHour | Hour of day to send briefing | Yes | Integer `0-23` | n/a
schedule:sendMinute | Minute of hour to send briefing | Yes | Integer `0-59` | n/a
schedule:frequency | Frequency to send briefing | Yes | `DAILY`, `WEEKLY`, `MONTHLY` | n/a
schedule:interval | Interval of frequency to send.  e.g. send every `<interval>` days  | No | Integer `1-31` | 1
schedule:sendDays | Array of days of the week to send briefing on | For WEEKLY frequency | [`SU`,`MO`,`TU`,`WE`,`TH`,`FR`,`SA`] | n/a
schedule:timeZone | Timezone of requested send time | Yes | [Supported time zone string](#time-zones) | `null`


### Response

Status code `200`

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
           "password": "myPasswordForSecuredRSSFeed"
       },
       "emailPostingEnabled": false,
       "streamEmailAddress": "test.stream.01@email.attensa.net",
       "openForReading": true,
       "rssEnabled": false,
       "tagIds": ["54da78488ab02386a4658eee"],
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
  "tagIds": ["54da78488ab02386a4658eee"],
  "emailPostingEnabled": false,
  "openForReading": true,
  "openForPosting": true,
  "published": true,
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668"],
  "itemsCount": 0,
  "followersCount": 0,
  "_links": {
    "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
    "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
  }
}
```

Update an existing stream.  Updates are applied in a incremental PATCH-like manner, so the entire stream resource does not need to be supplied, only the properties that are changing.

### Request

`PUT https://api.attensa.net/streams/{streamId}`

### JSON body request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
title | Stream Title | No | String | n/a
description | Stream description | No | String | n/a
ownerId | User id of stream owner | No | String of valid user id | n/a
source:search | Search term. Only supply for ATTENSA_SEARCH, PUBMED_SEARCH or TWITTER_SEARCH streams | No | String | n/a
source:uri | Uri of rss feed. Only supply for type RSS streams | No | String | n/a
source:username | Basic auth username for secured rss feed. Only supply for type RSS streams. | No | String | n/a
source:password | Basic auth password for secured rss feed. Only supply for type RSS streams. | No | String | n/a
emailPostingEnabled | Allow posting to COLLECTION stream via email. | No | Boolean | n/a
streamEmailAddress | Email address to for stream if emailPosting is enabled. Only set for collection streams | No | Valid email string | n/a
openForReading | Allow all users to read this stream | No | Boolean | n/a
openForPosting | Allow all users to post content to a COLLECTION stream | No | Boolean | n/a
published | Publish the stream for users in your account to discover | No | boolean | false
rssEnabled | Allow public access to an RSS feed of this stream | No | Boolean | n/a
tagIds | Stream tag IDs to tag the stream | No | [String] | n/a
categoryIds | Categories to put the stream in | No | [String] | n/a

<aside class="notice">Stream type can not be updated.  Once a stream is created it's type is immutable.</aside>
<aside class="notice">All categories or stream tags can be removed by sending an empty categoryIds or tagIds array (<code>"categoryIds": []</code>)</aside>
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

## DELETE /streams/{streamId}/briefing

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/streams/{streamId}/briefing
```
> 204 empty body returned on success

Remove a briefing from a stream

### Request

`DELETE https://api.attensa.net/streams/{streamId}/streams/{substreamId}`

### Response

Status code `204` with empty body

## DELETE /streams/{streamId}/streams/{substreamId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/streams/{streamId}/streams/{substreamId}
```
> 204 empty body returned on success

Remove a substream from an existing COLLECTION stream.

### Request

`DELETE https://api.attensa.net/streams/{streamId}/streams/{substreamId}`

### Response

Status code `204` with empty body
