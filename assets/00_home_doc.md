# 📘 Welcome to Shpper Partner API Docs

Welcome, developer! 👋

This is the official documentation hub for integrating with **Shpper’s Partner APIs**. These APIs are designed for external services or admins to:

- Onboard users and manage their delivery addresses
- Create product delivery requests on behalf of customers
- Search for available travelers (trip routes)
- Lookup location or user metadata
- Build automation around the Shpper fulfillment system

---

## 📌 How to Use This Documentation

The sidebar provides links to key feature modules:

| 📁 Section                            | 🧭 Description |
|--------------------------------------|----------------|
| **👤 User Onboarding with Address**  | API to create a new user with their delivery address and preferred currency. |
| **📦 Request Creation**              | API for creating a request (including uploading product images) for existing users. |
| **📮 User Lookup by Email**          | Helps check if a user is already registered in the system. |
| **🗺️ Location Search**              | Fetch locations (regions, countries, cities) that are usable in trip and product request flows. |
| **✈️ Trip Search**                   | Lets you query traveler trips available from-to locations based on the buyer’s intention. |
| **🧾 Request Listing by User ID**    | Fetch recent 5 requests made by a specific user. |
| **📘 You're Here!**                  | This home page guide. |

---

## 🔧 Integration Guidelines

### 1. 🔐 Authentication

All APIs are **public** for trusted backend partner access. No token is required. However, misuse or abuse will result in IP ban.

> *Only authorized services and admin panels should call these APIs.*

---

### 2. ⚙️ Response Structure

- All APIs respond with standard JSON.
- Errors are returned with `error` key and proper status codes.

Example:

```json
{
  "error": "User not found."
}
```

---

### 3. 📷 Image Upload

When creating requests, product images should be passed as **base64 strings**, which are automatically converted to image URLs via AWS S3.

---

### 4. 🧭 Location Selection

Use `/location/search/` for autocomplete functionality before sending location data in:
- Product requests
- Trip search

Use the **`searchTerm`** field from the results when filtering trips or creating payloads.

---

## 📥 Example Workflow

Typical request creation via admin panel:

1. Search or onboard a user via `/onboard/`
2. Add delivery address (if not provided in onboarding)
3. Use `/location/search/` to suggest `productLocations`
4. Create a request via `/request/create/`
5. View it using `/request/list/?uid=...`

---

## 🤝 Contact & Support

Need help? Reach out to the Shpper team at:

📧 **support@shpper.net**  
🌐 [www.shpper.net](https://www.shpper.net)

Let’s build something amazing 🚀
