---
layout: apiv2
title: Media Type
categories: summary
---

# Media Type

The CloudApp API accepts and returns only the [Collection+JSON][collection-json]
media type. For convenience, this media type is also used for any generic
`application/json` requests.

A Collection+JSON response will always be an object with a
single `collection` attribute. The `collection` will always have a `version` and
`href` which are strings and an array of `items`. Optionally it may have an
array of `links` or a `template`.

Read the short [Collection+JSON format documention][collection-json-format] for
the exact details or take a look at [a few examples][collection-json-examples].

[collection-json]:          http://www.amundsen.com/media-types/collection
[collection-json-format]:   http://amundsen.com/media-types/collection/format
[collection-json-examples]: http://amundsen.com/media-types/collection/examples


## Examples

Response when requesting an account's token.

    {
      collection: {
        version: "1.0",
        href: "http://api.getcloudapp.com/account/token",
        items: [{
          href: "http://api.getcloudapp.com/account/token",
          data: [{ name: "token", value: "0gc504cf7e4a51ff8119" }]
        }],
        template: {
          data: [
            { name: "email",    value: "" },
            { name: "password", value: "" }
          ]
        }
      }
    }

Listing drops.

    {
      collection: {
        version: "1.0",

        href: "http://api.getcloudapp.com/drops?page=2&per_page=5",
        links: [
          { rel: "next",     href: "http://api.getcloudapp.com/drops?page=1&per_page=5" },
          { rel: "previous", href: "http://api.getcloudapp.com/drops?page=3&per_page=5" }
        ],
        items: [{
          href: "http://api.getcloudapp.com/drops/1",
          links: [{
            { rel: "canonical", href: "http://cl.ly/40b6ab341aca432a34ee" },
            { rel: "icon",      href: "http://my.cl.ly/images/item_types/bookmark.png" }
          ],
          data: [
            { name: "name",           value: "My CloudApp" },
            { name: "private",        value: true },
            { name: "bookmark_url",   value: "http://my.cl.ly" }
          ]
        }, {
          href: "http://api.getcloudapp.com/drops/2",
          links: [{
            { rel: "canonical", href: "http://cl.ly/2wr4" },
            { rel: "alternate", href: "http://cl.ly/2wr4/CloudApp%20Logo.png" },
            { rel: "icon",      href: "http://my.cl.ly/images/item_types/bookmark.png" }
          ],
          data: [
            { name: "name",           value: "CloudApp Logo.png" },
            { name: "private",        value: false },
            { name: "content_length", value: 3516 }
          ]
        }],
        template: {
          data: [
            { name: "name",           value: "" },
            { name: "private",        value: true },
            { name: "bookmark_url",   value: "" },
            { name: "content_length", value: 0 }
          ]
        }
      }
    }
