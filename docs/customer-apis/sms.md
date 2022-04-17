# SMS
Devos provides customers with an API for sending and receiving SMS messages.

> These API endpoints requires authentication. If you're a customer of Devos and haven't got an API key, please [reach out](https://devos.no/kontakt).

## Authentication
Use the standard `Authorization: Bearer $API_KEY` header to authenticate.

## Base URL
All these requests have the following base URL:

```
https://api.devos.no/v1
```

## Sending an SMS

### Sender names
Only whitelisted sender names can be used in the `from` field. [Contact us](https://devos.no/kontakt) to get a new sender name whitelisted.

### Status callback
If you'd like to be notified whenever the status of the SMS changes, you can provide a `status_callback` field when creating the SMS. The provided URL will receive a `POST` request with the body of the message when the status changes.

### Request
```json
POST /sms

{
  "sms": {
    "from": "SenderName",
    "to": "+4799998888",
    "body": "Message goes here.",
    "status_callback": null || "https://example.com/sms/callback"
  }
}
```

### Response
If all goes well, you'll get a `201 Created` response with the following body:

```json
{
    "body": "Message goes here",
    "from": "Sender Name",
    "id": "9d7766cb-a3f9-4155-86e9-6153a0c00957",
    "inserted_at": "2022-04-17T12:57:43",
    "status": "accepted",
    "to": "+4799998888",
    "updated_at": "2022-04-17T12:57:43"
}
```

If something goes wrong, you'll get an appropriate status code and a body with the error message, like this:

#### 403 Forbidden
```json
{
  "error": "You are not allowed to use 'Testing' in the 'from' field."
}
```

#### 400 Bad Request
```json
{
    "error": "A 'To' phone number is required."
}
```