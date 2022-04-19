# Postal Codes

Devos provides an open API for retrieving information about Norwegian postal codes. The data comes from [Bring](https://www.bring.no/tjenester/adressetjenester/postnummer)'s postal code registry.

The base URL for all these requests is:
```
https://api.devos.no/v1/public/postal-codes/
```

## Objects

### County
The `County` object represents a Norwegian county.
```
{
  "id": String,
  "name": String,
  "county_code": String
}
```

### Municipality
The `Municipality` object represents a Norwegian municipality. It belongs to a `County`.
```
{
  "id": String,
  "name": String,
  "municipality_code": String,
  "county: County
}
```

### City
The `City` object represents a Norwegian city or place. It belongs to a `Municipality`.
```
{
  "id": String,
  "name": String,
  "municipality": Municipality
}
```

### Postal Code
The `Postal Code` object represents the actual postal code. It belongs to a `City` and a `Type`.
```
{
  "id": String,
  "postal_code": String,
  "city": City,
  "type": Type
}
```

### Type
The `Type` object represents the type of the postal code. 
```
{
  "id": String,
  "identifier": String,
  "name": String
}
```

It can be one of the following (in Norwegian):
```
B = Både gateadresser og postbokser
F = Flere bruksområder (felles)
G = Gateadresser (og stedsadresser), dvs. “grønne postkasser”
P = Postbokser
S = Servicepostnummer (disse postnumrene er ikke i bruk til postadresser)
```

## API Reference
### Get a single postal code
```curl
GET /:postal_code
```

```json
{
  "id": "edf3550e-8478-4f6e-a79a-c5d6606ca8e8",
  "postal_code": "4842",
  "city": {
    "id": "fa5cee47-7684-4a12-863f-f4d1f1e0bfa7",
    "name": "ARENDAL",
    "municipality": {
      "id": "e57d7fd4-73cd-4c9f-8a88-008690f1d3c8",
      "name": "ARENDAL",
      "municipality_code": "4203",
      "county": {
        "id": "d75d060e-3c93-4a5f-b26d-73118100c50c",
        "name": "Agder",
        "county_code": "42"
      }
    }
  },
  "type": {
    "id": "05ad696c-c5d0-442f-8349-91d09552e266",
    "identifier": "G",
    "name": "Gateadresser"
  }
}
```

### Get all counties
```curl
GET /counties
```

```json
[
  {
    "id": "394344af-67ed-4a3e-9ee2-0f9ca2237344",
    "name": "Svalbard"
  },
  {
    "id": "77626fb4-26cc-4436-b949-34c3a804ae00",
    "name": "Jan Mayen"
  },
  {
    "id": "0f0944ab-19c5-41fd-9630-b23b1be61f9c",
    "name": "Oslo"
  }
  ...
]
```

### Get a specific county
This will also return a list of all the [municipalities](#municipality) belonging to this county.

```curl
GET /counties/:id
```

```json
{
  "id": "1a4a0eed-4bce-4e76-921b-3eb4c7847a5d",
  "municipalities": [
    {
      "id": "19ba6268-d95a-4f96-bc7d-7316e5680bb3",
      "name": "FRØYA"
    },
    {
      "id": "724e60bc-0aba-41d8-a573-52b604978578",
      "name": "SELBU"
    },
    {
      "id": "b8813f93-4f3f-4fc3-ab73-061c235e13ea",
      "name": "SNÅSA"
    }
    ...
  ],
  "name": "Trøndelag"
}
```

### Get all municipalities
```curl
GET /municipalities
```

```json
[
  {
    "id": "d5dc0b4a-726e-4c0b-967e-af2319d3454e",
    "name": "OSLO"
  },
  {
    "id": "20d73c5a-fac1-4ada-94d7-76a7c1cf6d94",
    "name": "BÆRUM"
  },
  {
    "id": "b14f3b66-549b-4837-b53c-0b7ee1cced26",
    "name": "ASKER"
  }
  ...
]
```

### Get a specific municipality
This will also return a list of all the [cities](#city) belonging to this municipality.

```curl
GET /municipalities/:id
```

```json
{
  "cities": [
    {
      "id": "5555c298-82d2-403f-99e1-92949c3220d4",
      "name": "NESODDTANGEN"
    },
    {
      "id": "88423023-1614-4055-addb-1fef0e08deb8",
      "name": "BJØRNEMYR"
    }
    ...
  ],
  "id": "8bd668b8-f3d4-42be-900e-2368bd6ac3a0",
  "name": "NESODDEN"
}
```

### Get all cities
```curl
GET /cities
```

```json
[
  {
    "id": "0d16641b-eb43-416c-a0a9-1639bd3431df",
    "name": "OSLO"
  },
  {
    "id": "0882131c-09fb-4b44-82b8-c3587520acd0",
    "name": "SANDVIKA"
  },
  {
    "id": "e15ddb05-611c-4cda-960d-3226913739da",
    "name": "HASLUM"
  }
  ...
]
```

### Get a specific city
This will also return a list of all the [postal codes](#postal-code) belonging to this city.

```curl
GET /cities/:id
```

```json
{
  "id": "cfc319b8-cd01-4871-a3cb-0be8045612b2",
  "name": "LANGHUS",
  "postal_codes": [
    {
      "id": "3ace675f-0e58-41cf-85c5-a3b4a91c80f2",
      "postal_code": "1403"
    },
    {
      "id": "94fde050-c62c-48bb-9d97-4a4f33914ad5",
      "postal_code": "1405"
    }
  ]
}
```