---
layout: master
title: Change Email
categories: account
---

# Change Email

Update the email address on an account.


## Request

- Requires [authentication](/authentication/) and current password
- HTTP Method: PUT
- URL: http://my.cl.ly/account
- Body:

      {
        "user": {
          "email":            "ford@prefect.com",
          "current_password": "towel",
        }
      }


## Response

- Status: 200 OK
- Body:

      {
        "id":               1,
        "email":            "ford@prefect.com",
        "domain":           null,
        "domain_home_page": null,
        "private_items":    true,
        "subscribed":       false,
        "alpha":            null,
        "created_at":       "2010-12-10T17:07:01Z",
        "updated_at":       "2010-12-10T17:07:01Z",
        "activated_at":     null
      }


## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         -H "Content-Type: application/json" \
         -d \
           '{
              "user": {
                "email":            "ford@prefect.com",
                "current_password": "towel"
              }
            }' \
         -X PUT \
         "http://my.cloudapp.local/account"
