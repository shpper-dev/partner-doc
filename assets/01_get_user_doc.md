### 📌 **User Lookup by Email**

**Endpoint:**

```
GET /xenogate/partner/lookup/?email=zahid@example.com
```

**Description:**
Check if a user exists in Authentication by providing their email address. Returns basic user profile information if found.

---

### ✅ **Successful Response**

```json
{
  "customerId": "SUNgX0xwTSZVBlllQlegaIrAYph1",
  "customerEmail": "zahid@example.com",
  "customerName": "Zahid Hasan",
  "customerPhone": "+8801700000000"
}
```

---

### ❌ **Error Response (User Not Found)**

```json
{
  "error": "User not found."
}
```

---

### 🔑 **Query Parameters**

| Parameter | Type   | Required | Description                   |
| --------- | ------ | -------- | ----------------------------- |
| `email`   | string | ✅       | Email address to look up user |

---
