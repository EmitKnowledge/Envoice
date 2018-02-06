## Envoice API documentation with examples

*For more details please read the [official Envoice documentation](https://www.envoice.in/reference/api/docs/v1) or [postman documentation.](https://documenter.getpostman.com/collection/view/1150943-7298a928-f509-01a3-5e4c-08592855085c)*

This is a practical guide to inform users how to use the Envoice API in real case scenarios.  
Currently there are several business domains which you can interact with:
- [Client](./client.md)
- [General](./general.md)
- [Invoice](./invoice.md)
- [Tax](./tax.md) 
- [Work type](./work-type.md)

 ---

### Goal

This guide has a goal to teach you how to implement all real-case scenarios that might be useful having in your application. 
All examples will be presented as cURL request and JSON examples for request and response objects.

 ---

### Authentication setup

In order to use the Envoice API you must be a [user](https://www.envoice.in/pricing) and generate 
[API key and secret](https://www.envoice.in/account/settings#api-tab) from your account settings.

They might look something like this:  
API Key: `SkfoOZ3y8swCt6jXLYdPt1Km2Vgu5FVm8Pc2QsJ7niGl9HbGVjxaix4wncyb4`  
API Secret: `Ko3zHfv8bAMAwPKZFrolIHcEaS8QoVS3C6f8An4Tku8Cc25TsX1WOjXqzZ3Zh61`


An example usage with those credentials should look like this:  
```
curl --request GET \
  --url 'https://www.envoice.in/api/client/all' \
  --header 'x-auth-key: SkfoOZ3y8swCt6jXLYdPt1Km2Vgu5FVm8Pc2QsJ7niGl9HbGVjxaix4wncyb4TU' \
  --header 'x-auth-secret: Ko3zHfv8bAMAwPKZFrolIHcEaS8QoVS3C6f8An4Tku8Cc25TsX1WOjXqzZ3Zh61'
```
<sub style="color: darkblue;">\* for future examples we will use placeholders like \{YOUR_AUTH_KEY] and \{YOUR_AUTH_SECRET} to improve readability</sub>

## Quickstart

In order to send an invoice to a client with minimum data required you must follow the following process.

First create a work type, for example "Software development", some work you have done for your client.

###  New work type

api/worktype/new
```
curl --request POST \
  --url 'https://www.envoice.in/api/worktype/new' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Title": "API Integration"
    }'
```


Response: Id of created work type 

```
3764
```

You will use this id as an item in your invoice.

 --- 

After this you need to create a client, but for that you also need some system data.

### Get all supported countries
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

### Get all supported currencies


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
        "Symbol": "€"
    },
    {
        "Id": 170,
        "Name": "United Kingdom Pound",
        "Value": "GBP",
        "Symbol": "£"
    }
]
```

 --- 

### Get all supported languages

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
        "Id": 1,
        "Name": "English",
        "UiCulture": "en-US"
    },
    {
        "Id": 3,
        "Name": "German",
        "UiCulture": "de-DE"
    }
]
```

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

 --- 

###  New client

Lets say we want to add a client named Bob Smith from UK with email bob.smith@email.com.
That implies that he wants to receive invoice in Pound sterling and view the invoice in English.  

The minimal request that we have to send contains Name, Email, Language, Currency and Country, everything else is optional.  
Detailed information about which fields are accepted in the "New" and "Update" API calls can be found in the [official documentation](https://www.envoice.in/reference/api/docs/v1)


api/client/new
```
curl --request POST \
  --url 'https://www.envoice.in/api/client/new' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "ClientCurrencyId": 170,
      "ClientCountryId": 235,
      "UiLanguageId": 1,
      "Name": "Bob Smith",
      "Email": "bob.smith@email.com",
    }'
```


Response: Id of created client

```
2185
```

 --- 
 
Next you can finally create the invoice that would be sent to your client

###  New invoice


api/invoice/new
```
curl --request POST \
  --url 'https://www.envoice.in/api/invoice/new' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "ClientId": 2185,
      "Number": "#INV-0001",
      "IssuedOn": "2018-02-06T11:43:30Z",
      "Duedate": "2018-02-06T11:43:30Z",
      "Status": "Draft",
      "CurrencyId": 163,
      "PaymentGateways": [
        {
          "Name": "paypal"
        }
      ],
      "Items": [
        {
          "WorkTypeId": 2402,
          "Cost": 100,
          "Quantity": 1
        }
      ]
    }'
```