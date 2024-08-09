---
search:
  exclude: false
---

# Lightrun REST API

## Introduction 

The Lightrun API is an HTTP REST API. From Lightrun version 1.29, you can configure REST API commands for the Runtime Reachability feature.

This is how you use the Lightrun REST API using cURL as an example.

```yaml
/api/v<number>/<entity>/....
```

You can download cURL here. For information on how to configure and use cURL, click [here](https://curl.se/docs/manpage.html). 

### Availability

From Lightrun version 1.29, the Lightrun APIs are available as part of the Lightrun Server.

### Authentication

Lightrun uses [API keys](/api-keys/) to authenticate REST API requests. You manage your API keys directly in the Lightrun Management Portal.

All APIs require authentication. The api-key will be passed via an http header.


```yaml
curl --header "Authorization: Bearer API-KEY" url
```

Lightrun returns the following error message with a status code of 401 if authentication information is not valid or missing.

```yaml
{
  "message": "401 Unauthorized"
}
```

### Data Encryption

The communication is encrypted at transit via TLS 1.2 or higher.

### Pagination

Lightrun supports offset-based pagination, where the default number of records on a page is 10, with a maximum limit of 1000 records.

To modify pagination when listing resources, you can use the offset and limit parameters.

For example, the command to retrieve records 51 through 75, would be:

```yaml
curl "https://lightrun.com/api/v1/reports?offset=50&limit=25"
```

### HTTP Response Codes

Lightrun uses standard HTTP response codes to indicate the success or failure of an API request.
The following table provides a list of return codes along with an explanation for each code.

| Number | Type           | Description                                                     |
|--------|----------------|-----------------------------------------------------------------|
| 200    | OK             | Successful transition.                                           |
| 201    | Package added to the watch list. | Package successfully added to watchlist. |
| 400    | Invalid input, object invalid parameters | The request failed because it didn't include all the information. |
| 401    | Unauthorized   | API Key is invalid.                                             |
| 402    | Request Failed| The request failed but the parameters are valid.               |
| 409 | Watched package already exists | The package added to the watch list already is set as watched.|


## Get Started

To access the Lightrun API, click [here](/public_api/api-reference/).
