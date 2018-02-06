## Tax

*For more details please read the [official Envoice documentation](https://www.envoice.in/reference/api/docs/v1) or [postman documentation.](https://documenter.getpostman.com/collection/view/1150943-7298a928-f509-01a3-5e4c-08592855085c#5e656527-d1e1-0ac1-22bd-944b292f9406)*

In this section we have pretty straightforward API calls that don't have any dependencies. This data is used when interacting with [invoices](./invoice.md) and [clients](./client.md).

 --- 

###  New tax

api/tax/new
```
curl --request POST \
  --url 'https://www.envoice.in/api/tax/new' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Name": "Personal tax",
      "Percentage": 10
    }'
```


Response: Id of created tax

```
311
```

 --- 

###  Update tax

api/tax/update
```
curl --request POST \
  --url 'https://www.envoice.in/api/tax/update' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Name": "Other tax",
      "Percentage": 12,
      "Id: 311
    }'
```

 --- 

###  Get all taxes

api/tax/all
```
curl --request GET \
  --url 'https://www.envoice.in/api/tax/all' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
```

Response: List of all your taxes

```
[
    {
        "Name": "Other tax",
        "Percentage": 12,
        "Id": 311,
        "CreatedOn": "2018-01-17T08:42:41+00:00"
    }
]
```

 --- 

###  Delete tax

api/tax/delete
```
curl --request POST \
  --url 'https://www.envoice.in/api/tax/delete' \
  --header 'Content-Type: application/json' \
  --header 'x-auth-key: {YOUR_AUTH_KEY}' \
  --header 'x-auth-secret: {YOUR_AUTH_SECRET}' \
  --data '{
      "Id: 311
    }'
```

Response: Id of deleted tax

```
311
```