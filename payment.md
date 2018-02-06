## Payment

*For more details please read the [official Envoice documentation](https://www.envoice.in/reference/api/docs/v1) or [postman documentation.](https://documenter.getpostman.com/collection/view/1150943-7298a928-f509-01a3-5e4c-08592855085c#94bd4cf4-d3dc-ee29-7861-24eda482142e)*

In this section we have pretty straightforward API calls that don't have any dependencies. This data is used when interacting with [invoices](./invoice.md).

 --- 

###  Supported payment providers

api/payment/supported
```
curl --request GET \
  --url 'https://www.envoice.in/api/general/countries' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}'
```

Response:
```
[
    {
        "Name": "paypal",
        "SupportedCurrencies": []
    },
    {
        "Name": "stripe",
        "SupportedCurrencies": []
    },
    {
        "Name": "payoneer",
        "SupportedCurrencies": [
            {
                "Name": "Euro Member Countries",
                "Value": "EUR"
            },
            {
                "Name": "Pound sterling",
                "Value": "GBP"
            },
            {
                "Name": "United States Dollar",
                "Value": "USD"
            },
            {
                "Name": "Australian Dollar",
                "Value": "AUD"
            }
        ]
    },
    {
        "Name": "square",
        "SupportedCurrencies": []
    },
    {
        "Name": "klikandpay",
        "SupportedCurrencies": [
            {
                "Name": "Euro Member Countries",
                "Value": "EUR"
            }
        ]
    }
]
```