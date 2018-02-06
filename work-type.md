## Work type

*For more details please read the [official Envoice documentation](https://www.envoice.in/reference/api/docs/v1) or [postman documentation.](https://documenter.getpostman.com/collection/view/1150943-7298a928-f509-01a3-5e4c-08592855085c#655ef83a-a1be-5212-78be-490f69f3e7c2)*

In this section we have pretty straightforward API calls that don't have any dependencies. This data is used when interacting with [invoices](./invoice.md) and [clients](./client.md).

 --- 

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

 --- 

###  Update work type

api/worktype/update
```
curl --request POST \
  --url 'https://www.envoice.in/api/worktype/update' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Title": "Software development",
      "Id: 3764
    }'
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

###  Delete work type

api/worktype/delete
```
curl --request POST \
  --url 'https://www.envoice.in/api/worktype/delete' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Id: 3764
    }'
```

Response: Id of deleted work type 

```
3764
```