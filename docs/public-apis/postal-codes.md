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

## Get a single postal code
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