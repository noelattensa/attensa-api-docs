# Paging

## Paging format

> Paged responses return _paging and _links elements

```json
{
  "_paging": {
    "totalElementCount": 82,
    "pageCount": 5,
    "requestedPageSize": 20,
    "elementCount": 20,
    "page": 2
  },
  "_links": {
    "first": "https://api.attensa.net/users?rows=20&page=0",
    "last": "https://api.attensa.net/users?rows=20&page=4",
    "next": "https://api.attensa.net/users?rows=20&page=3",
    "previous": "https://api.attensa.net/users?rows=20&page=1"
  },
  "users": [
    { "arrayOfUsers": "goes here" }
  ]
}
```

Paged responses will return `_paging` and `_links` elements.

### `_paging` metadata:

* `totalElementCount`: The total number of elements across all pages
* `pageCount`: The number of pages
* `requestedPageSize`: The requested page size
* `elementCount`: The number of elements returned in the current page.  Not that in some cases this may be less than the requested page size due to de-duping rules or filters
* `page`: The current page number

### `_links` for paging:

* `first`: The first page (page 0) of the current result set
* `last`: The last page of the current result set
* `next`: The page immediately after the current page. Omitted if the current page is last.
* `previous`: The page before the current page. Omitted if the current page is first.

The return data will be named for the type of data being responded to (e.g. requesting users will return a `users` array while requesting streams will return a `streams` array)