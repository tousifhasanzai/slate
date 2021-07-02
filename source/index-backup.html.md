---
title: API Neem Pro Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript
  - php
  
toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://analytica.neem.pro'>Documentation Powered by Neem</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the docs Neem Pro. This document can be used to get clear understanding of how to call our WMS system and
perform various activities.


you may use our api to create product(s) on our sytem, inbound product(s) or change the stock quantity, Place the order, 
get trackings of any current or previous order and perform return activites.

To get better understanding we have provided sample code along with the methods.

# Authentication

> To authorize, use this code:

```php
CURLOPT_HTTPHEADER => array(
    'api-token: SDFOL3FOS23FGOS3423DNERE',
    'api-user: 152380'
    )
```

```javascript
 "headers": {
    "api-token": "SDFOL3FOS23FGOS3423DNERE",
    "api-user": "152380"
  }
```


> Make sure to replace `api-token` & `api-user` with your own credentials.

Kindly contact our support to give you credentials. They will provide api-key and api-token. In each request you will have to
pass these parameters in header

`'api-token: SDFOL3FOS23FGOS3423DNERE',
     'api-user: 152380'`

<aside class="notice">
You must replace <code>api-token</code> & <code>api-user</code> with your own credentials.
</aside>

# Place Order

```javascript
var form = new FormData();
form.append("orderId", "90000989898");
form.append("shippingAddress", "294, Garden East");
form.append("shippingZip", "49800");
form.append("shippingCity", "Karachi");
form.append("shippingState", "Sindh");
form.append("shippingCountry", "PK");
form.append("customerPhone", "03103434345");
form.append("customerName", "Tousif Khan");
form.append("products[0][qty]", "1");
form.append("products[0][price]", "45.00");
form.append("products[0][sku]", "8445156687569");
form.append("remarks", "This is my testing remarks for this order");

var settings = {
  "url": "http://api.neem.pro/order-create",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "api-token": "SDFOL3FOS23FGOS3423DNERE",
    "api-user": "152380"
  },
  "processData": false,
  "mimeType": "multipart/form-data",
  "contentType": false,
  "data": form
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

```php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'http://api.neem.pro/order-create',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => array('orderId' => '90000989898','shippingAddress' => '294, Garden East','shippingZip' => '49800','shippingCity' => 'Karachi','shippingState' => 'Sindh','shippingCountry' => 'PK','customerPhone' => '03103434345','customerName' => 'Tousif Khan','products[0][qty]' => '1','products[0][price]' => '45.00','products[0][sku]' => '8445156687569','remarks' => 'This is my testing remarks for this order'),
  CURLOPT_HTTPHEADER => array(
    'api-token: SDFOL3FOS23FGOS3423DNERE',
    'api-user: 152380'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

> The above command returns JSON structured like this:

```json
{
    "response": {
        "content": {
            "data": "FS202172151711415646",
            "errorCode": 200,
            "errorMsg": "Operation successful",
            "failed": false,
            "success": true
        },
        "code": 0
    }
}
```

When you have order in confirm state and you want to push that order to the WMS system so that we could start processing that order.


### HTTP Request

`POST http://api.neem.pro/order-create`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
orderId | Yes | order id of your system
shippingAddress | Yes | Customer Shipping Address
shippingZip | Yes | Customer Zip Code
shippingCity | Yes | Customer/Shipping City
shippingState | Yes | Customer/Shipping State
shippingCountry | Yes | Shipping Country in ISO-2 Format
customerPhone | Yes | Customer Phone Number
customerName | Yes | Customer Name
products[0][qty] | Yes | 1st Product Quantity
products[0][price] | Yes | 1st Product Price
products[0][sku] | Yes | 1st Product SKU Code
remarks | No | Optional Remarks

<aside class="success">
Remember — Your order may contains more than 1 product in that case use array as described above
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete


