# WhatsApp Cloud API - Send Message for new users using a template 

### since we can't send a text message directly without user consent so we need to use pre approved message template !

## Endpoint

```
POST https://graph.facebook.com/v22.0/512728175267525/messages
```

📌 **Note**: Always use your specific `phone_number_id` in the endpoint. In this example, `512728175267525` is the phone number ID.

## Headers

```json
{
  "Authorization": "Bearer YOUR_ACCESS_TOKEN",
  "Content-Type": "application/json"
}
```

# Template preview
![image](https://github.com/user-attachments/assets/86ba39d5-49d1-42d5-94b0-f94212ba2ec1)


## Request Body (Send template  Message)

```json
{
    "messaging_product": "whatsapp",
    "to": "919618863286", 
    "type": "template",
    "template": {
        "name": "text_message",
        "language": {
            "code": "en"
        }
    }
}
```


- `to` is the recipient's WhatsApp number in international format.


### To recipient receives this message in their whatsapp Account !!

The template has this text predefined!!!
```
Welcome to Bluebex Software Private Limited!

Just reply "Hi" to this message so we can get started. 🚀
```

## Sample Response

```json
{
    "messaging_product": "whatsapp",
    "contacts": [
        {
            "input": "919618863286",
            "wa_id": "919618863286"
        }
    ],
    "messages": [
        {
            "id": "wamid.HBgMOTE5NjE4ODYzMjg2FQIAERgSNUJGODRENjJBRjY2NjA2ODlGAA==",
            "message_status": "accepted"
        }
    ]
}
```

This confirms the message has been sent successfully to the WhatsApp user.

---


