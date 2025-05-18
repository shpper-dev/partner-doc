# 📑 Shpper - Request Creation API Documentation

This guide helps frontend developers integrate with the **Create Request API** of Shpper's partner interface.

---

## ✨ Endpoint

**POST** `/xenogate/partner/request/create/`

Use this endpoint to create a new request from the frontend or 3rd-party source (e.g., BoxIt).

---

## ✉ Headers

```
Content-Type: application/json
```

---

## 🖊️ Payload Example

```json
{
  "customerId": "SUNgX0xwTSZVBlllQlegaIrAYph1",
  "customerName": "Zahid Hasan",
  "customerEmail": "zahid@example.com",
  "customerPhone": "8801700000000",
  "products": [
    {
      "name": "Product Testing",
      "details": "This is a test request from developer side",
      "images": [
        "<base64_encoded_string>"
      ],
      "quantity": 1,
      "price": 1200,
      "url": "",
      "isOnline": true
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
  "searchTerms": [],
  "removeBox": false,
  "removeTags": false,
  "over2kg": false,
  "isLiquidTobacco": false,
  "isAgreedToPriceTerms": true,
  "selectedTrips": [],
  "selectedTravelerIds": [],
  "isFromTripBanner": false
}
```

### 🔎 Notes:

* `customerId`: Firebase UID (must match delivery address owner)
* `images[]`: Base64 strings, backend will upload them to AWS S3.
* `productLocations[]`: Each location must contain an English name (`en`) used for trip matching.
* `selectedTrips` / `selectedTravelerIds`: Leave empty if you want backend to auto-match.

---

## ✅ Successful Response

```json
{
  "status": "success",
  "requestId": "SUNgX0xwTSZVBlllQlegaIrAYph1_1747376289343",
  "message": "Your request has been created, Please Install Shpper App for explore your Offers from the Travelers"
}
```

---

## ❌ Error Responses

* `400 Bad Request` with:

```json
{ "error": "No default delivery address found for this user." }
```

* Or any validation issues like:

```json
{ "error": "price and quantity required" }
```

---

## ⚖️ Important Behaviors

* The backend **auto-calculates commission and total price**.
* If no trips are provided, **it automatically matches trips** using `TripSearchService`.
* Image uploads happen per-product to path: `requests/{request_id}/{product_id}/{index}.jpg`
* The response includes a **globally unique request ID**.

---

## 🛠️ Dev Notes

* Make sure the user **already has a default delivery address** in Firestore `/users/{uid}/address_book`.
* The `products[].images[]` should be a **list of base64 strings** (not objects).
* You can reuse this flow to integrate with external stores, chatbot frontends, or mobile apps.

---

## ☑️ Next Step for Users

Once the request is created, direct users to:

**[https://www.shpper.net/en](https://www.shpper.net/en)**
To manage their requests and connect with matched travelers.

---

For support or API key authentication concerns, please contact the backend team or open a ticket in the developer portal.

