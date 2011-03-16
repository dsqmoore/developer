---
layout: master
title: Common Errors
categories: account
---

# Common Errors

There are several errors that may be returned by any CloudApp API endpoint.
These are their stories.


## Unactivated Account

After registering, an account must be activated by following a link that was
emailed. If the account is used prior to activation, the request will return the
following response.

- Status: 409 Conflict
- Body:

      "Your account hasn't been activated. Please check your email and activate your account."
