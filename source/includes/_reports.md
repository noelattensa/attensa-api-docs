# Reports

## GET /reports

```shell
curl -u username:password https://api.attensa.net/reports
```
> Status code 200 with response as follows:

```json
[
  {
    "fromDate": "2016-05-04",
    "size": 123,
    "toDate": "2016-05-11",
    "type": "briefing_activity",
    "url": "<snip>"
  }
]
```

Get a list of all user activity reports for your account.  The `url` property will contain a signed link that is valid for 15 minutes that points to a tab seperated file with user activity.


### Request

`GET https://api.attensa.net/reports`

### Response

Status code `200`