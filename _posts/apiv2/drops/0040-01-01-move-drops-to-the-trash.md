---
layout: apiv2
title: Move Drops to the Trash
categories: drops
---

# Move Drops to the Trash

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 200 OK
    Content-Type: application/vnd.collection+json; charset=utf-8
    ETag: "fb83cd304bacd599af0a1e73603500e5"
    {
      "collection": {
        "version":   "1.0",
        "href":      "/drops?page=1&per_page=20",
        "links":     [...],
        "items":     [...],
        "templates": [{
          "rel":    "/rels/trash-drops",
          "href":   "/drops",
          "data":   [{ "name": "drop_ids", "value": [] }]
        }, {
          "rel":    "/rels/delete-drops",
          "href":   "/drops?filter=trash",
          "data":   [{ "name": "drop_ids", "value": [] }]
        }, {
          "rel":    "/rels/restore-drops",
          "href":   "/drops",
          "data":   [{ "name": "drop_ids", "value": [] }]
        }]
      }
    }

Fill the `/rels/trash-drops` template with an array of the drop IDs to move to
the trash.

    $ curl -i -H 'Authorization: Token token="0gc504cf7e4a51ff8119"' \
           -H "Content-Type: application/json" \
           -X DELETE \
           -d '{
                 "drop_ids": [ 1, 2, 3, 4 ]
               }' \
           "http://api.getcloudapp.com/drops"

    HTTP/1.1 204 No Content
    Cache-Control: no-cache
