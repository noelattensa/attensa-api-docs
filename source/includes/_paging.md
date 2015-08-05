# Paging

## Paging format

> Paged responses return a _paging element

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
    { "arrayOfUsers": "goes here" }
  ]
}
```

Paged responses will return a `_paging` element with paging metadata as shown to the right. The return data will be named for the type of data being responded to (e.g. requesting users will return a `users` array while requesting streams will return a `streams` array)

Paging metadata:

* `totalElementCount`: The total number of elements across all pages
* `pageCount`: The number of pages
* `requestedPageSize`: The requested page size
* `elementCount`: The number of elements returned in the current page.  Not that in some cases this may be less than the requested page size due to de-duping rules or filters
* `page`: The current page number
