---
layout: master
title: List Items
categories: items
---

# List Items

Page through your items. For the best performance, make sure your requests:

- Read and set [cookies](http://en.wikipedia.org/wiki/HTTP_cookie).
- Read the [Etag](http://en.wikipedia.org/wiki/HTTP_ETag) header on the responses to set the [If-None-Match](http://en.wikipedia.org/wiki/HTTP_ETag) header on
  future requests.
- Read the [Last-Modified](http://en.wikipedia.org/wiki/List_of_HTTP_headers) header on responses to set the [If-Modified-Since](http://en.wikipedia.org/wiki/List_of_HTTP_headers) header on future requests.

If you're lucky, the HTTP library you use will take care of this for you.

## Request

- Requires [authentication](/authentication/)
- HTTP Method: GET
- URL: http://my.cl.ly/items
- Optional paramters:
  - `page=1`: Page number starting at 1.
  - `per_page=5`: Number of items per page.
  - `type=image`: Filter items by type (image, bookmark, text, archive, audio, video, or unknown).
  - `deleted=true`: Show trashed items.

## Response

- Status: 200 OK
- Body:

      [{
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
        "deleted_at":   null
      }, {
        "href":         "http://my.cl.ly/items/1912565",
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
        "deleted_at":   null
      }, {
        "href":         "http://my.cl.ly/items/1912559",
        "name":         "CloudApp Logo.png",
        "private":      false,
        "url":          "http://cl.ly/2wr4",
        "content_url":  "http://cl.ly/2wr4/content",
        "item_type":    "image",
        "view_counter": 2,
        "icon":         "http://my.cl.ly/images/item_types/image.png",
        "remote_url":   "http://f.cl.ly/items/7c7aea1395c3db0aee18/CloudApp%20Logo.png",
        "redirect_url": null,
        "created_at":   "2010-10-23T19:50:13Z",
        "updated_at":   "2010-10-23T19:50:38Z",
        "deleted_at":   null
      }]

## Example

{: .shell}
    curl --digest -u arthur@dent.com:towel \
         -H "Accept: application/json" \
         "http://my.cl.ly/items?page=1&per_page=5"
