# Overview

The public APIs are located at the following URL:

```
https://api.devos.no/v1/public/
```

If you do a `GET` request to this endpoint, you'll receive a JSON response with information about the available APIs:

```json
{
    "_message": "Welcome to the Devos Public API. For more information about this API, please see the attached URL.",
    "_url": "https://devos.no/api/",
    "apis": [
        {
            "description": "Retrieve information about Norwegian postal codes, municipalities, counties and cities.",
            "name": "Postal Code API (Norway)",
            "path": "/postal-codes"
        }
    ]
}
```

## Rate limiting
All public API endpoints are rate limited to 5 requests per 10 seconds per IP address. Authenticated requests are not rate limited, but this is not available to the public.