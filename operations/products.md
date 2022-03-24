# Products

## Get all products

Returns all products offered together with the specified services.

### Request

`[PlatformAddress]/api/connector/v1/products/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "ServiceIds": [
        "bd26d8db-86da-4f96-9efc-e5a4654a4a94"
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `ServiceIds` | array of string | required, max 1000 items | Unique identifiers of the [Services](services.md#service). |

### Response

```javascript
{
    "Products": [
        {
            "Id": "198bc308-c1f2-4a1c-a827-c41d99d52f3d",
            "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
            "CategoryId": null,
            "IsActive": true,
            "Name": "Breakfast",
            "ExternalName": "Breakfast",
            "ShortName": "BFST",
            "Description": "Nice continental breakfast.",
            "Charging": "PerPersonPerTimeUnit",
            "Posting": "Once",
            "Options": {
                "BillAsPackage": false
            },
            "Promotions": {
                "BeforeCheckIn": false,
                "AfterCheckIn": false,
                "DuringStay": false,
                "BeforeCheckOut": false,
                "AfterCheckOut": false,
                "DuringCheckOut": false
            },
            "Classifications": {
                "Food": false,
                "Beverage": false,
                "Wellness": false,
                "CityTax": false
            },
            "Price": {
                "Currency": "GBP",
                "NetValue": 7.5,
                "GrossValue": 9
                "TaxValues": [
                    {
                        "Code": "UK-S",
                        "Value": 1.50
                    }
                ],
            }
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Products` | array of [Product](#product) | required | Products offered with the service. |

#### Product

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the product. |
| `ServiceId` | string | required | Unique identifier of the [Service](services.md#service). |
| `CategoryId` | string | optional | Unique identifier of the Product category. |
| `IsActive` | boolean | required | Whether the product is still active. |
| `Name` | string | required | Name of the product.  |
| `ExternalName` | string | required | Name of the product meant to be displayed to customer. |
| `ShortName` | string | required | Short name of the product. |
| `Description` | string | optional | Description of the product. |
| `Charging` | string [Product charging](#product-charging) | required | Charging of the product. |
| `Posting` | string [Product posting](#product-posting) | required | Posting of the product. |
| `Options` | [Product options](#product-options) | required | Options of the product. |
| `Promotions` | [Promotions](services.md#promotions) | required | Promotions of the service. |
| `Classifications` | [Product classifications](#product-classifications) | required | Classifications of the service. |
| `Price` | [Currency value](accountingitems.md#currency-value) | required | Price of the product. |

#### Product charging

* `Once`
* `PerTimeUnit`
* `PerPersonPerTimeUnit`
* `PerPerson`

#### Product posting

* `Once`
* `Daily`

#### Product options

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `BillAsPackage` | boolean | required | Product should be displayed as part of a package. |

#### Product classifications

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Food` | boolean | required | Product is classified as food. |
| `Beverage` | boolean | required | Product is classified as beverage. |
| `Wellness` | boolean | required | Product is classified as wellness. |
| `CityTax` | boolean | required | Product is classified as city tax. |
