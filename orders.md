# Fy! Marketplace API - Orders

## Overview
<a name="overview"></a>
The Fy! Marketplace API for Orders allows developers to programmatically retrieve order information.

### URI scheme
* *Host:* marketplace-api.iamfy.co
* *Scheme:* HTTPS

### Content type
* Consumes: `application/json`
* Returns: `application/json`

### Operations
* [getOrders](#getorders)<br>

----

<a name="paths"></a>
## Paths

### `GET` /v0/orders
<a name="getorders"></a>

Returns orders created between the specified `from` and `to` parameters.

|<!--  -->|<!--  -->|
|-|-|
|Operation|`getOrders`|
|Method|`GET`|
|Endpoint|`/v0/orders`|
<br>

#### Parameters

|Type|Name|Description|Schema|
|-|-|-|-|
|Query|**from** <br>*required*|An ISO-8601 date from which to return orders. The from parameter is the exclusive, lower bound of the query range. Must not be in the future.|string|
|Query|**to**   <br>*required*|An ISO-8601 date to which to return orders. The to parameter is the inclusive, upper bound of the query range.|string|
<br>

#### Responses

An example of a successful response from the [getOrders](#getorders) operation:

```json
{
	"data": [{
		"orderReference": "SO-1234",
		"contactDetails": {
			"phone": "+00 123456789",
			"email": "j.doe@example.com"
		},
		"address": {
			"recipient": "Jane Doe",
			"line1": "123 Main Street",
			"line2": "42nd Floor",
			"city": "London",
			"postcode": "E1 2BC",
			"state": null,
			"country": "United Kingdom",
			"company": "Acme Internet"
		},
		"orderLines": [{
			"id": 1234,
			"sku": "SKU-A",
			"quantity": 1,
		}],
		"createdAt": "2021-01-01T00:00:00Z"
	}]
}
```

|Status|Description|Schema|
|-|-|-|
|`200`|Success.|[GetOrdersResponse](#getordersresponse)|
|`400`|Missing or invalid parameters.|[GetOrdersResponse](#getordersresponse)|
|`403`|Access forbidden.|[GetOrdersResponse](#getordersresponse)|
|`500`|Server error.|[GetOrdersResponse](#getordersresponse)|

----

## Definitions
<a name="definitions"></a>

### GetOrdersResponse
<a name="getordersresponse"></a>

```
{"data": <Orders>} | <Errors>
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**payload**    <br>*optional*|The payload for the getOrders operation.|[Orders](#orders)|
|**errors**     <br>*optional*|One or more unexpected errors which occurred during the getOrders operation.|-|

</details>

### Orders
<a name="orders"></a>

```
[<Order>, ...]
```
An array containing one or more [Order](#order).

### Order
<a name="order"></a>

```
{"orderReference" <string>
 "contactDetails" <ContactDetails>
 "address"        <Address>
 "orderLines"     <OrderLines>
 "createdAt"      <string>}
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**orderReference** <br>*required*|The reference for a specific Fy! order: an "SO-" prefix followed by a series of numbers. |string|
|**contactDetails** <br>*required*|The contact details of the recipient.|[ContactDetails](#contactdetails)|
|**address**        <br>*required*|The address of the recipient.|[Address](#address)|
|**orderLines**     <br>*required*|One or more orderlines associated with the order.|[OrderLines](#orderlines)|
|**createdAt**      <br>*required*|The (ISO-8601) datetime when the order was created.|string|

</details>

### OrderLines
<a name="orderlines"></a>

```
[<OrderLine>, ...]
```
An array containing one or more [OrderLine](#orderline).

### OrderLine
<a name="orderline"></a>

```
{"id"       <number>
 "sku"      <string>
 "quantity" <number>}
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**id**         <br>*required*|The identification number of the orderline.|number|
|**sku**        <br>*required*|The SKU (stock keeping unit) of the orderline item.|string|
|**quantity**   <br>*required*|The quantity of items in the orderline.|number|

</details>

### ContactDetails
<a name="contactdetails"></a>

```
{"phone" <string>
 "email" <string>}
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**phone**  <br>*optional*|The phone number of the recipient.|string|
|**email**  <br>*optional*|The email address of the recipient.|string|

</details>

### Address
<a name="address"></a>

```
{"recipient" <string>
 "line1"     <string>
 "line2"     <string>
 "city"      <string>
 "postcode"  <string>
 "state"     <string>
 "country"   <string>
 "company"   <string>}
```

<details>
  <summary>View descriptions</summary>
  
|Name|Description|Schema|
|-|-|-|
|**recipient**  <br>*required*|The combined first and last names of the recipient.|string|
|**line1**      <br>*required*|The first line of the recipient's address.|string|
|**line2**      <br>*optional*|The second line of the recipient's address.|string|
|**city**       <br>*required*|The recipient's city.|string|
|**postcode**   <br>*required*|The recipient's postcode.|string|
|**state**      <br>*optional*|The recipient's state.|string|
|**country**    <br>*required*|The recipient's country.|string|
|**company**    <br>*optional*|The recipient's company.|string|

</details>
