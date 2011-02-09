---
layout: master
title: Delete Multiple Items
categories: items
---

# Delete Multiple Items

Send several items to the trash.

## Request

Pass an array containing the value of each item's `id` to be deleted.

- Requires [authentication](/usage/#authentication)
- HTTP Method: DELETE
- URL: http://my.cl.ly/items
- Body:

      { "item_ids": [ 1912729, 1912565 ] }

## Response

- Status: 200 OK
- Body:

      [{
        "id":           1912729,
        "href":         "http://my.cl.ly/items/1912729",
        "name":         "My CloudApp",
        "private":      true,
        "url":          "http://cl.ly/40b6ab341aca432a34ee",
        "content_url":  "http://cl.ly/40b6ab341aca432a34ee/content",
        "item_type":    "bookmark",
        "view_counter": 0,
        "icon":         "http://my.cl.ly/images/item_types/bookmark.png",
        "remote_url":   null,
        "redirect_url": "http://my.cl.ly",
        "created_at":   "2010-10-23T20:10:37Z",
        "updated_at":   "2010-10-23T20:10:41Z",
        "deleted_at":   "2010-10-25T14:37:43Z"
      }, {
        "id":           1912565,
        "name":         "CloudApp",
        "private":      false,
        "url":          "http://cl.ly/2wt6",
        "content_url":  "http://cl.ly/2wt6/content",
        "item_type":    "bookmark",
        "view_counter": 2,
        "icon":         "http://my.cl.ly/images/item_types/bookmark.png",
        "remote_url":   null,
        "redirect_url": "http://getcloudapp.com",
        "created_at":   "2010-10-23T19:50:24Z",
        "updated_at":   "2010-10-23T19:50:39Z",
        "deleted_at":   "2010-10-25T14:37:43Z"
      }]


## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         -H "Content-Type: application/json" \
         -X DELETE \
         -d '{ "item_ids": [ 16, 17, 18 ] }' \
         "http://my.cloudapp.local/items"


## Errors

If an item is unable to be deleted, its place in the array will be `null`.

- Status: 422 Unprocessable Entity
- Body:

      [
        {
          "id":           1912729,
          "href":         "http://my.cl.ly/items/1912729",
          "name":         "My CloudApp",
          "private":      true,
          "url":          "http://cl.ly/40b6ab341aca432a34ee",
          "content_url":  "http://cl.ly/40b6ab341aca432a34ee/content",
          "item_type":    "bookmark",
          "view_counter": 0,
          "icon":         "http://my.cl.ly/images/item_types/bookmark.png",
          "remote_url":   null,
          "redirect_url": "http://my.cl.ly",
          "created_at":   "2010-10-23T20:10:37Z",
          "updated_at":   "2010-10-23T20:10:41Z",
          "deleted_at":   "2010-10-25T14:37:43Z"
        },
        null
      ]
