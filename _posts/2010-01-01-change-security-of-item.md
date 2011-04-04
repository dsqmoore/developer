---
layout: master
title: Change Security Of Item
categories: items
---

# Change Security of Item

Modify an item with a private URL to have a public URL or vice versa.

## Request

- Requires [authentication](/usage/#authentication)
- HTTP Method: PUT
- URL: Value of item's `href` attribute. _(e.g., http://my.cl.ly/items/1912565)_
- Body:

      {
        "item": {
          "private": false
        }
      }

## Response

- Status: 200 OK
- Body:

      {
        "href":         "http://my.cl.ly/items/1912565",
        "name":         "CloudApp",
        "private":      false,
        "url":          "http://cl.ly/2wt6",
        "content_url":  "http://cl.ly/2wt6",
        "item_type":    "bookmark",
        "view_counter": 0,
        "icon":         "http://my.cl.ly/images/item_types/bookmark.png",
        "remote_url":   null,
        "redirect_url": "http://getcloudapp.com",
        "created_at":   "2010-10-23T21:15:21Z",
        "updated_at":   "2010-10-23T21:17:04Z",
        "deleted_at":   null
      }

## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         -H "Content-Type: application/json" \
         -d \
           '{
              "item": {
                "private": false
              }
            }' \
         -X PUT \
         "http://my.cl.ly/items/1912565"
