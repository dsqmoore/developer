---
layout: apiv2
title: Update Drop
categories: drops
---

# Update Drop

Get a drop's details either by [listing drops](/list-drops) or
[viewing a single drop](/view-single-drop).

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
          "links": [...],
          "data":  [
            { "name": "id",      "value": 101 },
            { "name": "name",    "value": null },
            { "name": "private", "value": true },
            { "name": "views",   "value": 2 }
          ]
        }],
        "templates": [{
          "rel":  "/rels/create",
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

Copy the drop's `data` into the `/rels/create` template igoring any attributes
that don't exist in the template. Update any desired attributes. Encode each
name and value pair in the template as `application/x-www-form-urlencoded` or
`application/json` and POST it to the drop's `href`.

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           -H "Content-Type: application/json; charset=utf-8" \
           -X POST \
           -d '{
                 "name":         "Renamed Drop",
                 "private":      true,
                 "bookmark_url": null,
                 "file_size":    null
               }' \
           "http://api.getcloudapp.com/drops/101"

    HTTP/1.1 200 OK
    Content-Type: application/vnd.collection+json; charset=utf-8
    {
      "collection": {
        "version": "1.0",
        "href":    "...",
        "items": [{
          "href":  "...",
          "links": [...],
          "data":  [
            { "name": "id",      "value": 101 },
            { "name": "name",    "value": "Renamed Drop" },
            { "name": "private", "value": true },
            { "name": "views",   "value": 2 }
          ]
        }],
        "templates": [{
          "rel":  "/rels/create",
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
