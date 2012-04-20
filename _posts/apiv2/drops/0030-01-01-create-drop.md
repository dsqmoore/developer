---
layout: apiv2
title: Create Drop
categories: drops
---

# Create Drop

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 200 OK
    Cache-Control: max-age=0, private, must-revalidate
    Content-Type: application/vnd.collection+json; charset=utf-8
    Etag: "52284b921f36b0e124e1b4b423a1ff69"
    {
      "collection": {
        "version": "1.0",
        "href":    "...",
        "links":   [...],
        "template": {
          "data": [
            { "name": "name",         "value": null },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": null },
            { "name": "file_size",    "value": null }
          ]
        },
        "items": [...]
      }
    }

# Bookmark a Link

Following the Collection+JSON spec, fill `template` with the drop's name and URL
to bookmark. Send it as an HTTP POST to the collection's `href`. **Note:** The
value of the `private` field will be the default drop privacy the owner has
configured for their account.

**TODO:** This resource MUST accept `application/vnd.collection+json` as per the
Collection+JSON spec.

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           -H "Content-Type: application/json; charset=utf-8" \
           -X POST \
           -d '{
                 "name":         "CloudApp",
                 "private":      true,
                 "bookmark_url": "http://getcloudapp.com",
                 "file_size":    null
               }' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Type: application/vnd.collection+json; charset=utf-8
    {
      "collection": {
        "version": "1.0",
        "href": "...",
        "template": {
          "data": [
            { "name": "name",         "value": null },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": null },
            { "name": "file_size",    "value": null }
          ]
        },
        "items": [{
          "href": "...",
          "links": [
            { "rel": "root",       "href": "..." },
            { "rel": "collection", "href": "..." },
            { "rel": "canonical",  "href": "..." },
            { "rel": "icon",       "href": "..." }
          ],
          "data": [
            { "name": "id",           "value": 17532961 },
            { "name": "name",         "value": "CloudApp" },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": "http://getcloudapp.com" },
            { "name": "views",        "value": 0 }
          ]
        }]
      }
    }

# Upload a File

Following the Collection+JSON spec, fill `template` with the drop's name and the
size in bytes of the file to be uploaded. Send it as an HTTP POST to the
collection's `href`. **Note:** The value of the `private` field will be the
default drop privacy the owner has configured for their account.

**TODO:** This resource MUST accept `application/vnd.collection+json` as per the
Collection+JSON spec.

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           -H "Content-Type: application/json; charset=utf-8" \
           -X POST \
           -d '{
                 "name":         null,
                 "private":      true,
                 "bookmark_url": null,
                 "file_size":    1150
               }' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Type: application/vnd.collection+json; charset=utf-8
    {
      "collection": {
        "version":  "1.0",
        "href":     "...",
        "template": {
          "data": [
            { "name": "success_action_redirect", "value": "http://api.getcloudapp.com/drops/17533090/s3" },
            { "name": "AWSAccessKeyId", "value": "AKIAIDPUZISHSBEOFS6Q" },
            { "name": "key",            "value": "items/422X1J3J020J1Z1S0V19/${filename}" },
            { "name": "key",            "value": "items/1L2c052P0F0V2X1i0r30/${filename}" },
            { "name": "policy",         "value": "eyJleHBpcmF0aW9uIjoiMjAxM..." },
            { "name": "signature",      "value": "0zsDbT0t8hRkyHfWj2MTo0Ot6ec=" },
            { "name": "acl",            "value": "public-read" },
            { "name": "file",           "value": null }
          ]
        },
        "items": [{
          "href":  "...",
          "links": [
            { "rel": "root",       "href": "..." },
            { "rel": "collection", "href": "..." },
            { "rel": "canonical",  "href": "..." },
            { "rel": "icon",       "href": "..." }
          ],
          "data": [
            { "name": "id",           "value": 17533090 },
            { "name": "name",         "value": null },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": null },
            { "name": "views",        "value": 0 }
          ]
        }]
      }
    }

Fill `template` with the file to be uploaded. Encode each name and value pair in
`data` as `application/x-www-form-urlencoded` and POST it to the template's
`href`.

**Note:** According to [Amazon's documentation][s3-docs], any parameter after
`file` is ignored. Make sure `file` is the last parameter in the encoded request
or the upload may be rejected.

[s3-docs]: http://developer.amazonwebservices.com/connect/entry.jspa?externalID=1434

    $ curl -i -X POST \
           -F 'success_action_redirect=http://api.getcloudapp.com/drops/17533090/s3' \
           -F 'AWSAccessKeyId=AKIAIDPUZISHSBEOFS6Q' \
           -F 'key=items/422X1J3J020J1Z1S0V19/${filename}' \
           -F 'policy=eyJleHBpcmF0aW9uIjoiMjAxM...' \
           -F 'signature=0zsDbT0t8hRkyHfWj2MTo0Ot6ec=' \
           -F 'acl=public-read' \
           -F 'file=@/Users/Larry/Desktop/favicon.ico' \
           'http://f.cl.ly'

    HTTP/1.1 100 Continue

    HTTP/1.1 303 See Other
    ETag: "567d2d49d2d30e2db956d680a4d03f25"
    Location: http://api.getcloudapp.com/drops/17533090/s3?bucket=f.cl.ly&key=items%2F422X1J3J020J1Z1S0V19%2Ffavicon.ico&etag=%22567d2d49d2d30e2db956d680a4d03f25%22

Follow the redirect back to our API. Be sure to include the authentication token
when following this link.

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           'http://api.getcloudapp.com/drops/17533090/s3?bucket=f.cl.ly&key=items%2F422X1J3J020J1Z1S0V19%2Ffavicon.ico&etag=%22567d2d49d2d30e2db956d680a4d03f25%22'

    HTTP/1.1 200 OK
    Cache-Control: max-age=0, private, must-revalidate
    Content-Type: application/vnd.collection+json; charset=utf-8
    Etag: "4ef7d5eccf7c1a0bdcaa1dd5ea792de0"
    {
      "collection": {
        "version":  "1.0",
        "href":     "...",
        "template": {
          "data": [
            { "name": "name",         "value": null },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": null },
            { "name": "file_size",    "value": null }
          ]
        },
        "items": [
          {
            "href": "...",
            "links": [
              { "rel": "root",       "href": "..." },
              { "rel": "collection", "href": "..." },
              { "rel": "canonical",  "href": "..." },
              { "rel": "icon",       "href": "..." },
              { "rel": "embed",      "href": "..." },
              { "rel": "download",   "href": "..." }
            ],
            "data": [
              { "name": "id",           "value": 17533090 },
              { "name": "name",         "value": "favicon.ico" },
              { "name": "private",      "value": true },
              { "name": "bookmark_url", "value": null },
              { "name": "views",        "value": 0 }
            ]
          }
        ]
      }
    }
