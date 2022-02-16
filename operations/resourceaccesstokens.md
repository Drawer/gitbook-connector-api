# Resource access tokens

## Get all resource access tokens

Returns all resource access tokens based on resource access tokens, reservations or interval. One of them must be specified in the request.

### Request

`[PlatformAddress]/api/connector/v1/resourceAccessTokens/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "ResourceAccessTokenIds": [
        "90eff5aa-36b4-4689-80c0-ab3a00bb412e"
    ],
    "ServiceOrderIds": [
        "65eff5aa-36b4-4689-80c0-ab3a00bb412e"
    ],
    "CollidingUtc": {
        "StartUtc": "2020-02-15T00:00:00Z",
        "EndUtc": "2020-02-20T00:00:00Z"
    },
    "ActivityStates": [
        "Active"
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `ResourceAccessTokenIds` | array of string | optional, max 1000 items | Unique identifiers of [Resource access tokens](#resource-access-token). Required if no other filter is provided. |
| `ServiceOrderIds` | array of string | optional, max 1000 items | Unique identifiers of service orders (for example [Reservation](reservations.md#reservation)). Required if no other filter is provided. |
| `CollidingUtc` | [Time interval](#time-interval) | optional, max length 3 months | Interval in which the [Resource access token](#resource-access-token) is valid. Required if no other filter is provided. |
| `ActivityStates` | array of string [Activity state](vouchers.md#activity-state) | required | Whether return only active, only deleted or both records. |

#### Time interval

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |

### Response

```javascript
{
    "ResourceAccessTokens": [
        {
            "Id": "72d4b117-1f84-44a3-1f84-8b2c0635ac60",
            "ServiceOrderId": "35d4b117-4e60-44a3-9580-c582117eff98",
            "CompanionshipId": "25d4b117-4e60-44a3-9580-c582117eff98",
            "ResourceId": "65d4b117-4e60-44a3-9580-c582117eff98",
            "Type": "PinCode",
            "Value": "1234#",
            "SerialNumber": null,
            "ValidityStartUtc": "2020-10-09T22:00:00Z",
            "ValidityEndUtc": "2020-10-10T22:00:00Z",
            "Permissions":
            {
                "Bed": true,
                "Room": false,
                "Floor": false,
                "Building": false
            }
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ResourceAccessTokens` | array of [Resource access token](#resource-access-token) | required | Resource access tokens. |

#### Resource access token

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of [Resource access token](#resource-access-token). |
| `ServiceOrderId` | string | required | Unique identifier of a service order (for example [Reservation](reservations.md#reservation)). |
| `CompanionshipId` | string | optional | Unique identifier of [Companionship](companionships.md#companionship). |
| `ResourceId` | string | optional | Unique identifier of [Resource](resources.md#resource). |
| `Type` | [Resource access token type](#resource-access-token-type) | required | Type of stored value. |
| `Value` | string | required | Value of resource access token |
| `SerialNumber` | string | optional | Serial number of [Resource access token type](#resource-access-token-type). |
| `ValidityStartUtc` | string | required | Marks the start of interval in which the resource access token can be used. |
| `ValidityEndUtc` | string | required | Marks the end of interval in which the resource access token can be used. |
| `Permissions` | [Resource access token permissions](#resource-access-token-permissions) | required | Specify permissions of [Resource access token](#resource-access-token). |

#### Resource access token type

* `PinCode`
* `RfidTag`

#### Resource access token permissions

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Bed` | bool | required | Specify whether [Resource access token](#resource-access-token) grants permission to access bed. |
| `Room` | bool | required | Specify whether [Resource access token](#resource-access-token) grants permission to access room. |
| `Floor` | bool | required | Specify whether [Resource access token](#resource-access-token) grants permission to access floor. |
| `Building` | bool | required | Specify whether [Resource access token](#resource-access-token) grants permission to access building. |

## Add resource access tokens

Adds new resource access tokens with the specified data.

### Request

`[PlatformAddress]/api/connector/v1/resourceAccessTokens/add`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "ResourceAccessTokenParameters": [
        {
            "ServiceOrderId": "35d4b117-4e60-44a3-9580-c582117eff98",
            "CompanionshipId": "25d4b117-4e60-44a3-9580-c582117eff98",
            "ResourceId": "65d4b117-4e60-44a3-9580-c582117eff98",
            "Type": "PinCode",
            "Value": "1234#",
            "SerialNumber": null,
            "ValidityStartUtc": "2020-10-09T22:00:00Z",
            "ValidityEndUtc": "2020-10-10T22:00:00Z",
            "Permissions":
            {
                "Bed": { "Value": true },
                "Room": { "Value": false },
                "Floor": { "Value": false },
                "Building": { "Value": false }
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
| `ResourceAccessTokenParameters` | Array of [Resource access token parameter](#resource-access-token-parameter) | required, max 1000 items | Parameters of [Resource access token](#resource-access-token). |

#### Resource access token parameter

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ServiceOrderId` | string | required | Unique identifier of a service order (for example [Reservation](reservations.md#reservation)). |
| `CompanionshipId` | string | optional | Unique identifier of [Companionship](companionships.md#companionship). |
| `ResourceId` | string | optional | Unique identifier of [Resource](resources.md#resource). |
| `Type` | [Resource access token type](#resource-access-token-type) | required | Type of stored value. |
| `Value` | string | required | Value of resource access token |
| `SerialNumber` | string | optional | Serial number of [Resource access token type](#resource-access-token-type). |
| `ValidityStartUtc` | string | required | Marks the start of interval in which the resource access token can be used. |
| `ValidityEndUtc` | string | required | Marks the end of interval in which the resource access token can be used. |
| `Permissions` | [Resource access token permission parameter](#resource-access-token-permission-parameter) | required | Specify permissions of [Resource access token](#resource-access-token). |

#### Resource access token permission parameter

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Bed` | [Bool update value](#bool-update-value) | optional | Specify whether [Resource access token](#resource-access-token) grants permission to access bed. |
| `Room` | [Bool update value](#bool-update-value) | optional | Specify whether [Resource access token](#resource-access-token) grants permission to access room. |
| `Floor` | [Bool update value](#bool-update-value) | optional | Specify whether [Resource access token](#resource-access-token) grants permission to access floor. |
| `Building` | [Bool update value](#bool-update-value) | optional | Specify whether [Resource access token](#resource-access-token) grants permission to access building. |

#### Bool update value

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Value` | bool | optional | Value which is to be updated. |

### Response

```javascript
{
    "ResourceAccessTokens": [
        {
            "Id": "72d4b117-1f84-44a3-1f84-8b2c0635ac60",
            "ServiceOrderId": "35d4b117-4e60-44a3-9580-c582117eff98",
            "CompanionshipId": "25d4b117-4e60-44a3-9580-c582117eff98",
            "ResourceId": "65d4b117-4e60-44a3-9580-c582117eff98",
            "Type": "PinCode",
            "Value": "1234#",
            "SerialNumber": null,
            "ValidityStartUtc": "2020-10-09T22:00:00Z",
            "ValidityEndUtc": "2020-10-10T22:00:00Z",
            "Permissions":
            {
                "Bed": true,
                "Room": false,
                "Floor": false,
                "Building": false
            }
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ResourceAccessTokens` | array of [Resource access token](#resource-access-token) | required | Resource access tokens. |

## Update resource access tokens

Updates the [Resource access token](#resource-access-token) validity interval and [permissions](#resource-access-token-permission-parameter) that it grants.

### Request

`[PlatformAddress]/api/connector/v1/resourceAccessTokens/update`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "ResourceAccessTokenUpdates": [
        {
            "ResourceAccessTokenId": "35d4b117-4e60-44a3-9580-c582117eff98",
            "ValidityStartUtc": { "Value": "2020-10-09T22:00:00Z" },
            "ValidityEndUtc": { "Value": "2020-10-10T22:00:00Z" },
            "Permissions":
            {
                "Bed": { "Value": true },
                "Room": { "Value": false },
                "Floor": { "Value": false },
                "Building": { "Value": false }
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
| `ResourceAccessTokenUpdates` | Array of [Resource access token update](#resource-access-token-update) | required | Parameters of [Resource access token](#resource-access-token). |

#### Resource access token update

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ResourceAccessTokenId` | [String update value](#string-update-value) | required | Unique identifier of [Resource access token](#resource-access-token). |
| `ValidityStartUtc` | [String update value](#string-update-value) | optional | Marks the start of interval in which the resource access token can be used. |
| `ValidityEndUtc` | [String update value](#string-update-value) | optional | Marks the end of interval in which the resource access token can be used. |
| `Permissions` | [Resource access token permission parameter](#resource-access-token-permission-parameter) | optional | Specify permissions of [Resource access token](#resource-access-token). |

#### String update value

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Value` | string | optional | Value which is to be updated. |

### Response

```javascript
{
    "ResourceAccessTokens": [
        {
            "Id": "72d4b117-1f84-44a3-1f84-8b2c0635ac60",
            "ServiceOrderId": "35d4b117-4e60-44a3-9580-c582117eff98",
            "CompanionshipId": "25d4b117-4e60-44a3-9580-c582117eff98",
            "ResourceId": "65d4b117-4e60-44a3-9580-c582117eff98",
            "Type": "PinCode",
            "Value": "1234#",
            "SerialNumber": null,
            "ValidityStartUtc": "2020-10-09T22:00:00Z",
            "ValidityEndUtc": "2020-10-10T22:00:00Z",
            "Permissions":
            {
                "Bed": true,
                "Room": false,
                "Floor": false,
                "Building": false
            }
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ResourceAccessTokens` | array of [Resource access token](#resource-access-token) | required | Resource access tokens. |


## Delete resource access tokens

Delete specified resource access tokens.

### Request

`[PlatformAddress]/api/connector/v1/resourceAccessTokens/delete`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "Ids": [
        "35d4b117-4e60-44a3-9580-c582117eff98"
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `Ids` | Array of string | required | Unique identifiers of [Resource access token](#resource-access-token). |

### Response

```javascript
{}
```
