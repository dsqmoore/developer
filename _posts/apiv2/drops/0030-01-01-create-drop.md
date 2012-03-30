---
layout: apiv2
title: Create Drop
categories: drops
---

# Create Drop

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 200 OK
    Content-Type: application/vnd.collection+json; charset=utf-8
    ETag: "fb83cd304bacd599af0a1e73603500e5"
    {
      "collection": {
        "version":   "1.0",
        "href":      "...",
        "links":     [...],
        "items":     [...],
        "templates": [{
          "rel":    "/rels/create",
          "href":   "...",
          "data":   [
            { "name": "name",         "value": null },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": null },
            { "name": "file_size",    "value": null }
          ]
        },
        ...
        ]
      }
    }


# Bookmark a Link

Fill the `/rels/create` template with the drop's name and the URL to bookmark.
Encode each name and value pair in `data` as `application/x-www-form-urlencoded`
or `application/json` and POST it to the template's `href`. **Note:** The value
of the `private` field will be the default drop privacy the owner has configured
for their account.

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
    Content-Type: application/vnd.collection+json; charset=utf-8
    Cache-Control: no-cache
    {
      "collection": {
        "version": "1.0",
        "href":    "...",
        "items": [{
          "href":  "...",
          "links": [
            { "rel":  "canonical", "href": "..." },
            { "rel":  "icon",      "href": "..." }
          ],
          "data": [
            { "name": "id",      "value": 42 },
            { "name": "name",    "value": "CloudApp" },
            { "name": "private", "value": true },
            { "name": "views",   "value": 0 }
          ]
        }],
        "templates": [{
          "rel":  "/rels/remove",
          "href": "...",
          "data": [{ "name": "drop_ids", "value": [] }]
        }]
      }
    }


# Upload a file

Fill the `/rels/create` template with the drop's name and the size in bytes of
the file to be uploaded. Encode each name and value pair in `data` as
`application/x-www-form-urlencoded` or `application/json` and POST it to the
template's `href`. **Note:** The value of the `private` field will be the
default drop privacy the owner has configured for their account.

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           -H "Content-Type: application/json; charset=utf-8" \
           -X POST \
           -d '{
                 "name":         "CloudApp",
                 "private":      true,
                 "bookmark_url": null,
                 "file_size":    43008
               }' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 201 Created
    Content-Type: application/vnd.collection+json; charset=utf-8
    Cache-Control: no-cache
    {
      "collection": {
        "version": "1.0",
        "href":    "...",
        "items": [{
          "href":  "...",
          "links": [
            { "rel":  "canonical", "href": "..." },
            { "rel":  "icon",      "href": "..." }
          ],
          "data": [
            { "name": "id",      "value": 42 },
            { "name": "name",    "value": "CloudApp" },
            { "name": "private", "value": true },
            { "name": "views",   "value": 0 }
          ]
        }],
        "templates": [{
          "rel":  "/rels/upload",
          "href": "...",
          "data": [
            { "name": "AWSAccessKeyId",          "value": "AKIAIDPUZISHSBEOFS6Q" },
            { "name": "key",                     "value": "items/qL/${filename}" },
            { "name": "acl",                     "value": "public-read" },
            { "name": "success_action_redirect", "value": "http://api.getcloudapp.com/drops/42/s3" },
            { "name": "signature",               "value": "2vRWmaSy46WGs0MDUdLHAqjSL8k=" },
            { "name": "policy",                  "value": "eyJleHBpcmF0aW9uIjo..." },
            { "name": "file",                    "value": null }
          ]
        }]
      }
    }

Fill the `/rels/upload` template with the file to be uploaded. Encode each name
and value pair in `data` as `application/x-www-form-urlencoded` and POST it to
the template's `href`.

**Note:** According to [Amazon's documentation][s3-docs], any parameter after
`file` is ignored. Make sure `file` is the last parameter in the encoded request
or the upload may be rejected.

[s3-docs]: http://developer.amazonwebservices.com/connect/entry.jspa?externalID=1434

    $ curl -i -X POST \
           -d ... \
           -L \
           "http://f.cl.ly/..."

    HTTP/1.1 303 See Other
    Location: http://api.getcloudapp.com/drops/42/s3

    HTTP/1.1 200 OK
    Content-Type: application/vnd.collection+json; charset=utf-8
    {
      "collection": {
        "version": "1.0",
        "href":    "...",
        "items": [{
          "href":  "...",
          "links": [
            { "rel":  "canonical", "href": "..." },
            { "rel":  "icon",      "href": "..." }
          ],
          "data": [
            { "name": "id",      "value": 42 },
            { "name": "name",    "value": "CloudApp" },
            { "name": "private", "value": true },
            { "name": "views",   "value": 0 }
          ]
        }],
        "templates": [{
          "rel":  "/rels/upload",
          "href": "...",
          "data": [
            { "name": "AWSAccessKeyId",          "value": "AKIAIDPUZISHSBEOFS6Q" },
            { "name": "key",                     "value": "items/qL/${filename}" },
            { "name": "acl",                     "value": "public-read" },
            { "name": "success_action_redirect", "value": "http://api.getcloudapp.com/drops/42/s3" },
            { "name": "signature",               "value": "2vRWmaSy46WGs0MDUdLHAqjSL8k=" },
            { "name": "policy",                  "value": "eyJleHBpcmF0aW9uIjo..." },
            { "name": "file",                    "value": null }
          ]
        }]
      }
    }

**Note:** Be sure the redirect after uploading the file is followed with the
authentication token supplied.


# Errors

_Exceeded plan limits (file too large, too many drops)._
