# 📦 Get User's Latest Requests

This endpoint retrieves the **latest 5 requests** created by a specific user. If more requests exist, users are encouraged to install the Shpper app to view the full list.

---

### 🔗 Endpoint

```
GET xenogate/partner/request/list/?uid=<FIREBASE_USER_ID>
```

---

### 🧾 Query Parameters

| Parameter | Type   | Required | Description                       |
| --------- | ------ | -------- | --------------------------------- |
| uid       | string | ✅ Yes   | Firebase UID of the customer user |

---

### ✅ Success Response (200)

```json
{
  "latestRequests": [
    {
      "id": "SUNgX0xwTSZVBlllQlegaIrAYph1_1747383624905",
      "customerId": "SUNgX0xwTSZVBlllQlegaIrAYph1",
      "customerName": "Zahid Hasan",
      "customerEmail": "zahid@example.com",
      "customerPhone": "8801700000000",
      "deliveryAddress": {
        "type": "Home",
        "formattedAddress": "Q953+49F, Dhaka, Bangladesh",
        "lat": 23.757921,
        "lng": 90.3535845,
        "address1": "House 10",
        "address2": "Road 5",
        "city": "Dhaka",
        "postalCode": "1207",
        "buildingName": "Shahriar Heights",
        "floor": "5",
        "apartment": "C",
        "specialLandmark": "Near Dhaka University",
        "country": {
          "en": "Bangladesh",
          "ar": "بنغلاديش",
          "code": "BD"
        },
        "isDefault": true,
        "userId": "SUNgX0xwTSZVBlllQlegaIrAYph1",
        "id": "Home1747370012202",
        "createdAt": 1747370012202
      },
      "products": [
        {
          "id": "SUNgX0xwTSZVBlllQlegaIrAYph1_1747383618363_0",
          "name": "Product Testing",
          "quantity": 1,
          "price": 1200,
          "totalProductPrice": 1200,
          "details": "This is a test request from developer side",
          "url": "",
          "images": [
            "https://shppermedia.s3.us-east-1.amazonaws.com/media/product_images/..."
          ],
          "isOnline": true,
          "actualCurrency": {
            "cc": "USD",
            "flag": "🇦🇪",
            "name": "UAE dirham",
            "symbol": "د.إ;"
          },
          "targetCurrency": {
            "cc": "USD",
            "flag": "🇦🇪",
            "name": "UAE dirham",
            "symbol": "د.إ;"
          },
          "conversionRate": 1
        }
      ],
      "productLocations": [
        {
          "en": "Kabul",
          "ar": "كابول",
          "country": "Afghanistan",
          "region": "AS",
          "searchTerm": "kabul"
        }
      ],
      "totalProductPrice": 1200,
      "commission": 96,
      "totalRequestPrice": 1296,
      "searchTerms": [],
      "removeBox": false,
      "removeTags": false,
      "over2kg": false,
      "isLiquidTobacco": false,
      "isAgreedToPriceTerms": true,
      "isArchived": false,
      "isGlobal": true,
      "status": "published",
      "isFromTripBanner": false,
      "selectedTrips": [],
      "selectedTravelerIds": [],
      "createdAt": 1747383624905
    }
  ],
  "message": "Only recent 5 requests are shown. To explore more, please install Shpper App and sign in."
}
```

---

### ❌ No Requests Found

```json
{
  "latestRequests": [],
  "message": "Only recent 5 requests are shown. To explore more, please install Shpper App and sign in."
}
```

---

### ❌ Missing Query Parameter

```json
{
  "error": "user Id is required as a query parameter."
}
```
