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
    ETag: "5f4dbdf11727d52c5191e1e30ff766a4"
    Cache-Control: max-age=0, private, must-revalidate
    {
      "collection": {
        "version": "1.0",
        "href": "http://api.getcloudapp.com/drops?page=1&per_page=20",
        "links": [{
            "rel": "next",
            "href": "http://api.getcloudapp.com/drops?page=2&per_page=20"
        }],
        "items": [{
          "href": "...",
          "data": [
            { "name": "id",    "value": 101 },
            { "name": "name",  "value": "Awesome Drop 1" },
            { "name": "views", "value": 1 }
          ]
        }, {
          "href": "...",
          "data": [
            { "name": "id",    "value": 95 },
            { "name": "name",  "value": "Awesome Drop 2" },
            { "name": "views", "value": 0 }
          ]
        },
        ...
        {
          "href": "...",
          "data": [
            { "name": "id",    "value": 94 },
            { "name": "name",  "value": "api.md" },
            { "name": "views", "value": 0 }
          ]
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
        "href": "http://api.getcloudapp.com/drops?page=2&per_page=20",
        "links": [{
          "rel": "previous",
          "href": "http://api.getcloudapp.com/drops?page=1&per_page=3",
        }, {
          "rel": "next",
          "href": "http://api.getcloudapp.com/drops?page=3&per_page=3"
        }]
        "items": [...],
      }
    }
