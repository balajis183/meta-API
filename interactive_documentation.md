# 💬 WhatsApp Cloud API: Message Flow Documentation for Bluebex Software   (whatsapp-message-flow.md)

## 🧠 Overview

This document outlines the message flow rules, limitations, and structure used for the Bluebex Software WhatsApp chatbot using the WhatsApp Cloud API. It also includes a working interactive message format example.

---

## 🟡 Message Flow Types

### 1. ✅ Business-Initiated Messages
- **Definition:** Sent **without user consent** or **outside the 24-hour session window.**
- **Restriction:** Only **approved templates** can be sent.
- **Examples:**
  - Welcome messages
  - Promotional content
  - Important alerts

### 2. 🔄 User-Initiated Messages
- **Definition:** Sent by the user, which opens a 24-hour session.
- **Flexibility:** You can send **any message type** within this session:
  - Free-form text
  - Media
  - Interactive messages (buttons, lists)
  - Templates

---

## ❗️ Key Rule

> **Interactive messages (buttons, lists) can only be used when the user initiates a conversation or replies to your message within the 24-hour window.**

If the session is closed, use a template message to re-initiate.

---

## 🧊 Example: Business-Initiated Welcome Template

```json
{
  "messaging_product": "whatsapp",
  "to": "91981051xxxx",
  "type": "template",
  "template": {
    "name": "bluebex_chatbot",
    "language": { "code": "en" },
    "components": [
      {
        "type": "header",
        "parameters": [
          {
            "type": "image",
            "image": { "id": "9801615363183757" }
          }
        ]
      },
      {
        "type": "body",
        "parameters": [
          {
            "type": "text",
            "text": "Welcome to Bluebex Software Private Limited! 🎉\n\nWe specialize in cutting-edge technology solutions designed to accelerate your business growth.\n\nI’m Byte, your friendly virtual assistant from Bluebex Software 💙"
          }
        ]
      }
    ]
  }
}

---

#  📋 Follow-Up Interactive List (Only After User Replies)
### Once the user replies, you can send an interactive list message like this:

{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "91981051xxxx",
  "type": "interactive",
  "interactive": {
    "type": "list",
    "header": { "type": "text", "text": "Bluebex Services" },
    "body": { "text": "Please select one of the services below to know more:" },
    "footer": { "text": "Powered by Bluebex Software 💙" },
    "action": {
      "button": "Select Service",
      "sections": [
        {
          "title": "Our Services",
          "rows": [
            {
              "id": "web_dev",
              "title": "Web Development",
              "description": "Custom websites, portals, dashboards"
            },
            {
              "id": "app_dev",
              "title": "App Development",
              "description": "Native & hybrid mobile apps"
            },
            {
              "id": "devops",
              "title": "DevOps",
              "description": "CI/CD, infrastructure automation, cloud ops"
            }
          ]
        }
      ]
    }
  }
}


### 🧪 Suggested Flow


graph TD
    A[Business sends template] --> B[User replies]
    B --> C[Bot sends interactive list]
    C --> D[User selects option]
    D --> E[Bot sends info about selected service]

---

## 🧩 Recap

| Action Type             | Template Allowed? | Interactive Allowed? | Notes                                      |
|-------------------------|-------------------|------------------------|--------------------------------------------|
| Business Initiates      | ✅ Yes            | ❌ No                 | Must use approved template                 |
| User Replies            | ✅ Yes            | ✅ Yes                | 24-hour session opens                      |
| Within 24-Hour Window   | ✅ Yes            | ✅ Yes                | Free-form and interactive allowed          |


---


