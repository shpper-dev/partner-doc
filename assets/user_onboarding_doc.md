# 🧑‍💼 User Onboarding API Documentation

This API is used to onboard a new user into the Shpper system. It handles Authentication account creation, profile creation in db, wallet initialization, and optionally delivery address storage.

---

## 📍 Endpoint

`POST /xenogate/partner/onboard/`

---

## 📦 Payload (JSON Body)

```json
{
  "firstName": "Zahid",
  "lastName": "Hasan",
  "email": "zahid@example.com",
  "phoneNumber": "8801700000000",
  "country": "Bangladesh",
  "deliveryAddress": {
    "type": "Home",
    "formattedAddress": "Q953+49F, Dhaka, Bangladesh",
    "lat": 23.757921,
    "lng": 90.3535845,
    "isDefault": true,
    "country": "Bangladesh",
    "address1": "House 10",
    "address2": "Road 5",
    "city": "Dhaka",
    "postalCode": "1207",
    "buildingName": "Shahriar Heights",
    "floor": "5",
    "apartment": "C",
    "specialLandmark": "Near Dhaka University"
  }
}
```

> 🔒 If the user already exists by email, the existing account will be used and only a remark will be returned indicating to create an address if missing.

---

## ✅ Successful Response

```json
{
  "id": "SUNgX0xwTSZVBlllQlegaIrAYph1",
  "created": true,
  "Remarks": "User profile Created with a default address"
}
```

---

## ❌ Error Response

```json
{
  "error": "email is required"
}
```

Or:

```json
{
  "error": "User already exists and has no default address. Please create one."
}
```

---

## ⚙️ What Happens Internally?

1. Checks if a user exists using the given email.
2. If not:

   - Creates user in Auth
   - Generates a random password
   - Initializes user profile in User Table
   - Creates user wallet in `wallets` collection
   - Stores address in subcollection `users/{userId}/address_book` if provided
   - Sends a welcome email (in background thread)

3. If user exists:

   - Returns user ID
   - Skips profile re-creation

---

## 💬 Notes

- This API supports one delivery address creation during onboarding
- Country name is converted into structured country info (`{en, ar, code}`) from local JSON asset
- Preferred currency is derived using country code

---

## 📱 Post Onboarding Suggestion

Users are encouraged to download the Shpper app:
🔗 [https://www.shpper.net/en](https://www.shpper.net/en)

The onboarding email contains login credentials and this download prompt automatically.

---

## 🔐 Auth Requirement

This API is intended for internal/partner use — no auth token required by default. Add API key validation middleware if needed.

---

## 👨‍💻 API Maintainer

- 📧 Contact: Backend Developer Team
- 🧪 Tested via Postman

---

For support or integration issues, reach out to the backend maintainer of Shpper Partner API.
