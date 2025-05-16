---

# 🔧 Chat Message Storage & Notification - Feature Documentation

This module handles **storing WhatsApp chat messages in Firebase**, **sending notifications**, **tracking unread messages**, and **counting unread conversations**. Below is a detailed breakdown of how each feature works, including references to relevant code blocks.

## ✅ Core Responsibilities

1. **Store Incoming and Outgoing Messages**
2. **Send Notifications for Incoming Messages**
3. **Handle Form Submissions as Special Messages**
4. **Format Interactive Messages**
5. **Maintain Last Message Metadata**
6. **Track Unread Message Count per Chat**
7. **Track Unread Conversations Globally**

---

## 📩 1. Store Chat Messages

All incoming/outgoing messages are stored in the Firebase Realtime Database under the path:

```
chats/{phoneNumber}/messages
```

Each message object includes:

```json
{
  "content": "Hello there!",
  "profileName": "John Doe",
  "phoneNumber": "+911234567890",
  "messageType": "text",
  "direction": "incoming", // or "outgoing"
  "timestamp": "2025-05-13T10:30:00.000Z",
  "createdAt": "2025-05-13T10:30:00.000Z"
}
```

### 🔄 Direction Defaulting

If `direction` is not provided, it defaults to `"incoming"`.

---

## 📋 2. Handle Form Submissions

If a message is of type `form_submission`, it's treated specially:

* Stored normally under the messages path.
* Triggers a push notification to the user if it’s incoming.

```js
if (message.messageType === "form_submission") {
  await db.ref(`chats/${message.phoneNumber}/messages`).push(message);
  // ... send notification if incoming
}
```

---

## 💬 3. Format Interactive Messages

Interactive messages (like buttons or list replies) are transformed into readable text:

```js
if (message.messageType === "interactive") {
  message.content = `User clicked on '${message.content}' button`;
}
```

---

## 🕓 4. Store Last Message Metadata

The most recent message is stored at:

```
chats/{phoneNumber}/lastMessage
```

With these fields:

```json
{
  "content": "Hello there!",
  "timestamp": "2025-05-13T10:30:00.000Z",
  "date": "2025-05-13",
  "time": "04:00 PM",
  "unixTimestamp": 1747132800
}
```

This helps in displaying previews in chat lists.

---

## 🔕 5. Send Notifications for Incoming Messages

For all `incoming` messages (text, interactive, form), a push notification is sent:

```js
if (messageData.direction === "incoming") {
  await this.sendNotification(...);
}
```

---

## 🔢 6. Track Unread Message Count (Per Chat)

Each chat stores an `unreadCount` field. When a new `incoming` message is received:

```js
await db.ref(`chats/${phoneNumber}/unreadCount`).transaction(
  (current) => String((parseInt(current) || 0) + 1)
);
```

This ensures the count increases properly and stays stored as a string (for Firebase compatibility).

---

## 🧮 7. Track Unread Conversations (Global Counter)

A global counter is maintained at:

```
chats/unreadConversations
```

Whenever a chat's `unreadCount` becomes **1** (i.e., it transitions from 0 to 1), the counter is incremented:

```js
if (unreadCount === 1) {
  await unreadConvRef.transaction(
    (current) => (parseInt(current) || 0) + 1
  );
}
```

This gives a total count of how many chats have unread messages.

---

## 📦 Additional Stored Fields

* `profileName`: Stored at `chats/{phoneNumber}/profileName`
* `phoneNumber`: Redundantly stored at `chats/{phoneNumber}/phoneNumber`

These help in listing and filtering chats quickly.

---

## 🔄 Message Status Updates via Webhook

The webhook listens for delivery status updates:

```js
const statuses = changes?.statuses;
if (statuses && statuses.length > 0) {
  const status = statuses[0].status; // sent, delivered, read
  const recipientId = statuses[0].recipient_id;

  if (status === "read") {
    await db.ref(`chats/${recipientId}/unreadCount`).set(0);
  }
}
```

### 🟢 Purpose:

* Marks messages as read by setting `unreadCount = 0`
* (Optional) You can store status like "sent" or "delivered" under each message if needed

---

## 📍 Firebase Paths Used

* `chats/{phoneNumber}/messages`
* `chats/{phoneNumber}/lastMessage`
* `chats/{phoneNumber}/unreadCount`
* `chats/{phoneNumber}/profileName`
* `chats/unreadConversations`

---

## 📣 Summary

| Feature                 | Description                            |
| ----------------------- | -------------------------------------- |
| 🗃 Message Storage      | Saves messages under each phone number |
| 🧠 Form Handling        | Stores forms and sends alerts          |
| 🔘 Interactive Msgs     | Converts to readable log               |
| 🕔 Last Message         | Stores preview-friendly meta           |
| 🔕 Notifications        | Sent for all incoming messages         |
| 📊 Unread Count         | Tracks unseen messages per user        |
| 📈 Unread Conversations | Tracks total unread chat threads       |

---

> ✅ **Robust, Real-Time, and Scalable** — this logic ensures all chat metadata is live, accurate, and push-friendly.
