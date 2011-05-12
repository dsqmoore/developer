---
layout: master
title: Validate Purchase
categories: purchases
---

# Validate Purchase

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
        "subscribed":              true,
        "subscription_expires_at": "2012-05-21",
        "alpha":                   false,
        "created_at":              "2010-12-10T17:07:01Z",
        "updated_at":              "2010-12-10T17:07:01Z",
        "activated_at":            null
      }


## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         -H "Content-Type: application/json" \
         -d \
            '{
              "receipt-data" : "ewogICJzaWduYXR1cmUiID0gIkFn..."
            }' \
         http://my.cl.ly/purchases


## Errors

If the receipt is invalid for any reason, an array of errors will be returned.

- Status: 422 Unprocessable Entity
- Body:

      [ "Receipt is invalid" ]
