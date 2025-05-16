## ✈️ Trip Search API - From & To Location

This API allows you to retrieve **available upcoming trips** from Firestore based on `from` and `to` location values. It filters and returns **only active trips** within the next 30 days.

### 🔗 Endpoint

```
GET /xenogate/partner/trip/search/
```

### 🧾 Query Parameters

| Param  | Type   | Required | Description               |
| ------ | ------ | -------- | ------------------------- |
| `from` | string | ✅ Yes   | Departure location name   |
| `to`   | string | ✅ Yes   | Destination location name |

### ✅ Success Response

Returns a list of trips that match the criteria.

#### Example Request

```
GET /xenogate/partner/trip/search/?from=Bangladesh&to=Dubai
```

#### Example Response

```json
{
  "results": [
    {
      "id": "TRAVELER_ID_TIMESTAMP_INDEX",
      "userId": "Firebase UID",
      "travelerName": "Traveler Full Name",
      "travelerEmail": "email@example.com",
      "travelerPhone": "+971XXXXXXXXX",
      "from": {
        "location": "Dhaka, Bangladesh",
        "country": "Bangladesh",
        "code": "DAC",
        "region": "AS",
        "photo": "https://.../Dhaka.jpg",
        "searchTerms": ["dhaka", "bangladesh"]
      },
      "to": {
        "location": "Dubai, United Arab Emirates",
        "country": "United Arab Emirates",
        "code": "DXB",
        "region": "AS",
        "photo": "https://.../Dubai.jpg",
        "searchTerms": ["dubai", "uae"]
      },
      "departureDate": 1748520000000,
      "returnDate": 1748433600000,
      "departureDateStr": "Thu, 29 May",
      "returnDateStr": "Wed, 28 May",
      "isActive": true,
      "isKYCVerified": true,
      "isOneWay": true,
      "hotelName": null,
      "hotelCheckInDate": null,
      "hotelCheckOutDate": null,
      "shpperRole": "",
      "createdAt": 1746348967971
    }
  ]
}
```

### ❌ Error Responses

#### Missing Query Parameters

````json
{
  "error": "'from' and 'to' query parameters are required."
}

#### Internal Error
```json
{
  "error": "Internal server error occurred."
}

### 📝 Notes
- Trips are filtered by `isActive = true`.
- Only trips returning within **30 days from today** are considered.
- `from` and `to` locations are matched against search terms.
- Results are sorted by return date ascending.

### 🔁 Related
- Trips are pulled from the `schedule_trips` Firestore collection.
- Firestore composite index might be required for optimal performance (check Firebase console if errors arise).

---
🛫 This endpoint helps buyers discover available trips matching their product destination. Great for powering request-based logistics!

````
