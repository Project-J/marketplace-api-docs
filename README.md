# Fy! Marketplace API

## General
* Data is consumed and returned as [JSON](https://en.wikipedia.org/wiki/JSON).
* Date(time)s are consumed and returned using the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format.

## Authentication
Authentication requires the use of a unique supplier API-key over HTTP Basic Auth. In practice this means using your supplier API-key as the username and leaving the password blank.

You can make authenticated requests using a client (such as [Postman](https://learning.postman.com/docs/sending-requests/authorization/#basic-auth) or [cURL](https://curl.se/docs/manpage.html#-u)) or manually. 

To authenticate requests manually, Basic Auth requires the username and password to be separated by a colon (e.g. `my-api-key:`). This then needs to be base-64 encoded and included in the Authorization header, e.g. `Authorization: Basic bXktYXBpLWtleQ==`.

## Reference

### Endpoints
|Endpoint|Description|URL|
|---|---|---|
|[getOrders](orders.md)|Returns orders created between the specified `from` and `to` parameters.|`/v0/orders?from={datetime}?to={datetime}`|
|[updateStock](stock.md)|Updates one or more stock items.|`/v0/inventory`|
|[updateShipments](shipments.md)|Updates one or more shipments.|`/v0/shipments`|
