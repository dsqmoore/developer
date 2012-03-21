---
layout: apiv2
title: View Single Drop
categories: drops
---

# View Single Drop

Follow a drop's `href` from the [drops collection](/list-drops).

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops/101"

    HTTP/1.1 200 OK
    Content-Type: application/vnd.collection+json; charset=utf-8
    ETag: "fb83cd304bacd599af0a1e73603500e5"
    Cache-Control: max-age=0, private, must-revalidate
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
            { "name": "id",      "value": 101 },
            { "name": "name",    "value": null },
            { "name": "private", "value": true },
            { "name": "views",   "value": 2 }
          ]
        }],
        "templates": [{
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
