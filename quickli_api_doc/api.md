# Documentation for [Quicklie Business API](http://staging.quickli.com) API v1.0


1. To access Quickli Business API first step is authenticate.
2. We will provide app_id and access_key for users after successful registration. Without these auth tokens, no application could access API. This `app_id` and `access_key` should be present in every call to Quickli Business API.
3. Quickli Business API version 1 url for testing is `http://staging.quickli.com/`.

## Create New Order

### Order with customer address present:-
* In parameters `app_id` and `access_key` should be present.
* partner_id(unique), store_id(unique), app_id(unique), access_key(unique) and address are required for call.
* For customer address required parameters are: destination_address(customer address), destination_location(customer location), destination_phone(customer phone), destination_ltd(latitude) and destination_lng(longitude).
* Url for the creating new order:- `/api/v1/business/createOrder`. Request type is `POST`.


Sample call:-

```array
  'partner_id' => '3',
  'store_id' => '2',
  'app_id' => 'o1b94DePfikYHyAQdhu9vtOdtDiMiMQR',
  'access_key' => 'I7OyrBI8qta4mv0RB6KrwQibBdMnBv0c',
  'address' => 'Yes',
  'destination_address' => 'A-175, Vatikas',
  'destination_location' => 'Huda City Centre Metro Station, Sector 29, Gurgaon, Haryana',
  'destination_phone' => '9958705209',
  'destination_ltd' => '28.459123',
  'destination_lng' => '77.072815'


```

* If tokens for calls are authorised and order is created successfully, API will return status as `Success` with order id and current order status in `json` format.

```json

{
  "status": "Success",
  "order_id": "230",
  "order_status": "Processing"
}

```

* If destination location is not found , API will return status as `Retry` in `json` format.

```json

{
  "status": "Retry",
  "Message": "Address not found. Please try a landmark or building name."
}

```

* If required parameters are missing, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Required Parameters Missing"
}

```

* If store credentials are NOT authenticated, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Unauthorised Request"
}

```
* If partner store is not active, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Partner is not active"
}

```

* If store is not found, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Store not found"
}

```

* If store is not associated with requesting partner, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Store not associated with requesting partner"
}

```

### Order with customer address not present:-
* In parameters `app_id` and `access_key` should be present.
* partner_id(unique), store_id(unique), app_id(unique), access_key(unique) and address are required for call.
* Url for the creating new order:- `/api/v1/business/orders`. Request type is `POST`.


Sample call:-

```array
  'partner_id' => '3',
  'store_id' => '2',
  'app_id' => 'o1b94DePfikYHyAQdhu9vtOdtDiMiMQR',
  'access_key' => 'I7OyrBI8qta4mv0RB6KrwQibBdMnBv0c',
  'address' => 'No',

```

* If tokens for calls are authorised and order is created successfully, API will return status as `Success` with order id and current order status in `json` format.

```json

{
  "status": "Success",
  "order_id": "230",
  "order_status": "Processing"
}

```

* If required parameters are missing, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Required Parameters Missing"
}

```

* If store credentials are NOT authenticated, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Unauthorised Request"
}

```
* If partner store is not active, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Partner is not active"
}

```

* If store is not found, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Store not found"
}

```

* If store is not associated with requesting partner, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Store not associated with requesting partner"
}

```

## Track Order

### Tracking order :-
* This call is made whenever updated order status is required.
* In parameters `app_id` and `access_key` should be present.
* partner_id(unique), store_id(unique), app_id(unique), access_key(unique) and order_id are required for call.
* Url for the accept order call is :- `/api/v1/business/orders/track`. Request type is `POST`.

Sample call:-

```array
  'partner_id' => '3',
  'store_id' => '2',
  'app_id' => '3f426816b1859f6f9688cd266ddfadd7',
  'access_key' => '3f426816b1859f6f9688cd266ddfadd7',
  'order_id' => '293'

```

* If tokens for call are authorised successfully, API will return status as `Success` with order details in `json` format within array.

```json

[
  {
    "Order Id " : "'230'" ,
    "Status" : "Processing" ,
    "Customer Phone" : "7852255888",
    "Customer Address" : "A-175, Vatikas, Huda City Centre Metro Station, Sector 29, Gurgaon, Haryana, India",
    "Store Name": "Deepak Store",
    "Store Phone": "9958705209",
    "Delivery Boy Phone" : "undefined",
    "Placed at" : "Mon Jun 29 2015 12:47:17 GMT+0530 (IST)",
    "Accepted at" : "undefined",
    "Picked at" : "undefined",
    "Delivered at" : "undefined",
    "Billing Amount" : "0",
    "Delivery Amount" : "51.60"
  }
]

```

* If required parameters are missing, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Required Parameters Missing"
}

```

* If store credentials are NOT authenticated, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Unauthorised Request"
}

```
* If partner store is not active, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Partner is not active"
}

```

* If store is not found, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Store not found or Inactive store"
}

```

* If store is not associated with requesting partner, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Store not associated with requesting partner"
}

```

* If order is not associated with requesting partner or store, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Order not associated with requesting store and partner."
}

```

## Check Delivery Balance

### Tracking delivery balance :-
* This call is made whenever updated delivery balance is required.
* In parameters `app_id` and `access_key` should be present.
* partner_id(unique), app_id(unique) and access_key(unique) are required for call.
* Url for the accept order call is :- `/api/v1/business/balance/track`. Request type is `POST`.

Sample call:-

```array
  'partner_id' => '3',
  'app_id' => '3f426816b1859f6f9688cd266ddfadd7',
  'access_key' => '3f426816b1859f6f9688cd266ddfadd7'

```

* If tokens for call are authorised successfully, API will return status as `Success` with order details in `json` format within array.

```json

{
  "Status" : "Success",
  "Available Delivery Balance" : "189.40"
}

```

* If required parameters are missing, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Required Parameters Missing"
}

```

* If store credentials are NOT authenticated, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Unauthorised Request"
}

```
* If partner store is not active, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Partner is not active"
}

```

* If delivery balance is not applicable for requesting partner, API will return status as `Fail` in `json` format.

```json

{
  "Status" : "Fail",
  "Message" : "Delivery balance is not applicable with this account."
}

```
