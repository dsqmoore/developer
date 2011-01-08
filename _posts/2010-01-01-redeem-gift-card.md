---
layout: master
title: Redeem Gift Card
categories: account
---

# Redeem Gift Card

Apply a gift card to an account.


## Request

- Requires [authentication](/usage/#authentication)
- HTTP Method: PUT
- URL: Value of `href` on a gift card. _(e.g., https://my.cl.ly/gift\_cards/ABC123)_


## Response

- Status: 200 OK
- Body:

      {
        "id":           1,
        "code":         "ABC123",
        "plan":         'pro',
        "months":       12,
        "href":         "https://my.cl.ly/gift_cards/ABC123",
        "created_at":   "2011-01-07T14:23:08Z",
        "updated_at":   "2011-01-07T14:23:08Z",
        "redeemed_at":  "2011-01-07T14:23:08Z",
        "effective_at": "2011-01-07T14:23:08Z",
        "expires_at":   "2011-01-07T14:23:08Z"
      }


## Example

{: .shell}
    curl -v --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         -H "Content-Type: application/json" \
         -X PUT \
         "https://my.cl.ly/gift_cards/38E07C624DD6DD9E"
