# ✈️ Trip Search API

This API helps customers (buyers) find available traveler trips who are moving from a desired **source (buy from)** location to a **destination (delivery to)** location. This aligns with the buyer’s perspective rather than the traveler's.

---

## 🔗 Endpoint

```

GET /xenogate/partner/trip/list/

```

---

## 🧾 Query Parameters

| Parameter | Type   | Required | Description                                    |
| --------- | ------ | -------- | ---------------------------------------------- |
| `from`    | string | Optional | The location the customer wants to buy from    |
| `to`      | string | Optional | The location where the customer wants delivery |

- If both parameters are provided, the trips are filtered accordingly.
- If **no query params** are given, the API returns the latest 200 active trips (sorted by return date).

---

## ✅ Example Request

```

GET /xenogate/partner/trip/search/?from=Dubai\&to=Bangladesh

```

---

## ✅ Successful Response

```json
{
  "message": "2 trips found",
  "results": [
    {
      "id": "abc123_xyz456",
      "userId": "user_firebase_uid",
      "travelerName": "John Doe",
      "travelerEmail": "john@example.com",
      "travelerPhone": "971500000000",
      "departureDate": 1747684740000,
      "departureDateStr": "Mon, 19 May",
      "returnDate": 1747511940000,
      "returnDateStr": "Sat, 17 May",
      "isKYCVerified": true,
      "isActive": true,
      "isOneWay": true,
      "createdAt": 1745491816574,
      "shpperRole": "",
      "hotelName": null,
      "hotelCheckInDate": null,
      "hotelCheckOutDate": null,
      "from": {
        "location": "Dubai, United Arab Emirates",
        "country": "United Arab Emirates",
        "countryCode": "AE",
        "region": "AS",
        "searchTerms": ["dubai", "uae"],
        "photo": "https://shpper-city.s3.../Dubai.jpg"
      },
      "to": {
        "location": "Dhaka, Bangladesh",
        "country": "Bangladesh",
        "countryCode": "BD",
        "region": "AS",
        "searchTerms": ["dhaka", "bangladesh"],
        "photo": "https://shpper-city.s3.../Dhaka.jpg"
      }
    }
  ]
}
```

---

## ❌ Missing Params Example

If neither `from` nor `to` is provided:

```bash
GET /xenogate/partner/trip/search/
```

Returns:

```json
{
  "message": "24 trips found",
  "results": [ ... latest 200 active trips ... ]
}
```

---

## ⚠️ Error Response

```json
{
  "error": "Internal server error: ..." // If unexpected failure
}
```

---

## 🧠 Logic Summary (Important!)

- `from`: Where the customer wants to buy the product from (matches traveler's `from`)
- `to`: Where the customer wants delivery (matches traveler's `to`)
- This model ensures travelers are shown **only if their trip route supports the buyer’s intent**.

---

## 🔁 Example Use Cases

- **User in Bangladesh wants to order something from Dubai:**

  → `from=Dubai&to=Bangladesh`

- **User exploring any incoming trips to UAE from anywhere:**

  → `to=UAE`

---

## 📎 Notes for Frontend Developers

- Location names should match entries in the `searchTerms` array (usually lowercase city or country names).
- For location search or autocomplete, use `/xenogate/partner/location/search/` API.
