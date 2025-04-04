# WhatsApp API Cloud Setup & Progress

## Overview
This document outlines the setup process and progress for integrating WhatsApp Cloud API. It details the required fields, authentication mechanisms, policy constraints, and challenges faced during implementation.

## Setup Requirements
To configure the WhatsApp Cloud API, we require the following four fields:
1. **Phone Number ID** - The unique identifier for the phone number registered with WhatsApp API.
2. **Access Token** - Used for authentication and secure communication with WhatsApp Cloud API.
3. **From Number** - The sender's phone number.
4. **To Number** - The recipient's phone number.

## Authentication
- A **permanent access token** has been created to resolve security concerns and ensure secure API requests.
- The token is used to authenticate API calls and prevent unauthorized access.

## Meta Policy Compliance
- As per **Meta's policy**, promotional messages **cannot** be sent without user consent or without the user initiating the conversation.
- To comply with this policy, we have created multiple API endpoints that support user-consent-based messages, including:
  - **Text messages**
  - **PDF files**
  - **Images with captions**
  - **Addresses**
  - **Audio messages**
  - **Text messages with URLs**
  - **Locations**
  - **Videos**
  - **Contacts**
- These message types can be sent **without using a template**, but they still require prior user consent.

## Sending Messages Without User Consent
- The only way to send messages **without user consent** is by using **Meta-approved WhatsApp templates**.
- Templates must be pre-approved by Meta before they can be used.
- Even when using the Meta test number, sending a template message requires user consent (such as OTP verification).

## Progress So Far
- **Test numbers** have been used to send template messages successfully.
- Several **message templates** have been created, including:
  - **Test Message Template**
  - **Purchase Receipt Template (PDF Format)**
  - **Greetings Template (Visit Website / Call Phone Number)**

## Challenges Faced
- Sending templates through an **official business account** requires **business information verification**.
- Until the business information is updated and verified, sending messages from the official WhatsApp Business Account remains restricted.

## Next Steps
- **Update business information** to enable sending messages via an official business account.
- **Integrate Terms of Service** to further enhance compliance and optimize messaging for customers.

---
### **Conclusion**
Once the business information is updated and approved, we will be able to send WhatsApp templates without requiring user consent, enabling automated and optimized communication with customers.

