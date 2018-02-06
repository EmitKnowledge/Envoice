## Client

*For more details please read the [official Envoice documentation](https://www.envoice.in/reference/api/docs/v1) or [postman documentation.](https://documenter.getpostman.com/collection/view/1150943-7298a928-f509-01a3-5e4c-08592855085c#52bd095a-ca2a-aeae-6bf7-dda9b114a713)*

A client is a person or legal entity that will be the receiver of your invoices. 
The client can pay the invoice via many payment gateways like PayPal, Payoneer, Stripe and others. 

In order to have the correct information on an invoice, you as a user must enter the information about all clients that you want to use throughout Envoice. 

## Data dependencies

Because the client itself holds the information about `country`, `language` and `currency` that will be used throughout the invoices he receives, we must put the correct `Id` in the corresponding fileds when creating or updating a client.

*For more details please read the [general readme](./general.md)*

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

## Client API calls

###  New client

Lets say we want to add a client named Bob Smith from UK with email bob.smith@email.com.
That implies that he wants to receive invoice in Pound sterling and view the invoice in English.  

The minimal request that we have to send contains Name, Email, Language, Currency and Country, everything else is optional.  
Detailed information about which fields are accepted in the "New" and "Update" API calls can be found in the official documentation](https://www.envoice.in/reference/api/docs/v1)


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

###  Update client

Lets say Bob changed his mind and wants to receive all invoices in Euros, all we have to do is change the `ClientCurrencyId` field to match the euros `Id` and update the client.

api/client/update
```
curl --request POST \
  --url 'https://www.envoice.in/api/client/update' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "ClientCurrencyId": 163,
      "ClientCountryId": 235,
      "UiLanguageId": 1,
      "Name": "Bob Smith",
      "Email": "bob.smith@email.com",
      "Id": 2185
    }'
```

 --- 

###  Get all clients

api/client/all
```
curl --request GET \
  --url 'https://www.envoice.in/api/client/all' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
```

Response: List of all your clients

```
[
    {
        "Id": 2185,
        "CreatedOn": "2018-01-31T15:19:52+01:00",
        "ClientCurrencyId": 170,
        "ClientCountryId": 235,
        "UiLanguageId": 1,
        "Name": "Bob Smith",
        "Address": null,
        "Email": "bob.smith@email.com",
        "CC": null,
        "PhoneNumber": null,
        "Vat": null
    }
]
```

 --- 

###  Delete client

api/client/delete
```
curl --request POST \
  --url 'https://www.envoice.in/api/client/delete' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Id: 2185
    }'
```

Response: Id of deleted client

```
2185
```