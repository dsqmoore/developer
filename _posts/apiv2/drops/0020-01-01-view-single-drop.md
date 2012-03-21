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
        "href":    "/drops",
        "items": [{
          "href":  "/drops/101",
          "links": [{
            "rel":  "canonical",
            "href": "http://localhost:3000/472k3i21201H2O3O0h2L"
          }, {
            "rel":  "icon",
            "href": "http://localhost:3001/472k3i21201H2O3O0h2L"
          }],
          "data": [
            { "name": "id",      "value": 101 },
            { "name": "name",    "value": null },
            { "name": "private", "value": true },
            { "name": "views",   "value": 2 }
          ]
        }],
        "templates": [{
          "rel":  "/rels/recover",
          "href": "/drops?filter=trash",
          "data": [{ "name": "drop_ids", "value": [] }]
        }, {
          "rel":  "/rels/remove",
          "href": "/drops",
          "data": [{ "name": "drop_ids", "value": [] }]
        }]
      }
    }
