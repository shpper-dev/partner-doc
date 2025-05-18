# Welcome to Shpper Partner API Documentation

Hello Developer!

This is your central hub for understanding and integrating with **Shpper’s Partner APIs**. These endpoints are designed for partners and admin tools to:

- Onboard users and manage addresses
- Create buyer requests with product images
- Search for trips (active trips)
- Look up location and user metadata
- Build automations on top of Shpper’s fulfillment engine

---

## How to Use This Documentation

Use the left sidebar to navigate between major API features:

| Section                          | Description                                                                      |
| -------------------------------- | -------------------------------------------------------------------------------- |
| **API Guide (You’re Here)**      | Entry guide to understand API usage.                                             |
| **User Lookup by Email**         | Check if a user already exists using their email address.                        |
| **User Onboarding with Address** | Create a new user profile along with delivery address and preferred currency.    |
| **Request Creation**             | Create a product delivery request for an existing user (with image support).     |
| **Location Search**              | Get regions, countries, or cities that can be used in trips or product requests. |
| **Trip Search**                  | Find upcoming traveler trips between selected locations.                         |
| **User’s Requests List**         | Fetch the latest 5 requests created by a user.                                   |

---

## Integration Guidelines

### Authentication

All APIs are currently **public** and meant for trusted server-to-server access.

> ❗ Avoid exposing these APIs from public or frontend clients. Abuse may result in access blocks.

---

## 🔐 API Authentication (Important)

All requests must include a valid API Key in the request header.

> Missing or invalid API keys will result in a 403 Forbidden response.

### 🔑 Header Format

```http
Authorization: Api-Key DqZWqMQu.IzyuZ6FZu8ZRm7CJAloecnBJkzXcWf4Z
```

---

### Response Format

All endpoints return JSON. On error, you'll receive:

```json
{
  "error": "Detailed error message here"
}
```

---

### Image Upload

For product request creation, images are passed as **base64 strings**. These are automatically:

- Uploaded to our media storage
- Replaced with accessible image URLs in the request payload

---

### Location-Based Data

Before submitting product or trip data, use the `/location/search/` API to autocomplete locations.

---

### **Shpper Partner API Endpoints**

| Endpoint                             | Method | Query Params     | Required                     | Description                                                                                                           |
| ------------------------------------ | ------ | ---------------- | ---------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `/xenogate/partner/lookup/`          | `GET`  | `email`          | ✅                           | Get user profile using email (returns user ID, name, phone).                                                          |
| `/xenogate/partner/onboard/`         | `POST` | –                | –                            | Create a user with email, name, phone, country & optional delivery address.                                           |
| `/xenogate/partner/address/create/`  | `POST` | –                | –                            | Add a new delivery address for an existing user.                                                                      |
| `/xenogate/partner/trip/list/`       | `GET`  | `from` <br> `to` | ❌ optional <br> ❌ optional | Search scheduled trips. If both `from` and `to` are given, filtered search. If none provided, lists all active trips. |
| `/xenogate/partner/request/create/`  | `POST` | –                | –                            | Create a product request for a user (requires existing customer ID and default address).                              |
| `/xenogate/partner/request/list/`    | `GET`  | `uid`            | ✅                           | Returns latest 5 product requests for a user.                                                                         |
| `/xenogate/partner/location/search/` | `GET`  | `search`         | ✅                           | Search across custom regions, countries, and cities using search terms.                                               |

---

### Example: Using Query Parameters

- **Lookup User**
  `GET /xenogate/partner/lookup/?email=zahid@example.com`

- **Search Trips with Filters**
  `GET /xenogate/partner/trip/list/?from=Bangladesh&to=Dubai`

- **Search Locations**
  `GET /xenogate/partner/location/search/?search=Dubai`

---

## 📌 Typical Workflow

Here’s a typical flow for creating a product delivery request:

1. **Check if user exists** via `/lookup/?email=...`
2. **Create user** via `/onboard/` if needed
3. **Add address** via `/address/create/` if not already provided
4. **Search locations** via `/location/search/?search=...`
5. **Create request** via `/request/create/`
6. **View latest requests** via `/request/list/?uid=...`

---

## Need Help?

If you're stuck, feel free to contact the Shpper support team:

- 📧 **[support@shpper.net](mailto:support@shpper.net)**
- 🌐 [www.shpper.net](https://www.shpper.net)

Let’s build a better shopping future together
