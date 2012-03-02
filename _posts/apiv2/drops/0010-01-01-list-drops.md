---
layout: apiv2
title: List Drops
categories: drops
---

# List Drops

    $ curl -i -H 'Authorization: Token token="9fb493be7e4441ff7117"' "http://api.getcloudapp.com/drops"
    HTTP/1.1 200 OK
    Cache-Control: max-age=0, private, must-revalidate
    Content-Type: application/vnd.cloudapp+json; charset=utf-8
    Etag: "f919426ed6d12da04b1fd8391d64c0c1"
    Link: <http://api.getcloudapp.com/drops?page=1&per_page=20>; rel="self",
          <http://api.getcloudapp.com/drops?page=2&per_page=20>; rel="next"

    [{...}, {...}, ...]

Follow the link `next` to get the next page of drops.

    $ curl -i -H 'Authorization: Token token="9fb493be7e4441ff7117"' "http://api.getcloudapp.com/drops?page=2&per_page=20"
    HTTP/1.1 200 OK
    Cache-Control: max-age=0, private, must-revalidate
    Content-Type: application/vnd.cloudapp+json; charset=utf-8
    Etag: "bdce0537e96fabf4897f5517ac2fad6a"
    Link: <http://api.getcloudapp.com/drops?page=2&per_page=20>; rel="self",
          <http://api.getcloudapp.com/drops?page=1&per_page=20>; rel="previous",
          <http://api.getcloudapp.com/drops?page=3&per_page=20>; rel="next"

    [{...}, {...}, ...]


Sample `application/vnd.collection+json` representation.

    {
      collection: {
        version: "1.0",

        href: "http://api.getcloudapp.com/drops?page=2&per_page=5",
        links: [{
          rel:  "next",
          href: "http://api.getcloudapp.com/drops?page=1&per_page=5"
        }, {
          rel:  "previous",
          href: "http://api.getcloudapp.com/drops?page=3&per_page=5"
        }],
        items: [{
          href: "http://api.getcloudapp.com/drops/1",
          links: [{
            rel:  "canonical",
            href: "http://cl.ly/40b6ab341aca432a34ee"
          }, {
            rel:  "icon",
            href: "http://my.cl.ly/images/item_types/bookmark.png"
          }],
          data: [
            { name: "name",           value: "My CloudApp" },
            { name: "private",        value: true },
            { name: "bookmark_url",   value: "http://my.cl.ly" }
          ]
        }, {
          href: "http://api.getcloudapp.com/drops/2",
          links: [{
            rel:  "canonical",
            href: "http://cl.ly/2wr4"
          }, {
            rel:  "alternate",
            href: "http://cl.ly/2wr4/CloudApp%20Logo.png"
          }, {
            rel:  "icon",
            href: "http://my.cl.ly/images/item_types/bookmark.png"
          }],
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
