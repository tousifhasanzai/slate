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
    'api-token: ABCDEF23DSOS4N)(dof3$!!@#%34',
    'api-user: 152380'
    )
```

```javascript
 "headers": {
    "api-token": "ABCDEF23DSOS4N)(dof3$!!@#%34",
    "api-user": "152380"
  }
```


> Make sure to replace `api-token` & `api-user` with your own credentials.

Kindly contact our support to give you credentials. They will provide api-key and api-token. In each request you will have to
pass these parameters in header

`'api-token: ABCDEF23DSOS4N)(dof3$!!@#%34',
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
    "api-token": "ABCDEF23DSOS4N)(dof3$!!@#%34",
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
  CURLOPT_POSTFIELDS => array(
        'orderId' => '90000989898',
        'shippingAddress' => '294, Garden East',
        'shippingZip' => '49800',
        'shippingCity' => 'Karachi',
        'shippingState' => 'Sindh',
        'shippingCountry' => 'PK',
        'customerPhone' => '03103434345',
        'customerName' => 'Tousif Khan',
        'products[0][qty]' => '1',
        'products[0][price]' => '45.00',
        'products[0][sku]' => '8445156687569',
        'remarks' => 'This is my testing remarks for this order'
),
  CURLOPT_HTTPHEADER => array(
    'api-token: ABCDEF23DSOS4N)(dof3$!!@#%34',
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
products[0][discount] | Yes | if discount is applied to only specific product
subTotal | Yes | Total Products amount excluding shipping fee and discounts
cartDiscount | No | if there is any discount applied on entire order
shippingFee | No| if there is any shipping fee applied on order
amount | Yes | Total amount needs to be collected from customer this include shipping fee and discounts
remarks | No | Optional Remarks

<aside class="success">
Remember — Your order may contains more than 1 product in that case use array as described above
</aside>

# Cancel Order

```javascript
var form = new FormData();
form.append("orderId", "90000989898");

var settings = {
  "url": "http://api.neem.pro/order-cancel",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "api-token": "ABCDEF23DSOS4N)(dof3$!!@#%34",
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
  CURLOPT_URL => 'http://api.neem.pro/order-cancel',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => array(
        'orderId' => '90000989898'
),
  CURLOPT_HTTPHEADER => array(
    'api-token: ABCDEF23DSOS4N)(dof3$!!@#%34',
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

When you have order successfully submitted to WMS system and now need to cancel that order.




`POST http://api.neem.pro/order-cancel`



Parameter | Required | Description
--------- | ------- | -----------
orderId | Yes | order id of your system

# Warehouse Order Status

```javascript
var form = new FormData();
form.append("orderId", "90000989898");

var settings = {
  "url": "http://api.neem.pro/order-status",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "api-token": "ABCDEF23DSOS4N)(dof3$!!@#%34",
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
  CURLOPT_URL => 'http://api.neem.pro/order-status',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => array(
        'orderId' => '90000989898'
),
  CURLOPT_HTTPHEADER => array(
    'api-token: ABCDEF23DSOS4N)(dof3$!!@#%34',
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
            "data": {
                "billType": 20,
                "code": "SO2021B4000006470",
                "customerBillCode": "AKG000032024",
                "list": [
                    {
                        "createTime": 1636005588000,
                        "createUser": "operations@cis.com.pk",
                        "stateOccurTimeStr": "2021-11-04 12:59:48",
                        "status": 27,
                        "statusDesc": "Picking"
                    },
                    {
                        "createTime": 1636005416000,
                        "createUser": "FOP-SYSTEM",
                        "stateOccurTimeStr": "2021-11-04 12:56:56",
                        "status": 20,
                        "statusDesc": "Released to warehouse"
                    },
                    {
                        "createTime": 1636005415000,
                        "createUser": "Tousif",
                        "stateOccurTimeStr": "2021-11-04 12:56:55",
                        "status": 10,
                        "statusDesc": "Initialized"
                    },
                    {
                        "createTime": 1636005415000,
                        "createUser": "Tousif",
                        "stateOccurTimeStr": "2021-11-04 12:56:55",
                        "status": 10,
                        "statusDesc": "Initialized"
                    }
                ]
            },
            "errorCode": 200,
            "errorMsg": "Operation successful",
            "failed": false,
            "success": true
        },
        "code": 0
    }
}
```

When you have order successfully submitted to WMS system and now need to view the status.




`POST http://api.neem.pro/order-status`



Parameter | Required | Description
--------- | ------- | -----------
orderId | Yes | order id of your system

# Return Order

```javascript
var form = new FormData();
form.append("orderId", "90000989898");
form.append("trackingNumber", "WR1965580");
form.append("courier", "rider");

var settings = {
  "url": "http://api.neem.pro/returns",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "api-token": "ABCDEF23DSOS4N)(dof3$!!@#%34",
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
  CURLOPT_URL => 'http://api.neem.pro/order-status',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => array(
        'orderId' => '90000989898'
        'trackingNumber' => 'WR1965580'
        'courier' => 'rider'
),
  CURLOPT_HTTPHEADER => array(
    'api-token: ABCDEF23DSOS4N)(dof3$!!@#%34',
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

When you have order successfully Shipped from WMS system and now need to return.




`POST http://api.neem.pro/return`



Parameter | Required | Description
--------- | ------- | -----------
orderId | Yes | order id of your system
trackingNumber | Yes | Tracking number of 3PL
courier | Yes | [lcs,tcs,rider]
trackingNumber | Yes | courier tracking number    
products[0][sku] | Yes | first returned Product: you can provide all return products in array form
products[0][quantity] | Yes | first returned product quantity
type | Yes | [return,partial_return]
# Create Product

```javascript
var form = new FormData();
form.append("barCode", "1000000100");
form.append("sku", "12300009092");
form.append("name", "Test CIS Product");
form.append("highValueFlag", "0");
form.append("easySpreadOdorFlag", "0");
form.append("dangerProductFlag", "0");
form.append("liquidFlag", "0");
form.append("cosmeticFlag", "0");
form.append("shelfLifeFlag", "0");



var settings = {
  "url": "http://api.neem.pro/product-create",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "api-token": "ABCDEF23DSOS4N)(dof3$!!@#%34",
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
  CURLOPT_URL => 'http://api.neem.pro/product-create',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => array(
      'barCode' => '1000000100',
      'sku' => '12300009092',
      'name' => 'Test CIS Product',
      'highValueFlag' => '0',
      'easySpreadOdorFlag' => '0',
      'dangerProductFlag' => '0',
      'liquidFlag' => '0',
      'cosmeticFlag' => '0',
      'shelfLifeFlag' => '0'
),
  CURLOPT_HTTPHEADER => array(
    'api-token: ABCDEF23DSOS4N)(dof3$!!@#%34',
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

To create a product on WMS system before getting inbound




`POST http://api.neem.pro/product-create`



Parameter | Required | Description
--------- | ------- | -----------
barCode | required | Product Barcode
sku | required | SKU code
name | required | Name of Product
highValueFlag | optional:boolean | Expensive or not
easySpreadOdorFlag | optional:boolean | Spread ordor
dangerProductFlag | optional:boolean | Dangerous Product
liquidFlag | optional:boolean | Liquid Product 
cosmeticFlag | optional:boolean | Cosmetics
shelfLifeFlag | optional:boolean | Does this product has expiry 
shelfLifeDays | required_with:shelfLifeFlag | Days should remain in shelf
advantDays | required_with:shelfLifeFlag:integer | No of Days for Expiry
inboundShelfLifeThreshold | required_with:shelfLifeFlag | Goods are not allowed to take in if threshold reached
outboundShelfLifeThreshold | required_with:shelfLifeFlag |Goods are not allowed to take out if threshold reached 
advantOutboundFlag | required_with:shelfLifeFlag:boolean | Allow sent out product if threshold reached
expiredOutboundFlag | required_with:shelfLifeFlag:boolean | Allow sent out expired product
shelfLifeAlarmDays | required_with:shelfLifeFlag:integer | No of days before shelf life alarm issue
shelfLifeOutStockDays | required_with:shelfLifeFlag:integer | No of days during which products are allowed sent out
shelfLifeInStockDays | required_with:shelfLifeFlag:integer | Required no. of days before expiration
shelfLifeAdvantThreshold | required_with:shelfLifeFlag | Threshold for no. of days before expiration
