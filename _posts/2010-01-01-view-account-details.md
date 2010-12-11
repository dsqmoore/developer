---
layout: master
title: View Account Details
categories: account
---

# View Account Details

Get the basic details of the authenticated account. This is the same response as returned by most account endpoints.


## Request

- Requires [authentication](/authentication/)
- HTTP Method: GET
- URL: http://my.cl.ly/account


## Response

- Status: 200 OK
- Body:

      {
        "id":               1,
        "email":            "arthur@dent.com",
        "domain":           null,
        "domain_home_page": null,
        "private_items":    true,
        "subscribed":       false,
        "alpha":            false,
        "created_at":       "2010-12-10T17:07:01Z",
        "updated_at":       "2010-12-10T17:12:51Z",
        "activated_at":     "2010-12-10T17:12:51Z"
      }


## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         "http://my.cl.ly/account"
