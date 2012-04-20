---
layout: apiv2
title: Media Type
categories: summary
---

# Media Type

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][rfc2119].

The CloudApp media type accepts and returns only the [Collection+JSON][cj] media
type. For convenience, this media type is also used for any requests asking for
the generic `application/json` media type.

## Design Characteristics

 - **Base Format:** [Collection+JSON][cj]
 - **State Transfer:** Ad-Hoc (via [Collection+JSON templates][cj])
 - **Domain Style:** Specific
 - **Application Flow:** Applied
 - **H-Factors:** [LE, LO, LT, LN, LI, CL][h-factors]

## Semantic Profile

### Root Collection

The collection SHOULD have a `drops` and `account` link.

    // sample root collection
    {
      "href" : URI,
      "links" :
      [
        { "href" : URI, "rel" : "drops" },
        { "href" : URI, "rel" : "account" }
      ]
    }

### Unauthorized Collection

The `template` SHOULD contain both an `email` and `password` property. The
`template` is used to create a token which is used for authentication.

    // sample unauthorized collection
    {
      "href" : URI,
      "template" :
      {
        "data" :
        [
          { "name" : "email",    "value" : null },
          { "name" : "password", "value" : null }
        ]
      }
    }

### Token Collection

Each `item` MUST be a token. The collection SHOULD have a `root` link.

    // sample token collection
    {
      "href" : URI,
      "links" :
      [
        { "href" : URI, "rel" : "root" }
      ],
      "items" : [TOKEN]
    }

### Token

A token SHOULD have a `token` property whose value MAY be added to the
`Authorization` header in the format `Token token="TOKEN"` to access resources
which require authentication.

    // sample token item
    {
      "href" : URI,
      "data" :
      [
        { "name" : "token", "value" : "0gc504cf7e4a51ff8119" }
      ]
    }

### Drop Collection

Each `item` MUST be a drop. It SHOULD have a `root` link and MAY have a `next`
and `previous` link. Creating a new drop SHOULD include either a `bookmark_url`
or `file_size` property. The response will be a drop collection if
`bookmark_url` is given and will be an upload collection if `file_size` is
given.

    // sample drop collection
    {
      "href" : URI,
      "links" :
      [
        { "href" : URI, "rel" : "root" },
        { "href" : URI, "rel" : "next" },
        { "href" : URI, "rel" : "previous" }
      ],
      "template" :
      {
        "data" :
        [
          { "name" : "name",         "value" : null },
          { "name" : "private",      "value" : true },
          { "name" : "bookmark_url", "value" : null },
          { "name" : "file_size",    "value" : null }
        ]
      },
      "items" : [DROP]
    }

### Drop

A drop MAY have any of the following properties: `id` (REQUIRED), `private`
(OPTIONAL), `name` (OPTIONAL), `views` (OPTIONAL). A drop SHOULD have a `root`
and `collection` link and MAY have any of the following links: `canonical`,
`icon`, `embed`, `download`

    // sample drop item
    {
      "href" : URI,
      "links" :
      [
        { "href" : URI, "rel" : "canonical" },
        { "href" : URI, "rel" : "icon" }
      ],
      "data" :
      [
        { "name" : "id",      "value" : 123 },
        { "name" : "private", "value" : true },
        { "name" : "name",    "value" : "The Guide" },
        { "name" : "views",   "value" : 42 }
      ]
    }

### Upload Collection

Each `item` MUST be a drop. The `template` MUST be filled with the file to be
uploaded, MUST be encoded as `application/x-www-form-urlencoded`, and MUST be
sent as an HTTP POST to the collection's `href`.

**Note:** According to [Amazon's documentation][s3-docs], any parameter after
`file` is ignored. Make sure `file` is the last parameter in the encoded request
or the upload may be rejected.

[s3-docs]: http://developer.amazonwebservices.com/connect/entry.jspa?externalID=1434

    // sample upload collection
    {
      "href" : URI,
      "template" :
      {
        "data" :
        [
          { "name": "success_action_redirect", "value": "http://api.getcloudapp.com/drops/140/s3" },
          { "name": "AWSAccessKeyId", "value": "AKIAIDPUZISHSBEOFS6Q" },
          { "name": "key",            "value": "items/1L2c052P0F0V2X1i0r30/${filename}" },
          { "name": "policy",         "value": "eyJleHBpcmF0aW9uIjoiMjAxM..." },
          { "name": "signature",      "value": "6n0Y1P8y6wgMGcKZ2shxiodgDW4=" },
          { "name": "acl",            "value": "public-read" },
          { "name": "file",           "value": null }
        ]
      },
      "items" : [DROP]
    }

### Link Relations

 - `root`: A root collection.
 - `drops`: A drops collection.
 - `drop`: A drops collection containing a single drop.
 - `next`: The next set of items in the collection.
 - `previous`: The previous set of items in the collection.
 - `collection`: The collection of items containing the resource.
 - `canonical`: A drop's sharable URL. _This link is publicly accessible._
 - `download`: Download a drop's content. _This link is publicly accessible._
 - `embed`: The drop's content. _This link is publicly accessible._
 - `icon`: The drop's thumbnail. _This link is publicly accessible._

## Acknowledgements

Special thanks to [Mike Amundsen][mike-amundsen] for giving feedback on using
Collection+JSON as well as general guidance on hypermedia APIs. His book
[Building Hypermedia APIs with HTML5 and Node][building-hypermedia-apis] as well
as [Steve Klabnik's][steve-klabnik] living book
[Designing Hypermedia APIs][designing-hypermedia-apis] have been invaluable
resources.


## References

 - [Key words for use in RFCs to Indicate Requirement Levels \[RFC2119\]][rfc2119]
 - [Collection+JSON][cj]
 - [H-Factors][h-factors]
 - [Building Hypermedia APIs with HTML5 and Node][building-hypermedia-apis]
 - [REST APIs must be hypertext-driven][rest-apis-must-be-hypertext]
 - [Designing Hypermedia APIs][designing-hypermedia-apis]
 - [Date and Time on the Internet: Timestamps \[RFC3339\]][rfc3339]


[cj]: http://www.amundsen.com/media-types/collection/
[h-factors]: http://amundsen.com/hypermedia/hfactor/
[rest-apis-must-be-hypertext]: http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven
[building-hypermedia-apis]: http://www.amazon.com/gp/product/1449306578
[designing-hypermedia-apis]: http://designinghypermediaapis.com
[mike-amundsen]: http://amundsen.com
[steve-klabnik]: http://designinghypermediaapis.com
[rfc2119]: http://tools.ietf.org/html/rfc2119
[rfc3339]: http://tools.ietf.org/html/rfc3339
