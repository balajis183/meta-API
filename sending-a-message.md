# WhatsApp Cloud API - Send Message API Documentation

## Endpoint

```
POST https://graph.facebook.com/v18.0/512728175267525/messages
```

📌 **Note**: Always use your specific `phone_number_id` in the endpoint. In this example, `512728175267525` is the phone number ID.

## Headers

```json
{
  "Authorization": "Bearer YOUR_ACCESS_TOKEN",
  "Content-Type": "application/json"
}
```

## Request Body (Send Text Message)

```json
{
  "messaging_product": "whatsapp",
  "to": "919108105199",
  "type": "text",
  "text": {
    "body": "Hello !This is a sample text message"
  }
}
```

📌 **IMPORTANT**: 
- You must **modify the `body` text** under the `text` field to match the actual message you want to send.
- `to` is the recipient's WhatsApp number in international format.

## Sample Response

```json
{
  "messaging_product": "whatsapp",
  "contacts": [
    {
      "input": "919108105199",
      "wa_id": "919108105199"
    }
  ],
  "messages": [
    {
      "id": "wamid.HBgMOTE5MTA4MTA1MTk5FQIAERgSMjdCOTY2NDVBNzM4NUNFOTUwAA=="
    }
  ]
}
```

This confirms the message has been sent successfully to the WhatsApp user.

---



