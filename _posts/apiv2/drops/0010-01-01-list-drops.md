---
layout: apiv2
title: List Drops
categories: drops
---

# List Drops

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 200 OK
    Content-Type: application/vnd.collection+json; charset=utf-8
    ETag: "fb83cd304bacd599af0a1e73603500e5"
    Cache-Control: max-age=0, private, must-revalidate
    {
      "collection": {
        "version": "1.0",
        "href":    "...",
        "links":   [{ "rel": "next", "href": "..." }],
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
            { "name": "views",   "value": 1 }
          ]
        }, {
          "href":  "...",
          "links": [
            { "rel":  "canonical", "href": "..." },
            { "rel":  "icon",      "href": "..." }
          ],
          "data": [
            { "name": "id",      "value": 95 },
            { "name": "name",    "value": null },
            { "name": "private", "value": true },
            { "name": "views",   "value": 0 }
          ]
        }
        ...
        {
          "href":  "...",
          "links": [
            { "rel":  "canonical", "href": "..." },
            { "rel":  "icon",      "href": "..." }
          ],
          "data": [
            { "name": "id",      "value": 94 },
            { "name": "name",    "value": "api.md" },
            { "name": "private", "value": true },
            { "name": "views",   "value": 0 }
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

Follow the link `next` to get the next page of drops.

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops?page=2&per_page=20"

    HTTP/1.1 200 OK
    Content-Type: application/vnd.collection+json; charset=utf-8
    ETag: "ba401fa75b322ee994b109805871855c"
    Cache-Control: max-age=0, private, must-revalidate
    {
      "collection": {
        "version": "1.0",
        "href":    "...",
        "links": [
          { "rel":  "previous", "href": "..." },
          { "rel":  "next",     "href": "..." }
        ],
        "items": [...]
      }
    }
