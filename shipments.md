# Fy! Marketplace API - Shipments

## Overview
<a name="overview"></a>
The Fy! Marketplace API for Shipments allows developers to programmatically create shipment updates.

### URI scheme
* *Host:* marketplace-api.iamfy.co
* *Scheme:* HTTPS

### Content type
* Consumes: `application/json`
* Returns: `application/json`

### Operations
* [updateShipments](#updateshipments)

----

## Paths
<a name="paths"></a>

### `POST` /shipments
<a name="updateshipments"></a>

Updates one or more shipments.


|<!--  -->|<!--  -->|
|-|-|
|Operation|`updateShipments`|
|Method|`POST`|
|Endpoint|`/shipments`|
<br>

#### Parameters

|Type|Name|Description|Schema|
|-|-|-|-|
|Body|**body** <br>*required*|The request schema for the updateShipments operation.|[UpdateShipmentsRequest](#updateshipmentsrequest)|
<br>

For example:

```json
{
	"data": [{
		"orderReference": "SO-1234",
		"items": [{
			"sku": "SKU-ABC-9000",
			"quantity": 1
		}],
		"courier": "U-Ship",
		"shippedOn": "2021-01-01T00:00:00Z",
		"trackingCode": "XYZ-321"
	}]
}
```

#### Responses

An example of a successful (`200`) response from the [updateShipments](#updateshipments) operation:

```json
{
	"supplier": "acme-inc",
	"success": true,
	"message": "Posted shipment updates for supplier: acme-inc"
}
```

|Status|Description|Schema|
|-|-|-|
|`200`|Success.|[UpdateShipmentsResponse](#updateshipmentsresponse)|
|`400`|Missing or invalid parameters.|[UpdateShipmentsResponse](#updateshipmentsresponse)|
|`403`|Access forbidden.|[UpdateShipmentsResponse](#updateshipmentsresponse)|
|`500`|Server error.|[UpdateShipmentsResponse](#updateshipmentsresponse)|

----

## Definitions
<a name="definitions"></a>

### UpdateShipmentsRequest
<a name="updateshipmentsrequest"></a>

```
{"data": [<ShipmentUpdate>, ...]}
```

### ShipmentUpdate
<a name="shipmentupdate"></a>

```
{"orderReference": <string>
 "items":          <Items>
 "courier":        <string>
 "shippedOn":      <ISO-8601 string>
 "trackingCode":   <string>}
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**orderReference** <br>*required*|The reference for a specific Fy! order: an "SO-" prefix followed by a series of numbers.|string|
|**items**          <br>*required*|The items being shipped.|[Items](#items)|
|**courier**        <br>*required*|The name of the courier handling the shipment.|string|
|**shippedOn**      <br>*required*|The (ISO-8601) datetime when the order was shipped.|string|
|**trackingCode**   <br>*required*|The tracking code associated with the shipment.|string|

</details>

### Items
<a name="items"></a>

```
[<Item>, ...]
```
An array of one or more [Item](#item).

### Item
<a name="item"></a>

```
{"sku"      <string>
 "quantity" <number>}
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**sku**        <br>*required*|The SKU (stock keeping unit) of the item.|string|
|**quantity**   <br>*required*|The quantity of items, usually `1`.|number|

</details>

### UpdateShipmentsResponse
<a name="updateshipmentsresponse"></a>

```
<SuccessResponse> | <Error>
```

<details>
  <summary>View descriptions</summary>

|Name|Description|Schema|
|-|-|-|
|**payload**    <br>*optional*|The payload for the updateShipments operation.|[SuccessResponse](#orders)|
|**errors**     <br>*optional*|One or more unexpected errors which occurred during the updateShipments operation.|-|

</details>

### SuccessResponse
<a name="successresponse"></a>

```
{"supplier": <number>
 "success":  <boolean>
 "message":  <string>}
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**supplier**   <br>*required*|The username of the supplier associated with the corresponding request.|number|
|**success**    <br>*required*|Always `true` for successful responses.|boolean|
|**message**    <br>*required*|A message specifying the update.|string|

</details>


