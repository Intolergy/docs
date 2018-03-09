# [Carrefour API](https://developer.fr.carrefour.io/docs)

## Endpoints

### POST

#### URL

```https://api.fr.carrefour.io/v1/openapi/items```

#### Body

* Look for the word 'nutell' in the brand/item description
  ```json
  {"queries":[{"query":"nutell","field":"barcodeDescription"}]}
  ```

### GET

* Look for the item based on the gtin:
 ```https://api.fr.carrefour.io/v1/openapi/items/{gtin}```

## Headers
```json
{
  "accept": "application/json",
  "content-type": "application/json",
  "x-ibm-client-id": "fe3c3292-3842-4583-8352-88be42d977d9",
  "x-ibm-client-secret": "mR1cW7yK8iV2kG2nP8yA2gU1bA8iP4cO5cP5qX4eF3aP3pM3uM"
}
```

