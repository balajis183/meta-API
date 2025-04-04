# 📌 Webhooks & WhatsApp Templates - Advanced Reference

## 1️⃣ What is a Webhook?  
A **webhook** is a server endpoint (URL) that listens for real-time events from an external service. Instead of polling for updates, the external service **pushes** data automatically when an event occurs.

### 🔹 How It Works:
1. A webhook URL is set up on your server.
2. When an event happens (e.g., a user replies on WhatsApp), WhatsApp **sends the event data** to your webhook.
3. Your server **processes the event** and takes action (e.g., storing the message, triggering automation, etc.).

---

## 2️⃣ Why Do We Need a Webhook for WhatsApp Messages?  
Webhooks help **track and process** user responses to business-initiated messages (such as WhatsApp template messages).  

### 🔹 Why store webhook responses?  
✅ **Monitor delivery & user interactions** (Did the user receive, read, or reply to a message?)  
✅ **Automate workflows** (e.g., auto-replies based on user input)  
✅ **Store chat history** for analytics & reporting  
✅ **Error handling & debugging** (e.g., checking failed messages)  

Without a webhook, we wouldn’t know **whether messages were delivered or what the user responded with**.

---

## 3️⃣ How to Handle Multiple WhatsApp Templates in a Webhook?  
Instead of writing **separate code for each template**, we process all templates **dynamically** based on the webhook payload.

### 4️⃣ Optimized Webhook Code (Express.js)

```bash

const express = require("express");
const app = express();

app.use(express.json()); // Middleware to parse JSON

// Webhook endpoint
app.post("/webhook", (req, res) => {
    const body = req.body;

    // Validate if webhook contains messages
    if (body.entry && body.entry[0].changes && body.entry[0].changes[0].value.messages) {
        const messages = body.entry[0].changes[0].value.messages;

        messages.forEach((msg) => {
            if (msg.type === "template" && msg.template) {
                const templateName = msg.template.name;
                console.log(`Received template: ${templateName}`);

                handleTemplate(templateName, msg);
            }
        });
    }

    res.sendStatus(200); // Respond to WhatsApp webhook
});

// Function to process different templates dynamically
function handleTemplate(templateName, msg) {
    switch (templateName) {
        case "order_confirmation":
            console.log("Processing Order Confirmation...");
            break;
        
        case "appointment_reminder":
            console.log("Processing Appointment Reminder...");
            break;

        case "payment_update":
            console.log("Processing Payment Update...");
            break;

        default:
            console.log(`Unhandled template: ${templateName}`);
    }
}

// Start server
app.listen(3000, () => console.log("Webhook listening on port 3000"));


```bash



#### 5️⃣ 🚀 Key Takeaways

✅ Why This Webhook is Better:
Handles multiple templates dynamically (no need for separate code per template).

Processes multiple messages in one webhook request.

Uses a switch-case for structured template handling.

Logs unhandled templates for debugging.

Easily extendable – just add a new case when new templates are introduced.




This Markdown file will help you **quickly review** webhooks and WhatsApp templates whenever needed! 
