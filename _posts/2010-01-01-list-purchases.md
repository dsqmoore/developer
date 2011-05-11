---
layout: master
title: List Purchases
categories: purchases
---

# List Purchases

Retrieve a list of product identifiers available via iOS In App Purchases.


## Request

- HTTP Method: GET
- URL: http://my.cl.ly/products


## Response

- Status: 200 OK
- Body:

      [ "com.linebreak.CloudAppPro.1month",
        "com.linebreak.CloudAppPro.3months",
        "com.linebreak.CloudAppPro.6months",
        "com.linebreak.CloudAppPro.1year" ]


## Example

{: .shell}
    curl -H "Accept: application/json" \
         "http://my.cloudapp.local/products"
