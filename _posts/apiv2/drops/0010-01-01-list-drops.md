---
layout: apiv2
title: List Drops
categories: drops
---

# List Drops

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
        "links":   [{ "rel": "next", "href": "..." }],
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
              { "rel": "icon",       "href": "..." }
            ],
            "data": [
              { "name": "id",           "value": 17009086 },
              { "name": "name",         "value": "Bing" },
              { "name": "private",      "value": false },
              { "name": "bookmark_url", "value": "http://bing.com" },
              { "name": "views",        "value": 4 }
            ]
          },
          ...
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
              { "name": "id",           "value": 13950097 },
              { "name": "name",         "value": "favicon.ico" },
              { "name": "private",      "value": true },
              { "name": "bookmark_url", "value": null },
              { "name": "views",        "value": 29 }
            ]
          }
        ]
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
        "links":   [
          { "rel": "next",     "href": "..." },
          { "rel": "previous", "href": "..." }
        ],
        "template": {...},
        "items":    [...]
      }
    }
