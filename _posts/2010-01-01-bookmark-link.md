---
layout: master
title: Bookmark Link
categories: items
---

# Bookmark Link

Create a bookmark to a URL.


## Request

- Requires [authentication](/usage/#authentication)
- HTTP Method: POST
- URL: http://my.cl.ly/items
- Body:

      {
        "item": {
          "name":         "CloudApp",
          "redirect_url": "http://getcloudapp.com"
        }
      }


## Response

- Status: 200 OK
- Body:

      {
        "href":         "http://my.cl.ly/items/1912565",
        "name":         "CloudApp",
        "private":      true,
        "url":          "http://cl.ly/4febbfdfb185c63d5e14",
        "content_url":  "http://cl.ly/4febbfdfb185c63d5e14/content",
        "item_type":    "bookmark",
        "view_counter": 0,
        "icon":         "http://my.cl.ly/images/item_types/bookmark.png",
        "remote_url":   null,
        "redirect_url": "http://getcloudapp.com",
        "created_at":   "2010-10-23T19:50:24Z",
        "updated_at":   "2010-10-23T19:50:39Z",
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
                "name":         "CloudApp",
                "redirect_url": "http://getcloudapp.com"
             }
           }' \
         "http://my.cl.ly/items"


## Errors

There may be one or more errors preventing the bookmark from being created. If
that's the case, the following response will be returned:

- Status: 422 Unprocessable Entity
- Body:

      [ "URL can't be blank" ]
