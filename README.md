# WhatsApp Cloud API Documentation

## Overview
The WhatsApp Cloud API allows businesses to send messages to users via WhatsApp. Different message types require specific fields to be included in the API request. This document outlines the necessary fields for each type of message implementation.

## General Requirements
Before sending messages, ensure that:
- The phone number is registered with WhatsApp Cloud API.
- The recipient has opted in to receive messages from your business (except for approved message templates).
- Your API request includes the required authentication headers.
- Your business follows WhatsApp's guidelines and policies to avoid delivery issues.

## Required Headers
All API requests should include:
```json
{
  "Authorization": "Bearer YOUR_ACCESS_TOKEN",
  "Content-Type": "application/json"
}
```

## API Request Format
### Endpoint
Use the following `POST` request format:
```
POST https://graph.facebook.com/v18.0/PHONE_ID/messages
```

### Required Fields
- `messaging_product`: Always set to `whatsapp`.
- `to`: Recipient's phone number in international format (e.g., `+919164949099`).
- `type`: Type of message (`text`, `template`, `image`, `contacts`, `document`, `audio`).
- Message-specific content fields.

## Message Types and Required Fields

### 1. Text Message
```json
{
  "messaging_product": "whatsapp",
  "to": "RECIPIENT_PHONE_NUMBER",
  "type": "text",
  "text": {
    "body": "Hello, this is a test message!"
  }
}
```

### 2. Template Message
```json
{
  "messaging_product": "whatsapp",
  "to": "RECIPIENT_PHONE_NUMBER",
  "type": "template",
  "template": {
    "name": "TEMPLATE_NAME",
    "language": {
      "code": "LANGUAGE_CODE"
    },
    "components": [
      {
        "type": "body",
        "parameters": [
          { "type": "text", "text": "John" }
        ]
      }
    ]
  }
}
```

### 3. Media Messages
**Example: Sending an Image**
```json
{
  "messaging_product": "whatsapp",
  "to": "RECIPIENT_PHONE_NUMBER",
  "type": "image",
  "image": {
    "link": "IMAGE_URL"
  }
}
```

### 4. Document Messages
```json
{
  "messaging_product": "whatsapp",
  "to": "RECIPIENT_PHONE_NUMBER",
  "type": "document",
  "document": {
    "link": "DOCUMENT_URL",
    "filename": "example.pdf"
  }
}
```

### 5. Audio Messages
```json
{
  "messaging_product": "whatsapp",
  "to": "RECIPIENT_PHONE_NUMBER",
  "type": "audio",
  "audio": {
    "link": "AUDIO_URL"
  }
}
```

### 6. Contact Messages
```json
{
  "messaging_product": "whatsapp",
  "to": "RECIPIENT_PHONE_NUMBER",
  "type": "contacts",
  "contacts": [
    {
      "name": {
        "formatted_name": "John Doe",
        "first_name": "John",
        "last_name": "Doe"
      },
      "phones": [
        {
          "phone": "1234567890",
          "type": "WORK"
        }
      ]
    }
  ]
}
```

### 7. Interactive Messages (Reply Buttons, List Messages)
**Example: Sending a Reply Button Message**
```json
{
  "messaging_product": "whatsapp",
  "to": "RECIPIENT_PHONE_NUMBER",
  "type": "interactive",
  "interactive": {
    "type": "button",
    "body": {
      "text": "Do you want to continue?"
    },
    "action": {
      "buttons": [
        {
          "type": "reply",
          "reply": {
            "id": "yes_button",
            "title": "Yes"
          }
        }
      ]
    }
  }
}
```

## Common Issues & Troubleshooting
1. **Recipient Not Receiving Messages**
   - Ensure the recipient has not blocked the business.
   - The message should comply with WhatsApp policies.
   - Use an approved template for the first message.
   - Check the template status (`active`, `quality pending`, etc.).

2. **Template Message Not Sending**
   - Verify that the template is approved and correctly formatted.
   - Ensure the parameters in `components` match the expected format.

3. **Media Message Not Displaying**
   - Ensure the media URL is publicly accessible.
   - Confirm the file format is supported by WhatsApp.

## Conclusion
This document provides an overview of the required fields for different message types in the WhatsApp Cloud API. Ensure that your API requests are correctly formatted and comply with WhatsApp’s policies to avoid delivery issues.

