## General

*For more details please read the [official Envoice documentation](https://www.envoice.in/reference/api/docs/v1) or [postman documentation.](https://documenter.getpostman.com/collection/view/1150943-7298a928-f509-01a3-5e4c-08592855085c#f935d027-1bb5-7a13-395d-99603d481fc9)*

In this section we have pretty straightforward API calls that don't have any dependencies. This data is used when interacting with [invoices](./invoice.md) and [clients](./client.md).

 --- 

###  Countries

api/general/countries
```
curl --request GET \
  --url 'https://www.envoice.in/api/general/countries' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}'
```

Response (shortened for readability purposes, ~249 items in real output):
```
[
    {
        "Id": 235,
        "Name": "United Kingdom (UK)",
        "Value": "GB"
    },
    {
        "Id": 237,
        "Name": "United States of America (USA)",
        "Value": "US"
    }
]
```

 --- 

### Currencies 

api/general/currencies
```
curl --request GET \
  --url 'https://www.envoice.in/api/general/currencies' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}'
```

Response (shortened for readability purposes, ~32 items in real output):
```
[
    {
        "Id": 163,
        "Name": "Euro Member Countries",
        "Value": "EUR",
        "Code": "978",
        "Symbol": "€"
    },
    {
        "Name": "United Kingdom Pound",
        "Value": "GBP",
        "Code": "826",
        "Symbol": "£",
        "Id": 170
    }
]
```

 --- 

### UI Languages

api/general/uilanguages
```
curl --request GET \
  --url 'https://www.envoice.in/api/general/uilanguages' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}'
```

Response (shortened for readability purposes, ~12 items in real output):
```
[
    {
        "Id": 9,
        "Name": "Bulgarian",
        "UiCulture": "bg-BG"
    },
    {
        "Id": 11,
        "Name": "Croatian",
        "UiCulture": "hr-HR"
    }
]
```