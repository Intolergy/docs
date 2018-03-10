
# Intolergy backend (API documentation)

## User

+ POST /api/signup
  - Description: Create new user,
  - Client: JSONObject ApiClient.login (JSONObject json),
  - Messages:
    ```js
      Request {
        name: 'test',
        password: 'testtest',
        intolerances: 'gluten, lactosa',
        admin: true || false
      }
      Response {
        error: false,
        code: 200,
        data: {}
      }
    ```

+ POST /api/login
  - Description: log in user,
  - Client: JSONObject ApiClient.signup (JSONObject json),
  - Messages:
    ```js
      Request {
        name: 'test',
        password: 'testtest'
      }
      Response {
        error: false,
        code: 200,
        data: {}
      }
    ```

+ POST /api/logout
  - Description: Log out user,
  - ApiClient: Not Implemented as it is not used yet,
  - Messages:
    ```js
      Request {}
      Response {
        error: false,
        code: 301,
        data: {}
      }
    ```

+ GET /api/user (admin)
  - Description: Get all users if you are logged and are an admin user,
  - ApiClient: Not implemented, only for debugging purposes,
  - Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: [{
          id: '90ue0f9uqew8',
          name: 'test',
          password: 'sadkfj92983fh92o3i8hfc89awy8oa37fg98ga9',
          admin: false,
          intolerances: 'gluten, lactosa'
        }]
      }
    ```

## Post

+ GET /api/post (auth)
  - Description: Get all posts (not paginated yet),
  - ApiClient: JSONObject getPosts (JSONObject queries),
  - Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: [{
          id: 1,
          title: 'Titulo post',
          body: 'Cuerpo del post',
          fk_user: 'usuario',
          image: null
        }]
      }
    ```

+ POST /api/post (admin)
  - Description: create post,
  - ApiClient: JSONObject postPlace (JSONObject body),
  - Messages:
    ```js
      Request {
        title: 'Titulo',
        body: 'Cuerpo del post',
        image: 'http://www.image.com' || null
      }
      Response {
        error: false,
        code: 200,
        data: {}
      }
    ```

## Place

+ GET /api/place (auth),
  - Description: List all places (not paginated yet),
  - ApiClient: JSONObject getPlaces (JSONObject body),
  - Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: [{
          name: 'Restaurante',
          latitude: 23.23434,
          longitude: 43.128712,
          description: 'Descripcion lugar',
          image: null,
          intolerances: 'gluten'
        }]
      }
    ```

+ POST /api/place (auth)
  - Description: Create place,
  - ApiClient: JSONObject postPlace (JSONObject body),
  - Messages:
    ```js
      Request {
        name: 'Restaurante',
        latitude: 23.24124,
        longitude: 34.1252,
        description: 'Descripcion de este lugar',
        image: 'http://www.image.com' || null,
        intolerances: 'gluten, lactosa'
      }
      Response {
        error: false,
        code: 200,
        data: {}
      }
    ```

## Product

+ GET /api/product (auth)
  - Description: List all products (not paginated yet),
  - ApiClient: JSONObject getProducts (JSONObject queries),
  - Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: [{
          name: 'Colacao',
          gtin: 123817287,
          description: 'Descripcion colacao',
          image: null,
          intolerances: 'gluten, lactosa'
        }]
      }
    ```

+ POST /api/product (auth)
  - Description: Create product,
  - ApiClient: JSONObject postProduct (JSONObject body),
  - Messages:
    ```js
      Request {
        name: 'Colacao',
        gtin: 123817287,
        description: 'Descripcion colacao',
        image: null,
        intolerances: 'gluten, lactosa'
      }
      Response {
        error: false,
        code: 200,
        data: {}
      }
    ```

## Vote

+ GET /api/vote/post/:id (auth)
  - Description: Get all votes for post with id == :id,
  - ApiClient: JSONObject getPostVotes (Integer id),
  - Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: {
          positive: 30,
          negative: 2
        }
      }
    ```

+ GET /api/vote/place/:id (auth)
  - Description: Get all votes for place with id == :id,
  - ApiClient: JSONObject getPlaceVotes (Integer id),
  - Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: {
          positive: 3,
          negative: 20
        }
      }
    ```

+ GET /api/vote/product/:id (auth)
  - Description: Get all votes for product with id =) :id,
  - ApiClient: JSONObject getProductVotes (Integer id),
  - Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: {
          positive: 105,
          negative: 42
        }
      }
    ```

+ POST /api/vote (auth)
  - Description: Create/update vote of any type,
  - ApiClient: JSONObject postVote (String type, Integer id, Boolean value),
    + type: 'place' || 'product' || 'post',
    + value: true => 1 => positive, false => -1 => negative
  - Messages:
    ```js
      Request {
        type: 'product' || 'place' || 'post',
        id: 12,
        value: 1 || -1
      }
    ```

## Carrefour

+ GET /api/product/carrefour?q=nutell
  - Description: Endpoint to look for products in the carrefour api. The query params is 'q'.
  - ApiClient: Not yet implemented
  - Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: [{
          "gtin": "8000500082379",
          "brand": "NUTELLA",
          "capacity_factor": 1,
          "capacity_unit": "KG",
          "capacity_volume": 1,
          "category_structures": {
            "hyper": {
              "hypUbDesc": "PATE A TARTINER > 500G",
              "hypClassDesc": "PATES A TARTINER",
              "hypUbKey": "1404002",
              "hypGrpClassKey": "140",
              "hypSectorDesc": "PGC",
              "hypDepartmentDesc": "EPICERIE",
              "hypSectorKey": "1",
              "hypSubClassDesc": "PATE A TARTINER",
              "hypGrpClassDesc": "PDTS POUR PETITS DEJEUNERS",
              "hypDepartmentKey": "14",
              "hypClassKey": "1404",
              "hypSubClassKey": "14040"
            },
            "proxy": {
              "prxShoDepartmentDesc": "EPICERIE",
              "prxShoDepartmentKey": "01",
              "prxSubClassDesc": "PATE A TARTINER",
              "prxShoSectorKey": "01",
              "prxGrpClassKey": "027",
              "prxHahSectorDesc": "EPICERIE",
              "prxClassKey": "232",
              "prxHahDepartmentKey": "01",
              "prxUbDesc": "PATE A TARTINER NOISET.>500G",
              "prxSubClassKey": "232006",
              "prxGrpClassDesc": "CONFITURE/P.A.T./MIEL",
              "prxClassDesc": "CONFIT. PATES A TARTINER MIEL",
              "prxUbKey": "23200632",
              "prxHahDepartmentDesc": "EPICERIE",
              "prxShoSectorDesc": "P. G. C.",
              "prxHahSectorKey": "01"
            },
            "super": {
              "supDepartmentKey": "01",
              "supSubClassKey": "120005",
              "supSectorKey": "1",
              "supClassKey": "120",
              "supSectorDesc": "DENREES NON PERISSABLES",
              "supGrpClassDesc": "CONFITURES",
              "supClassDesc": "CONFITURES",
              "supSubClassDesc": "PATES A TARTINER",
              "supUbKey": "12000501",
              "supDepartmentDesc": "EPICERIE",
              "supGrpClassKey": "120",
              "supUbDesc": "PATES A TARTINER"
            }
          },
          "description": "POT 1KG NUTELLA SLEEVE NOEL",
          "name": "NUTELLA SLEEVE"
        }]
      }
    ```

+ GET /api/product/carrefour/:gtin
  + Description: Retrive a product of the carrefour database by gtin,
  + ApiClient: Not yet implemented,
  + Messages:
    ```js
      Response {
        error: false,
        code: 200,
        data: {
          "gtin": [
            "8000500082379"
          ],
          "brand": [
            "NUTELLA"
          ],
          "description": [
            "POT 1KG NUTELLA SLEEVE NOEL"
          ],
          "name": [
            "NUTELLA SLEEVE"
          ],
          "capacity_factor": [
            1
          ],
          "capacity_unit": [
            "KG"
          ],
          "capacity_volume": [
            1
          ],
          "category_structures": {
            "hyper": [
              {
                "hypUbDesc": "PATE A TARTINER > 500G",
                "hypClassDesc": "PATES A TARTINER",
                "hypUbKey": "1404002",
                "hypGrpClassKey": "140",
                "hypSectorDesc": "PGC",
                "hypDepartmentDesc": "EPICERIE",
                "hypSectorKey": "1",
                "hypSubClassDesc": "PATE A TARTINER",
                "hypGrpClassDesc": "PDTS POUR PETITS DEJEUNERS",
                "hypDepartmentKey": "14",
                "hypClassKey": "1404",
                "hypSubClassKey": "14040"
              }
            ],
            "super": [
              {
                "supDepartmentKey": "01",
                "supSubClassKey": "120005",
                "supSectorKey": "1",
                "supClassKey": "120",
                "supSectorDesc": "DENREES NON PERISSABLES",
                "supGrpClassDesc": "CONFITURES",
                "supClassDesc": "CONFITURES",
                "supSubClassDesc": "PATES A TARTINER",
                "supUbKey": "12000501",
                "supDepartmentDesc": "EPICERIE",
                "supGrpClassKey": "120",
                "supUbDesc": "PATES A TARTINER"
              }
            ],
            "proxy": [
              {
                "prxShoDepartmentDesc": "EPICERIE",
                "prxShoDepartmentKey": "01",
                "prxSubClassDesc": "PATE A TARTINER",
                "prxShoSectorKey": "01",
                "prxGrpClassKey": "027",
                "prxHahSectorDesc": "EPICERIE",
                "prxClassKey": "232",
                "prxHahDepartmentKey": "01",
                "prxUbDesc": "PATE A TARTINER NOISET.>500G",
                "prxSubClassKey": "232006",
                "prxGrpClassDesc": "CONFITURE/P.A.T./MIEL",
                "prxClassDesc": "CONFIT. PATES A TARTINER MIEL",
                "prxUbKey": "23200632",
                "prxHahDepartmentDesc": "EPICERIE",
                "prxShoSectorDesc": "P. G. C.",
                "prxHahSectorKey": "01"
              }
            ]
          }
        }
      }
    ```

