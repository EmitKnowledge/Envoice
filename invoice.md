## Invoice

*For more details please read the [official Envoice documentation](https://www.envoice.in/reference/api/docs/v1) or [postman documentation.](https://documenter.getpostman.com/collection/view/1150943-7298a928-f509-01a3-5e4c-08592855085c#bc06f8eb-fa44-f34b-ea7a-dfaac35c1243)*



## Data dependencies

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
        "Name": "Euro Member Countries",
        "Value": "EUR",
        "Code": "978",
        "Symbol": "€",
        "Id": 163
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


###  Get all work types

api/worktype/all
```
curl --request GET \
  --url 'https://www.envoice.in/api/worktype/all' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
```

Response: List of all your work types

```
[
    {
        "Title": "Software development",
        "Id": 3764,
        "CreatedOn": "2018-01-17T08:42:41+00:00"
    }
]
```

 --- 

## Invoice API calls

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


Response: Created invoice

```
{
    "Items": [
        {
            "Id": 7936,
            "WorkTypeId": 2402,
            "Description": null,
            "Cost": 100,
            "Quantity": 1,
            "DiscountPercentage": 0,
            "TaxId": null,
            "TaxPercentage": 0,
            "DiscountAmount": 0,
            "TaxAmount": 0,
            "SubTotalAmount": 100,
            "TotalAmount": 100
        }
    ],
    "Attachments": [],
    "Payments": [],
    "Activities": [],
    "PaymentGateways": [
        {
            "Name": "paypal"
        }
    ],
    "Id": 3971,
    "Client": {
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
    },
    "Currency": {
        "Id": 163,
        "Name": "Euro Member Countries",
        "Value": "EUR",
        "Code": "978",
        "Symbol": null
    },
    "ClonedFromId": null,
    "RecurringProfileId": null,
    "Number": "#INV-0001",
    "IssuedOn": "2018-02-06T01:00:00+01:00",
    "Duedate": "2018-02-06T01:00:00+01:00",
    "PoNumber": null,
    "DiscountAmount": 0,
    "TaxAmount": 0,
    "SubTotalAmount": 100,
    "TotalAmount": 100,
    "Terms": null,
    "Notes": null,
    "Status": 0,
    "EnablePartialPayments": false,
    "AccessToken": "7qbW8V49wB2uK7mfWm9FZGZufMjw8MYTfXikmvMxIThvMdVvHG9T6hv8o7XCEC9f6hge9AEBWkarpGJiSSsbV9wSAXKGqRnpn1JHlrAhTwuf3rxGgqgEcwEUd7kucCJC"
}
```

 --- 

###  Update invoice

api/invoice/update
```
curl --request POST \
  --url 'https://www.envoice.in/api/invoice/update' \
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
          "Cost": 200,
          "Quantity": 1,
          "Id": 7936,
        }
      ]
    }'
```


Response: Updated invoice

```
{
    "Items": [
        {
            "Id": 7936,
            "WorkTypeId": 2402,
            "Description": null,
            "Cost": 100,
            "Quantity": 1,
            "DiscountPercentage": 0,
            "TaxId": null,
            "TaxPercentage": 0,
            "DiscountAmount": 0,
            "TaxAmount": 0,
            "SubTotalAmount": 100,
            "TotalAmount": 100
        }
    ],
    "Attachments": [],
    "Payments": [],
    "Activities": [],
    "PaymentGateways": [
        {
            "Name": "paypal"
        }
    ],
    "Id": 3971,
    "Client": {
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
    },
    "Currency": {
        "Id": 163,
        "Name": "Euro Member Countries",
        "Value": "EUR",
        "Code": "978",
        "Symbol": null
    },
    "ClonedFromId": null,
    "RecurringProfileId": null,
    "Number": "#INV-0001",
    "IssuedOn": "2018-02-06T01:00:00+01:00",
    "Duedate": "2018-02-06T01:00:00+01:00",
    "PoNumber": null,
    "DiscountAmount": 0,
    "TaxAmount": 0,
    "SubTotalAmount": 100,
    "TotalAmount": 100,
    "Terms": null,
    "Notes": null,
    "Status": 0,
    "EnablePartialPayments": false,
    "AccessToken": "7qbW8V49wB2uK7mfWm9FZGZufMjw8MYTfXikmvMxIThvMdVvHG9T6hv8o7XCEC9f6hge9AEBWkarpGJiSSsbV9wSAXKGqRnpn1JHlrAhTwuf3rxGgqgEcwEUd7kucCJC"
}
```

 --- 

###  Get all invoices

api/invoice/all
```
curl --request GET \
  --url 'https://www.envoice.in/api/invoice/all' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
```

Response: List of all your invoices

```
{
    "TotalCount": 16,
    "Count": 10,
    "Result": {
    "TotalCount": 17,
    "Count": 10,
    "Result": [        
        {
            "Id": 3900,
            "Client": {
                "Id": 2181,
                "CreatedOn": "2018-01-11T15:22:11+01:00",
                "ClientCurrencyId": 163,
                "ClientCountryId": 235,
                "UiLanguageId": 1,
                "Name": "vojdan",
                "Address": "",
                "Email": "vojdan.gicharovski@gmail.com",
                "CC": "vojdan.gicharovski@gmail.com",
                "PhoneNumber": "+44135645465465",
                "Vat": "12"
            },
            "Currency": {
                "Id": 163,
                "Name": "Euro Member Countries",
                "Value": "EUR",
    			"Code": "978",
                "Symbol": null
            },
            "ClonedFromId": null,
            "RecurringProfileId": null,
            "Number": "INV-00009",
            "IssuedOn": "2018-01-25T01:00:00+01:00",
            "Duedate": "2018-02-09T01:00:00+01:00",
            "PoNumber": null,
            "DiscountAmount": 0,
            "TaxAmount": 0,
            "SubTotalAmount": 30,
            "TotalAmount": 30,
            "Terms": "",
            "Notes": "",
            "Status": 0,
            "EnablePartialPayments": false,
            "AccessToken": "ndzvFfuMNeA1mzh6YjjSVYLdyIj9eWZDNSeBCOhdgLjGzWn9F934kFD7swowVqlaMABloXcPsS1HFeDxMbS3mjTKa0vzFdheTFAx00TEiejARHwgzBcrSO7NmZigWgj5"
        }
    ],
    "IsFaulted": false,
    "ErrorMessages": []
}
```

 --- 

###  Delete invoice

api/invoice/delete
```
curl --request POST \
  --url 'https://www.envoice.in/api/client/delete' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Id: 3900
    }'
```

Response: Id of deleted invoice

```
3900
```

 --- 

###  Send to client

api/invoice/sendtoclient
```
curl --request POST \
  --url 'https://www.envoice.in/api/client/sendtoclient' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Id": 3900, // down support, will be removed
      "InvoiceId": 3900,
      "Message": "Hey, please pay me!",
    }'
```

Response: Id of sent invoice

```
3900
```

 --- 

###  Send to accountant

api/invoice/sendtoclient
```
curl --request POST \
  --url 'https://www.envoice.in/api/client/sendtoaccountant' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Id": 3900
    }'
```

Response: Id of sent invoice

```
3900
```

 --- 

###  Change status

api/invoice/changestatus
```
curl --request POST \
  --url 'https://www.envoice.in/api/client/changestatus' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Id": 3900,
      "Status": "Draft",
    }'
```

Response: Boolean if the action is successful

```
true
```

 --- 

###  Status

api/invoice/status?id=3900
```
curl --request GET \
  --url 'https://www.envoice.in/api/client/status?id=123' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}'
```

Response: Invoice status

```
Draft
```

 --- 

###  Uri

api/invoice/uri?id=123
```
curl --request GET \
  --url 'https://www.envoice.in/api/client/uri?id=3900' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}'
```

Response: Invoice link for sharing

```
{
  "Link": "https://www.envoice.in/invoice/shared?token=Pp0txiAhE53VsEJtlV0WGAmfAoHgf9W77ScN1436SfVfv7fKSBaNbCQiGFQpNxcGWEkIAxwrL75OmiDoRRY30aPQxIVy9Qvp3i7MtG8kjRLvNFTdCePFxtEECJpqJERP&id=v6WMc2Bb6RhXdz0NOkfeAd6RzMVrJ2DKJI1oHs38upM"
}
```

 --- 

###  Details

api/invoice/details?id=3900
```
curl --request GET \
  --url 'https://www.envoice.in/api/client/details?id=3900' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}'
```

Response: Invoice details

```
{
    "Items": [
        {
            "Id": 7782,
            "WorkTypeId": 2402,
            "Description": "",
            "Cost": 30,
            "Quantity": 1,
            "DiscountPercentage": 0,
            "TaxId": null,
            "TaxPercentage": 0,
            "DiscountAmount": 0,
            "TaxAmount": 0,
            "SubTotalAmount": 30,
            "TotalAmount": 30
        }
    ],
    "Attachments": [],
    "Payments": [],
    "Activities": [],
    "PaymentGateways": [
        {
            "Name": "klikandpay"
        },
        {
            "Name": "paypal"
        }
    ],
    "Id": 3900,
    "Client": {
        "Id": 2181,
        "CreatedOn": "2018-01-11T15:22:11+01:00",
        "ClientCurrencyId": 163,
        "ClientCountryId": 235,
        "UiLanguageId": 1,
        "Name": "vojdan",
        "Address": "",
        "Email": "vojdan.gicharovski@gmail.com",
        "CC": "vojdan.gicharovski@gmail.com",
        "PhoneNumber": "+44135645465465",
        "Vat": "12"
    },
    "Currency": {
        "Id": 163,
        "Name": "Euro Member Countries",
        "Value": "EUR",
        "Code": "978",
        "Symbol": null
    },
    "ClonedFromId": null,
    "RecurringProfileId": null,
    "Number": "INV-00009",
    "IssuedOn": "2018-01-25T01:00:00+01:00",
    "Duedate": "2018-02-09T01:00:00+01:00",
    "PoNumber": null,
    "DiscountAmount": 0,
    "TaxAmount": 0,
    "SubTotalAmount": 30,
    "TotalAmount": 30,
    "Terms": "",
    "Notes": "",
    "Status": 0,
    "EnablePartialPayments": false,
    "AccessToken": "ndzvFfuMNeA1mzh6YjjSVYLdyI29eWZDNSeBCOhdgLjGzWn9F934kFD7s3hwVqlaMABloXcPbS1HFeDxMbS3mjTKa0vzFdheTFAx00TEiejARHwgzBcrSO7NmZigWgj5"
}
```