# 📄 WhatsApp Cloud API — Sending Invoice with Template and PDF

This documentation explains how to send an **approved WhatsApp template message** using the Meta (Facebook) Graph API, including how to attach a PDF invoice either via **media ID** or a **public URL**.

---

## 📌 Endpoint

```http
POST https://graph.facebook.com/v22.0/{phone_number_id}/messages
```

- Replace `{phone_number_id}` with your actual **WhatsApp Business Phone Number ID**.

---

## 🧾 Headers

```json
Content-Type: application/json  
Authorization: Bearer YOUR_TOKEN
```

---

## 📤 Request Body — Send Invoice Template

This request sends a WhatsApp message using the approved `bluebex_invoice` template.

### ✅ With Media ID
```json
{
  "messaging_product": "whatsapp",
  "to": "recipient_number",
  "type": "template",
  "template": {
    "name": "bluebex_invoice",
    "language": {
      "code": "en"
    },
    "components": [
      {
        "type": "header",
        "parameters": [
          {
            "type": "document",
            "document": {
              "filename": "Bluebex_invoice.pdf",
              "id": "1393679178313783"
            }
          }
        ]
      },
      {
        "type": "body",
        "parameters": [
          {
            "type": "text",
            "text": "{Dynamic User name}" //variable
          }
        ]
      }
    ]
  }
}
```

### 🌐 With Public URL Instead of Media ID
```json
{
  "messaging_product": "whatsapp",
  "to": "recipient_number",
  "type": "template",
  "template": {
    "name": "bluebex_invoice",
    "language": {
      "code": "en"
    },
    "components": [
      {
        "type": "header",
        "parameters": [
          {
            "type": "document",
            "document": {
              "filename": "Bluebex_invoice.pdf",
              "link": "https://yourdomain.com/invoice/Bluebex_invoice.pdf"
            }
          }
        ]
      },
      {
        "type": "body",
        "parameters": [
          {
            "type": "text",
            "text": "Dynamic User name"   //variable
          }
        ]
      }
    ]
  }
}
```

---

## 🧑‍💻 Node.js Axios Code Sample

```js
const axios = require("axios");
require("dotenv").config();

const TOKEN = process.env.TOKEN;

axios.post(
  `https://graph.facebook.com/v22.0/${phone_number_id}/messages`,
  {
    messaging_product: "whatsapp",
    to: recipient,
    type: "template",
    template: {
      name: "bluebex_invoice",
      language: { code: "en" },
      components: [
        {
          type: "header",
          parameters: [
            {
              type: "document",
              document: {
                filename: "Bluebex_invoice.pdf",
                id: mediaId
              }
            }
          ]
        },
        {
          type: "body",
          parameters: [
            {
              type: "text",
              text: personName
            }
          ]
        }
      ]
    }
  },
  {
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${TOKEN}`
    }
  }
);

```

---

## 📎 Uploading PDF to Get Media ID

To upload a PDF and get the `media_id`, use the following:

### 🔗 Endpoint
```http
POST https://graph.facebook.com/v22.0/{phone_number_id}/media
```

### 🧾 Form Data Parameters
```bash
file = Invoice98765432108.pdf
messaging_product = whatsapp
```

### 💡 Notes
- Attach the file as `form-data`
- After uploading, you'll get a JSON response:
```json
{
  "id": "1393679178313783"
}
```
- Use this ID in your template message to send as a document

---

✅ With this setup, you can dynamically send invoices to customers on WhatsApp with personalized names and documents — either using a hosted link or by uploading to Meta.

Let me know if you need Markdown download or want this as a shared file!

