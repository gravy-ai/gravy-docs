# Gravy API Authorization

All Gravy API endpoints require simple Token Based Authentication

This is accomplished by adding the provided api token in the Authorization header.

ex.

```Authorization: token YOUR_API_TOKEN_HERE```

###Error Codes

Improper authorization will return the following errors:

| Code | Description |
|:---|---|
| 403 |  Missing Authorization Header |
| 400 | Authorization Header is Malformed |
| 404 | The token provided in the Authorization has no associated Client |
