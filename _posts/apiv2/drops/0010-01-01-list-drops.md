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
