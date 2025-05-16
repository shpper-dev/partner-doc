# 🌍 Location Search API Documentation

### ✨ Note

Use this API during request creation to **search and select locations**. A single location must be selected from **either region, country, or city** per search. To attach multiple locations to a request, make multiple search calls and select results.

---

## ⚖️ Endpoint

**GET** `/xenogate/partner/location/search/?search={query}`

---

## ✍️ Query Parameters

| Name   | Type   | Required | Description              |
| ------ | ------ | -------- | ------------------------ |
| search | string | Yes      | The search query keyword |

---

## 📅 Sample Usage

### Request

```
GET /xenogate/partner/location/search/?search=kabul
```

### Success Response

```json
{
  "region": [],
  "country": [],
  "city": [
    {
      "en": "Kabul",
      "ar": "كابول",
      "country": "Afghanistan",
      "region": "AS",
      "searchTerm": "kabul"
    }
  ]
}
```

---

## 🌐 Other Examples

### Example 2: `search=BANG`

```json
{
  "region": [],
  "country": [
    {
      "en": "Bangladesh",
      "ar": "بنغلاديش",
      "country": "Bangladesh",
      "region": null,
      "searchTerm": "Bangladesh"
    }
  ],
  "city": [
    {
      "en": "Lubango",
      "ar": "لوبانغو",
      "country": "Angola",
      "region": "AF",
      "searchTerm": "lubango"
    },
    {
      "en": "Battambang",
      "ar": "باتامبانج",
      "country": "Cambodia",
      "region": "AS",
      "searchTerm": "battambang"
    },
    {
      "en": "Bangui",
      "ar": "بانجوي",
      "country": "Central African Republic",
      "region": "AF",
      "searchTerm": "bangui"
    },
    {
      "en": "Bangda",
      "ar": "بانجدا",
      "country": "China",
      "region": "AS",
      "searchTerm": "bangda"
    },
    {
      "en": "Bangor",
      "ar": "بانجور",
      "country": "France",
      "region": "EU",
      "searchTerm": "bangor"
    }
  ]
}
```

### Example 3: `search=EU`

```json
{
  "region": [
    {
      "en": "Europe",
      "ar": "أوروبا",
      "country": null,
      "region": "EU",
      "searchTerm": "europe"
    }
  ],
  "country": [
    {
      "en": "Reunion",
      "ar": "ريونيون",
      "country": "Reunion",
      "region": null,
      "searchTerm": "Reunion"
    }
  ],
  "city": [
    {
      "en": "El Atteuf",
      "ar": "العطف",
      "country": "Algeria",
      "region": "AF",
      "searchTerm": "el atteuf"
    },
    {
      "en": "Neuquen",
      "ar": "نيوكوين",
      "country": "Argentina",
      "region": "SA",
      "searchTerm": "neuquen"
    },
    {
      "en": "Eleuthera Island",
      "ar": "جزيرة إليوثيرا",
      "country": "Bahamas",
      "region": "US",
      "searchTerm": "eleuthera island"
    },
    {
      "en": "North Eleuthera",
      "ar": "نورث إليوثيرا",
      "country": "Bahamas",
      "region": "US",
      "searchTerm": "north eleuthera"
    },
    {
      "en": "Sint Eustatius",
      "ar": "سانت أوستاتيوس",
      "country": "Bonaire",
      "region": "US",
      "searchTerm": "sint eustatius"
    }
  ]
}
```

---

## ⚠️ Error Response

```json
{
  "detail": "Query param 'search' is required."
}
```
