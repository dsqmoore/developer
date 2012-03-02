---
layout: apiv2
title: Create Drop
categories: drops
---

# Create Drop

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/"

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Type: application/vnd.cloudapp+json
    Link: </account>; rel="/rels/account", </drops>; rel="/rels/drops"

Make a HEAD request to the link `/rels/drops`.

    $ curl -I -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 200 OK
    ...
    Link: </drops/new>; rel="/rels/drops/form"

Follow the link `/rels/drops/form`.

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops/new"

    HTTP/1.1 200 OK
    ...
    Link: </drops/new>; rel="/rels/drops/form"

    {
      "action": "/drops",
      "method": "post",
      "elements": {
        "name":     null,
        "private":  true,
        "bookmark": {
          "url": null
        },
        "file": {
          "content_length": 0
        }
      }
    }

**Bookmark:** Fill in the new drops name in `elements.name` and the URL to
bookmark in `elements.bookmark.url`.

**File:** Fill in the new drops name in `elements.name` and the content length
of the file in bytes in `elements.file.content_length`.

Optionally make the drop private or public by setting `elements.private` to
`true` or `false` respectively. Then collect each key/value pair in `elements`,
encode it as a string using `application/x-www-form-urlencoded`,
`application/json`, or `application/vnd.cloudapp+json`, and send it to the URL
in `action` using the HTTP method in `method`.


### Bookmark

    $ curl -i -H "Content-Type: application/json" \
           -X POST \
           -d '{
                 "name":     "Funny cat link",
                 "private":  true,
                 "bookmark": {
                   "url": "http://funnycats.com/cat123"
                 },
                 "file": {
                   "content_length": 0
                 }
               }' \
           "http://api.getcloudapp.com/account/token"

### File

    $ curl -i -H "Content-Type: application/json" \
           -X POST \
           -d '{
                 "name":     "Funny cat picture",
                 "private":  false,
                 "bookmark": {
                   "url": null
                 },
                 "file": {
                   "content_length": 1048576
                 }
               }' \
           "http://api.getcloudapp.com/drops"

    {
      "action": "https://s3.amazonaws.com/...",
      "method": "post",
      "elements": {
        "key":       "...",
        "acl":       "...",
        "signature": "...",
        "policy":    "...",
        "AWSAccessKeyId":          "AKIAIDPUZISHSBEOFS6Q",
        "success_action_redirect": "...",
        "file":      null
      }
    }

Either a bookmark or file will return:

    HTTP/1.1 201 Created
    ...
    Link: </drops/1234>; rel="self"

    {
      "action": "https://s3.amazonaws.com/...",
      "method": "post",
      "elements": {
        "key":       "...",
        "acl":       "...",
        "signature": "...",
        "policy":    "...",
        "AWSAccessKeyId":          "AKIAIDPUZISHSBEOFS6Q",
        "success_action_redirect": "...",
        "file":      null
      }
    }

Encode `elements` as `multipart/form-data`.

**Note:** According to Amazon’s documentation, any parameter after file is
ignored. Make sure file is last or the upload will be rejected.

_To be continued..._
