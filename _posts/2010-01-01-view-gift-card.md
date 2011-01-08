---
layout: master
title: View Gift Card Details
categories: account
---

# View Gift Card Details

Get the details of an unredeemed gift card.


## Request

- Requires [authentication](/usage/#authentication)
- HTTP Method: GET
- URL: https://my.cl.ly/redeem/**_gift card code_** _(e.g., https://my.cl.ly/redeem/ABC123)_

## Response

- Status: 200 OK
- Body:

      {
        "id":           1,
        "code":         "ABC123",
        "plan":         'pro',
        "months":       12,
        "href":         "https://my.cl.ly/redeem/ABC123",
        "created_at":   "2011-01-07T14:23:08Z",
        "updated_at":   "2011-01-07T14:23:08Z",
        "redeemed_at":  null,
        "effective_at": null,
        "expires_at":   null
      }

## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         -H "Content-Type: application/json" \
         "https://my.cl.ly/redeem/ABC123"
