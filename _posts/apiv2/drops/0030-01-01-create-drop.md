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
    ETag: "a128e2f8c12aaa95637a5d4af58efa22"
    Cache-Control: max-age=0, private, must-revalidate
    {
      "collection": {
        "version":   "1.0",
        "href":      "...",
        "links":     [...],
        "items":     [...],
        "templates": [{
          "rel":  "/rels/create",
          "href": "...",
          "data": [
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
        "items":   [{
          "href":  "...",
          "links": [
            { "rel": "canonical", "href": "..." },
            { "rel": "icon",      "href": "..." }
          ],
          "data": [
            { "name": "id",           "value": 136 },
            { "name": "name",         "value": "CloudApp" },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": "http://getcloudapp.com" },
            { "name": "views",        "value": 0 }
          ]
        }],
        "templates": [...]
      }
    }


# Upload a File

Fill the `/rels/create` template with the drop's name and the size in bytes of
the file to be uploaded. Encode each name and value pair in `data` as
`application/x-www-form-urlencoded` or `application/json` and POST it to the
template's `href`. **Note:** The value of the `private` field will be the
default drop privacy the owner has configured for their account.

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
    Content-Type: application/vnd.collection+json; charset=utf-8
    Cache-Control: no-cache
    {
      "collection": {
        "version": "1.0",
        "href":    "...",
        "items":   [{
          "href":  "...",
          "links": [
            { "rel": "canonical", "href": "..." },
            { "rel": "icon",      "href": "..." }
          ],
          "data": [
            { "name": "id",           "value": 140 },
            { "name": "name",         "value": null },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": null },
            { "name": "views",        "value": 0 }
          ]
        }],
        "templates": [{
          "rel":  "/rels/upload",
          "href": "...",
          "data": [
            { "name": "success_action_redirect", "value": "http://api.getcloudapp.com/drops/140/s3" },
            { "name": "AWSAccessKeyId", "value": "AKIAIDPUZISHSBEOFS6Q" },
            { "name": "key",            "value": "items/1L2c052P0F0V2X1i0r30/${filename}" },
            { "name": "policy",         "value": "eyJleHBpcmF0aW9uIjoiMjAxM..." },
            { "name": "signature",      "value": "6n0Y1P8y6wgMGcKZ2shxiodgDW4=" },
            { "name": "acl",            "value": "public-read" },
            { "name": "file",           "value": null }
          ]
        },
        ...
        ]
      }
    }

Fill the `/rels/upload` template with the file to be uploaded. Encode each name
and value pair in `data` as `application/x-www-form-urlencoded` and POST it to
the template's `href`.

**Note:** According to [Amazon's documentation][s3-docs], any parameter after
`file` is ignored. Make sure `file` is the last parameter in the encoded request
or the upload may be rejected.

[s3-docs]: http://developer.amazonwebservices.com/connect/entry.jspa?externalID=1434

     curl -i -X POST \
           -F 'success_action_redirect=http://api.getcloudapp.com/drops/140/s3' \
           -F 'AWSAccessKeyId=AKIAIDPUZISHSBEOFS6Q' \
           -F 'key=items/1L2c052P0F0V2X1i0r30/${filename}' \
           -F 'policy=eyJleHBpcmF0aW9uIjoiMjAxM...' \
           -F 'signature=6n0Y1P8y6wgMGcKZ2shxiodgDW4=' \
           -F 'acl=public-read' \
           -F 'file=@/Users/Larry/Desktop/favicon.ico' \
           'http://f.cl.ly'

    HTTP/1.1 100 Continue

    HTTP/1.1 303 See Other
    ETag: "567d2d49d2d30e2db956d680a4d03f25"
    Location: http://api.getcloudapp.com/drops/140/s3?bucket=f.cl.ly&key=items%2F1L2c052P0F0V2X1i0r30%2Ffavicon.ico&etag=%22567d2d49d2d30e2db956d680a4d03f25%22

Now follow the redirect back to our API. Be sure to include the authentication
token when following this link.

    curl -i -H 'Authorization: Token token="abc123"' \
         'http://api.getcloudapp.com/drops/140/s3?bucket=f.cl.ly&key=items%2F1L2c052P0F0V2X1i0r30%2Ffavicon.ico&etag=%22567d2d49d2d30e2db956d680a4d03f25%22'

    HTTP/1.1 200 OK
    Content-Type: application/vnd.collection+json; charset=utf-8
    Cache-Control: no-cache
    {
      "collection": {
        "version": "1.0",
        "href": "...",
        "items": [
          {
            "href": "...",
            "links": [
              { "rel": "canonical", "href": "..." },
              { "rel": "icon",      "href": "..." },
              { "rel": "embed",     "href": "..." },
              { "rel": "download",  "href": "..." }
            ],
            "data": [
              { "name": "id",           "value": 140 },
              { "name": "name",         "value": "favicon.ico" },
              { "name": "private",      "value": true },
              { "name": "bookmark_url", "value": null },
              { "name": "views",        "value": 0 }
            ]
          }
        ],
        "templates": [{
          "rel":  "/rels/create",
          "href": "...",
          "data": [
            { "name": "name",         "value": null },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": null },
            { "name": "file_size",    "value": null }
          ]
        }, {
          "rel":  "/rels/recover",
          "href": "...",
          "data": [{ "name": "drop_ids", "value": [] }]
        }, {
          "rel":  "/rels/remove",
          "href": "...",
          "data": [{ "name": "drop_ids", "value": [] }]
        }]
      }
    }


# Errors

_Exceeded plan limits (file too large, too many drops)._
