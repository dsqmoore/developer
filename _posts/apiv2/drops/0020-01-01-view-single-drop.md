---
layout: apiv2
title: View Single Drop
categories: drops
---

# View Single Drop

Follow a drop's `href` from the [drops collection](/list-drops).

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops/13950097"

    HTTP/1.1 200 OK
    Cache-Control: max-age=0, private, must-revalidate
    Content-Type: application/vnd.collection+json; charset=utf-8
    Etag: "35c4ad88d9ba03a26b2d332f5b5f6f06"
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
        "items": [{
          "href":  "...",
          "links": [
            { "rel": "root",       "href": "..." },
            { "rel": "collection", "href": "..." },
            { "rel": "canonical",  "href": "..." },
            { "rel": "icon",       "href": "..." },
            { "rel": "embed",      "href": "..." },
            { "rel": "download",   "href": "..." }
          ],
          "data": [
            { "name": "id",           "value": 13950097 },
            { "name": "name",         "value": "favicon.ico" },
            { "name": "private",      "value": true },
            { "name": "bookmark_url", "value": null },
            { "name": "views",        "value": 29 }
          ]
        }]
      }
    }
