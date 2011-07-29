---
layout: master
title: List Items by Source
categories: items
---

# List Items by Source

Page through all of your items created using a specific application. See
[List Items](/list-items) for recommendations using this endpoint.

## Filtering Details

An item's `source` attribute is set to the User-Agent used to create the item.
The `source` parameter value is matched case insensitively against the word
boundaries of an item's `source` attribute. For example, if the User-Agent used
to create an item was `CloudApp/1.0.3`, it would be found by searching for
`CloudApp` but not `Cloud`. The User-Agent `Mozilla/5.0 Safari/534.48.3` could
be matched with `Mozilla`, `Safari/534`, or the like.

## Request

- Requires [authentication](/usage/#authentication)
- HTTP Method: GET
- URL: http://my.cl.ly/items?source=*Cloud*


## Response

- Status: 200 OK
- Body:

      [{
        "href":          "http://my.cl.ly/items/1912729",
        "name":          "My CloudApp",
        "private":       true,
        "subscribed":    false,
        "url":           "http://cl.ly/40b6ab341aca432a34ee",
        "content_url":   "http://cl.ly/40b6ab341aca432a34ee/content",
        "item_type":     "bookmark",
        "view_counter":  0,
        "icon":          "http://my.cl.ly/images/item_types/bookmark.png",
        "remote_url":    null,
        "redirect_url":  "http://my.cl.ly",
        "source":        "Cloud/1.5.1 CFNetwork/520.0.13 Darwin/11.0.0 (x86_64) (MacBookPro5%2C5)",
        "created_at":    "2010-10-23T20:10:37Z",
        "updated_at":    "2010-10-23T20:10:41Z",
        "deleted_at":    null
      }, {
        "href":          "http://my.cl.ly/items/1912565",
        "name":          "CloudApp",
        "private":       false,
        "subscribed":    false,
        "url":           "http://cl.ly/2wt6",
        "content_url":   "http://cl.ly/2wt6/content",
        "item_type":     "bookmark",
        "view_counter":  2,
        "icon":          "http://my.cl.ly/images/item_types/bookmark.png",
        "remote_url":    null,
        "redirect_url":  "http://getcloudapp.com",
        "source":        "Cloud/1.5.1 CFNetwork/520.0.13 Darwin/11.0.0 (x86_64) (MacBookPro5%2C5)",
        "created_at":    "2010-10-23T19:50:24Z",
        "updated_at":    "2010-10-23T19:50:39Z",
        "deleted_at":    null
      }, {
        "href":          "http://my.cl.ly/items/1912559",
        "name":          "CloudApp Logo.png",
        "private":       false,
        "subscribed":    false,
        "url":           "http://cl.ly/2wr4",
        "content_url":   "http://cl.ly/2wr4/CloudApp_Logo.png",
        "item_type":     "image",
        "view_counter":  85,
        "icon":          "http://my.cl.ly/images/new/item-types/image.png",
        "remote_url":    "http://f.cl.ly/items/7c7aea1395c3db0aee18/CloudApp%20Logo.png",
        "thumbnail_url": "http://thumbs.cl.ly/2wr4",
        "redirect_url":  null,
        "source":        "Cloud/1.5.1 CFNetwork/520.0.13 Darwin/11.0.0 (x86_64) (MacBookPro5%2C5)",
        "created_at":    "2010-10-23T19:50:13Z",
        "updated_at":    "2011-04-04T00:33:57Z",
        "deleted_at":    null
      }]

## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         "http://my.cl.dev/items?page=1&per_page=5&source=Cloud"
