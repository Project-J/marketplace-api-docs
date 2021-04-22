# Fy! Marketplace API - Stock

## Overview
<a name="overview"></a>
The Fy! Marketplace API for Stock allows developers to programmatically create stock updates.

### URI scheme
* *Host:* marketplace-api.iamfy.co
* *Scheme:* HTTPS

### Content type
* Consumes: `application/json`
* Returns: `application/json`

### Operations
* [updateStock](#updatestock)

----

## Paths
<a name="paths"></a>

### `POST` /v0/inventory
<a name="updatestock"></a>

Updates one or more stock items.

|<!--  -->|<!--  -->|
|-|-|
|Operation|`updateStock`|
|Method|`POST`|
|Endpoint|`/v0/inventory`|
<br>
#### Parameters

|Type|Name|Description|Schema|
|-|-|-|-|
|Body|**body** <br>*required*|The request schema for the updateStock operation.|[UpdateStockRequest](#updatestockrequest)|
<br>

For example:

```json
{
	"data": [{
		"sku": "SKU-A",
		"availableStock": 100
	}, {
		"sku": "SKU-B",
		"availableStock": 25
	}]
}
```

#### Responses

An example of a successful (`200`) response from the [updateStock](#updatestock) operation:

```json
{
	"supplier": "acme-inc",
	"success": true,
	"message": "Posted stock update for supplier: acme-inc"
}
```

|Status|Description|Schema|
|-|-|-|
|`200`|Success.|[UpdateStockResponse](#updatestockresponse)|
|`400`|Missing or invalid parameters.|[UpdateStockResponse](#updatestockresponse)|
|`403`|Access forbidden.|[UpdateStockResponse](#updatestockresponse)|
|`500`|Server error.|[UpdateStockResponse](#updatestockresponse)|

----

## Definitions
<a name="definitions"></a>

### UpdateStockRequest
<a name="updatestockrequest"></a>

```
{"data": [<StockUpdate>, ...]}
```

### StockUpdate
<a name="stockupdate"></a>

```
{"sku":             <string>
 "availableStock":  <number>}
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**sku**            <br>*required*|The SKU (stock keeping unit) of the item.|string|
|**availableStock** <br>*required*|The quantity of available stock.|number|

</details>


### UpdateStockResponse
<a name="updatestockresponse"></a>

```
<SuccessResponse> | <Error>
```

<details>
  <summary>View descriptions</summary>

|Name|Description|Schema|
|-|-|-|
|**payload**    <br>*optional*|The payload for the updateStock operation.|[SuccessResponse](#orders)|
|**errors**     <br>*optional*|One or more unexpected errors which occurred during the updateStock operation.|-|

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
