# Restrictions

## Get all restrictions

Returns all restrictions of the default service provided by the enterprise.

### Request

`[PlatformAddress]/api/connector/v1/restrictions/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "ServiceIds": [
        "bd26d8db-86da-4f96-9efc-e5a4654a4a94"
    ],
    "ResourceCategoryIds": [
        "34c29e73-c8db-4e93-b51b-981e42655e03"
    ],
    "RateIds": [
        "ed4b660b-19d0-434b-9360-a4de2ea42eda"
    ],
    "CollidingUtc": {
        "StartUtc": "2020-02-15T00:00:00Z",
        "EndUtc": "2020-02-20T00:00:00Z"
    },
    "CreatedUtc": {
        "StartUtc": "2020-02-05T00:00:00Z",
        "EndUtc": "2020-02-15T00:00:00Z"
    },
    "UpdatedUtc": {
        "StartUtc": "2020-02-05T00:00:00Z",
        "EndUtc": "2020-02-15T00:00:00Z"
    }
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `ServiceIds` | array of string | required, max 1000 items | Unique identifiers of the [Services](services.md#service) from which the restrictions are requested. |
| `ResourceCategoryIds` | array of string | optional, max 1000 items | Unique identifiers of [Resource categories](resources.md#resource-category). |
| `RateIds` | array of string | optional, max 1000 items | Unique identifiers of [Rates](rates.md#rate). Returns all restrictions that affect given rates (i.e. ones without any [Conditions](#restriction-conditions), ones assigned directly to specified rates, ones assigned to [Rate group](rates.md#rate-group) of specified rates, or ones inherited from base rates).  |
| `BaseRateIds` | array of string | optional, max 1000 items | Unique identifiers of [Rates](rates.md#rate). Returns only those restrictions which have matching `BaseRateId` set in [Conditions](#restriction-conditions). |
| `ExactRateIds` | array of string | optional, max 1000 items | Unique identifiers of [Rates](rates.md#rate). Returns only those restrictions which have matching `ExactRateId` set in [Conditions](#restriction-conditions). |
| `CollidingUtc` | [Time interval](#time-interval) | optional, max length 3 months | Interval in which the [Restriction](#restriction) is active. Required if no other filter is provided. |
| `CreatedUtc` | [Time interval](#time-interval) | optional, max length 3 months | Interval in which the [Restriction](#restriction) was created. |
| `UpdatedUtc` | [Time interval](#time-interval) | optional, max length 3 months | Interval in which the [Restriction](#restriction) was updated. |

#### Time interval

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |

### Response

```javascript
{  
   "Restrictions": [  
      {  
         "Id": "40c24757-c16e-4094-91d3-4ca952e488a1",
         "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
         "ExternalIdentifier": "5678",
         "Conditions": {  
            "Type": "Stay",
            "ExactRateId": "7c7e89d6-69c0-4cce-9d42-35443f2193f3",
            "BaseRateId": null,
            "RateGroupId": null,
            "ResourceCategoryId": "86336EAC-4168-46B1-A544-2A47251BF864",
            "ResourceCategoryType": null,
            "StartUtc": "2018-10-09T00:00:00Z",
            "EndUtc": "2018-10-31T00:00:00Z",
            "Days": [  
               "Saturday",
               "Sunday"
            ]
         },
         "Exceptions": {  
            "MinAdvance": null,
            "MaxAdvance": null,
            "MinLength": "P0M2DT0H0M0S",
            "MaxLength": "P0M7DT0H0M0S",
            "MinPrice": {  
               "Value": 50,
               "Currency": "EUR"
            },
            "MaxPrice": {  
               "Value": 150,
               "Currency": "EUR"
            }
         }
      },
      {  
         "Id": "b40ac4a8-f5da-457d-88fe-7a895e1580ab",
         "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
         "ExternalIdentifier": "5678",
         "Conditions": {  
            "Type": "Start",
            "ExactRateId": null,
            "BaseRateId": "e5b538b1-36e6-43a0-9f5c-103204c7f68e",
            "RateGroupId": null,
            "ResourceCategoryId": null,
            "ResourceCategoryType": "Room",
            "StartUtc": "2018-10-01T00:00:00Z",
            "EndUtc": "2018-10-31T00:00:00Z",
            "Days": [  
               "Monday",
               "Tuesday",
               "Wednesday",
               "Thursday",
               "Friday"
            ]
         },
         "Exceptions": {  
            "MinAdvance": "P0M1DT0H0M0S",
            "MaxAdvance": "P0M3DT0H0M0S",
            "MinLength": null,
            "MaxLength": null,
            "MinPrice": null,
            "MaxPrice": null
         }
      }
   ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Restrictions` | array of [Restriction](#restriction) | required | Restrictions of the default service. |

#### Restriction

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the restriction. |
| `ServiceId` | string | required | Unique identifier of the [Service](services.md#service). |
| `ExternalIdentifier` | string | optional | External identifier of the restriction. |
| `Conditions` | string | required | [Conditions](#restriction-conditions) are rules that must be met by a reservation for the restriction to apply. |
| `Exceptions` | string | optional | [Exceptions](#restriction-exceptions) are rules that prevent the restriction from applying to a reservation, even when all conditions have been met. |

#### Restriction Conditions

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Type` | string | required | [Restriction type](#restriction-type). |
| `ExactRateId` | string | optional | Unique identifier of the restricted exact [Rate](rates.md#rate). |
| `BaseRateId` | string | optional | Unique identifier of the restricted base [Rate](rates.md#rate). |
| `RateGroupId` | string | optional | Unique identifier of the restricted [Rate group](rates.md#rate-group). |
| `ResourceCategoryId` | string | optional | Unique identifier of the restricted [Resource category](resources.md#resource-category). |
| `ResourceCategoryType` | string | optional | Name of the restricted [Resource category type](resources.md#resource-category-type). |
| `StartUtc` | string | optional | Start of the restricted interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | optional | End of the restricted interval in UTC timezone in ISO 8601 format. |
| `Days` | array of string [Day](#day) | required | The restricted days of week. |

#### Restriction Exceptions

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `MinAdvance` | string | optional | The minimum time before the reservation starts, you can reserve in ISO 8601 duration format. |
| `MaxAdvance` | string | optional | The maximum time before the reservation starts, you can reserve in ISO 8601 duration format. |
| `MinLength` | string | optional | Minimal reservation length in ISO 8601 duration format. |
| `MaxLength` | string | optional | Maximal reservation length in ISO 8601 duration format. |
| `MinPrice` | [Currency value](accountingitems.md#currency-value)| optional | Value of the minimum night price. |
| `MaxPrice` | [Currency value](accountingitems.md#currency-value)| optional | Value of the maximum night price. |

#### Day

* `Monday`
* `Tuesday`
* `Wednesday`
* `Thursday`
* `Friday`
* `Saturday`
* `Sunday`

#### Restriction type

* `Stay` - guests can't stay overnight within specified dates.
* `Start`- guests can't check in within specified dates.
* `End` - guests can't check out within specified dates.

## Add restrictions

Adds new restrictions with the specified conditions.

### Request

`[PlatformAddress]/api/connector/v1/restrictions/add`

```javascript
{  
   "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
   "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
   "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
   "Restrictions": [  
      {  
         "Identifier": "1234",
         "ExternalIdentifier": "5678",
         "Conditions": {  
            "Type": "Start",
            "ExactRateId": "7c7e89d6-69c0-4cce-9d42-35443f2193f3",
            "ResourceCategoryId": "86336EAC-4168-46B1-A544-2A47251BF864",
            "Days": [  
               "Friday",
               "Saturday",
               "Sunday"
            ]
         },
         "Exceptions": {  
            "MinLength": "P0M2DT0H0M0S",
            "MaxLength": "P0M7DT0H0M0S",
         }
      },
      {  
         "Identifier": "1235",
         "ExternalIdentifier": "5678",
         "Conditions": {  
            "Type": "Start",
            "BaseRateId": "e5b538b1-36e6-43a0-9f5c-103204c7f68e",
            "Days": [  
               "Friday",
               "Saturday",
               "Sunday"
            ]
         },
         "Exceptions": {  
            "MinAdvance": "P0Y0M1DT0H0M0S",
            "MaxAdvance": "P0Y0M3DT0H0M0S"
         }
      }
   ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `ServiceId` | string | required | Unique identifier of the [Service](services.md#service) restrictions will be added in. |
| `Restrictions` | array of [Restriction parameters](#restriction-parameters) | required | Parameters of restrictions. |

#### Restriction parameters
| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Identifier` | string | optional | Identifier of the restriction within the transaction. |
| `ExternalIdentifier` | string | optional | External identifier of the restriction. |
| `Conditions` | string | required | [Conditions](#restriction-conditions) are rules that must be met by a reservation for the restriction to apply. |
| `Exceptions` | string | optional | [Exceptions](#restriction-exceptions) are rules that prevent the restriction from applying to a reservation, even when all conditions have been met. |

### Response

```javascript
{
   "Restrictions": [
      {
         "Identifier": "1234",
         "Restriction": {
            "Id": "40c24757-c16e-4094-91d3-4ca952e488a1",
            "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
            "ExternalIdentifier": "5678",
            "Conditions": {
               "Type": "Stay",
               "ExactRateId": "7c7e89d6-69c0-4cce-9d42-35443f2193f3",
               "BaseRateId": null,
               "RateGroupId": null,
               "ResourceCategoryId": "86336EAC-4168-46B1-A544-2A47251BF864",
               "ResourceCategoryType": null,
               "StartUtc": "2018-10-09T00:00:00Z",
               "EndUtc": "2018-10-31T00:00:00Z",
               "Days": [
                  "Saturday",
                  "Sunday"
               ]
            },
            "Exceptions": {
               "MinAdvance": null,
               "MaxAdvance": null,
               "MinLength": "P0M2DT0H0M0S",
               "MaxLength": "P0M7DT0H0M0S",
               "MinPrice": null,
               "MaxPrice": null
            }
         }
      },
      {
         "Identifier": "1235",
         "Restriction": {
            "Id": "b40ac4a8-f5da-457d-88fe-7a895e1580ab",
            "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
            "ExternalIdentifier": "5678",
            "Conditions": {
               "Type": "Start",
               "ExactRateId": null,
               "BaseRateId": "e5b538b1-36e6-43a0-9f5c-103204c7f68e",
               "RateGroupId": null,
               "ResourceCategoryId": null,
               "ResourceCategoryType": "Room",
               "StartUtc": "2018-10-01T00:00:00Z",
               "EndUtc": "2018-10-31T00:00:00Z",
               "Days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
               ]
            },
            "Exceptions": {
               "MinAdvance": "P0M1DT0H0M0S",
               "MaxAdvance": "P0M3DT0H0M0S",
               "MinLength": null,
               "MaxLength": null,
               "MinPrice": null,
               "MaxPrice": null
            }
         }
      }
   ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Restrictions` | array of [Added restriction](#added-restriction) | required | The added restrictions. |

#### Added restriction

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Identifier` | string | optional | Identifier of the restriction within the transaction. |
| `Restriction` | [Restriction](#restriction) | required | The added restriction. |

## Delete restrictions

Removes restrictions from the service.

### Request

`[PlatformAddress]/api/connector/v1/restrictions/delete`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "RestrictionIds": [
        "af4949ce-c061-4f27-89f9-5a6a9ef725a7", 
        "e2f8aa29-0c09-4097-801c-7888c9fb57ae"
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `RestrictionIds` | array of string | required | Unique identifiers of the [Restrictions](#restriction). |

### Response

```javascript
{}
```
