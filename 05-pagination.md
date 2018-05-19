# Pagination

All `ledger` routes are paginated. Pagination routes can have the following query parameters: `limit`, `order`, `before`, `after`, and `page`.

## Limit

```
/ledger?limit=1
```

The default value for `limit` is 100.

## Order

```
/ledger?order=asc
```

The default value for `order` is `desc` which shows the most recent transactions first.

## Before and After

```
/ledger?before=1526711066983&after=1516711066983
```

The values for `before` and `after` needs to be a UTC timestamp (number of milliseconds elapsed since January 1, 1970 00:00:00 UTC).


## Page

```
/ledger?page=2&limit=5
```
