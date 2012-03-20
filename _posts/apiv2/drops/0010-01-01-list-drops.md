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
        "href":    "/drops?page=1&per_page=20",
        "links":   [{
          "rel":  "next",
          "href": "/drops?page=2&per_page=20"
        }],
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
            { "name": "views",   "value": 1 }
          ]
        }, {
          "href":  "/drops/95",
          "links": [{
            "rel":  "canonical",
            "href": "http://localhost:3000/2U1b1J363E47170M303Z"
          }, {
            "rel":  "icon",
            "href": "http://localhost:3001/2U1b1J363E47170M303Z"
          }],
          "data": [
            { "name": "id",      "value": 95 },
            { "name": "name",    "value": null },
            { "name": "private", "value": true },
            { "name": "views",   "value": 0 }
          ]
        }
        ...
        {
          "href":  "/drops/94",
          "links": [{
            "rel":  "canonical",
            "href": "http://localhost:3000/081T3q0B0b2T160M3n0V"
          }, {
            "rel":  "icon",
            "href": "http://localhost:3001/081T3q0B0b2T160M3n0V"
          }],
          "data": [
            { "name": "id",      "value": 94 },
            { "name": "name",    "value": "api.md" },
            { "name": "private", "value": true },
            { "name": "views",   "value": 0 }
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
        "href":    "/drops?page=2&per_page=20",
        "links": [{
          "rel":  "previous",
          "href": "/drops?page=1&per_page=20"
        }, {
          "rel":  "next",
          "href": "/drops?page=3&per_page=20"
        }],
        "items": [...]
      }
    }
