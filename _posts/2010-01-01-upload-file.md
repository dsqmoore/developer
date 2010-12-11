---
layout: master
title: Upload File
categories: items
---

# Upload File

Files are uploaded directly to [S3](http://aws.amazon.com/s3/) to be as fast as possible. You'll need to request a few parameters from CloudApp and send them along with the file.

## Request

- Requires [authentication](/usage/#authentication)
- HTTP Method: GET
- URL: http://my.cl.ly/items/new

## Response

- Status: 200 OK
- Body:

      {
        "url": "http://f.cl.ly",
        "params": {
          "AWSAccessKeyId":          "AKIAIDPUZISHSBEOFS6Q",
          "key":                     "items/qL/${filename}",
          "acl":                     "public-read",
          "success_action_redirect": "http://my.cl.ly/items/s3",
          "signature":               "2vRWmaSy46WGs0MDUdLHAqjSL8k=",
          "policy":                  "eyJleHBpcmF0aW9uIjoiMjAxMC0wNC0wMVQwMDowMDowMFoiLCJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJsaW5lYnJlYWstdGVzdCJ9LHsiYWNsIjoicHVibGljLXJlYWQifSx7InN1Y2Nlc3NfYWN0aW9uX3JlZGlyZWN0IjoiaHR0cDovL215LmNsb3VkYXBwLmxvY2FsL3VwbG9hZHMvczMifSxbInN0YXJ0cy13aXRoIiwiJGtleSIsInVwbG9hZHMvcUwvIl1dfQ=="
        }
      }

Use this response to construct the upload. Each item in `params` becomes a separate parameter you'll need to post to `url`. Send the file as the parameter `file`.

According to [Amazon's documentation](http://developer.amazonwebservices.com/connect/entry.jspa?externalID=1434), any parameter after `file` is ignored. Make sure `file` is the last parameter or the upload will be rejected.

## Request

- HTTP Method: POST
- URL: Value of `url` in response. _(e.g., http://f.cl.ly)_
- Post each key and value from `params` as a separate parameter.
- Post the file data as the parameter `file`.

## Response

- Status: 303 See Other *(Follow the redirect using CloudApp [authentication](/usage/#authentication)(/authentication/).)*

## Request

- HTTP Method: GET
- URL: Value of `Location` header from previous response. _(e.g., http://my.cl.ly/items/s3)_

## Response

- Status: 200 OK
- Body:

      {
        "href":         "http://my.cl.ly/items/3",
        "name":         "Screen shot 2010-04-01 at 12.00.00 AM.png",
        "private":      false,
        "url":          "http://cl.ly/2wr4",
        "content_url":  "http://cl.ly/2wr4/content",
        "item_type":    "image",
        "view_counter": 0,
        "icon":         "http://my.cl.ly/images/item_types/image.png",
        "remote_url":   "http://f.cl.ly/items/3d7ba41682802c301150/Screen shot 2010-04-01 at 12.00.00 AM.png",
        "redirect_url": null,
        "created_at":   "2010-04-01T12:00:00Z",
        "updated_at":   "2010-04-01T12:00:00Z"
      }
