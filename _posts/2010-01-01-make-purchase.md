---
layout: master
title: Make Purchase
categories: purchases
---

# Make Purchase

Send a Base64 encoded receipt from Apple to complete the purchase.


## Request

- HTTP Method: POST
- URL: http://my.cl.ly/purchases
- Body:

      {
        "receipt-data" : "ewogICJzaWduYXR1cmUiID0gIkFn..."
      }


## Response

- Status: 201 Created
- Body:

      {
        "id":                      1,
        "email":                   "arthur@dent.com",
        "domain":                  null,
        "domain_home_page":        null,
        "private_items":           true,
        "subscribed":              false,
        "subscription_expires_at": "2012-05-21",
        "alpha":                   false,
        "created_at":              "2010-12-10T17:07:01Z",
        "updated_at":              "2010-12-10T17:07:01Z",
        "activated_at":            null
      }


## Example

{: .shell}
    curl -H "Accept: application/json" \
         -H "Content-Type: application/json" \
         -d \
            '{
              "receipt-data" : "ewogICJzaWduYXR1cmUiID0gIkFn..."
            }' \
         http://my.cl.ly/purchases
