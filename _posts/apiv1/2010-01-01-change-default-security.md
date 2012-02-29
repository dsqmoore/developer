---
layout: master
title: Change Default Security
categories: account
---

# Change Default Security

Change the security of newly created items to either private (long links) or public (short links). Privacy can be set on a per-item basis after creation.


## Request

- Requires [authentication](/usage/#authentication)
- HTTP Method: PUT
- URL: http://my.cl.ly/account
- Body:

      {
        "user": {
          "private_items": false
        }
      }


## Response

- Status: 200 OK
- Body:

      {
        "id":               1,
        "email":            "arthur@dent.com",
        "domain":           null,
        "domain_home_page": null,
        "private_items":    false,
        "subscribed":       false,
        "alpha":            false,
        "created_at":       "2010-12-10T17:07:01Z",
        "updated_at":       "2010-12-10T20:33:38Z",
        "activated_at":     "2010-12-10T17:07:01Z"
      }

## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         -H "Content-Type: application/json" \
         -d \
           '{
              "user": {
                "private_items": false
              }
            }' \
         -X PUT \
         "http://my.cl.ly/account"
