---
layout: apiv2
title: Link Relations
categories: summary
---

# Link Relations

A brief description of all the link relations used throughout the API. When
possible, link relations from [RFC5988][standard-links] are used.

[standard-links]: http://www.iana.org/assignments/link-relations/link-relations.xml


 - `/rels/account`: View authenticated user's CloudApp account.
 - `/rels/authenticate`: POST account credentials to retrieve authentication
   token.
 - `/rels/drops`: List authenticated user's drops.

## Drop Collection

 - `next`: View the next page of drops.
 - `previous`: View the previous page of drops.
 - `root`: _I don't think this link is necessary and will likely be remove._
 - `/rels/trash-drops`: POST a list of drop IDs to move to the trash.
 - `/rels/restore-drops`: POST a list of drop IDs to restore from the trash.
 - `/rels/delete-drops`: POST a list of drop IDs to immediately and permanently
   delete.

## Drop Item

 - `alternate`: Alternate public representations of a drop (direct content link,
   force download).
 - `canonical`: A drop's public, sharable link.
 - `icon`: A drop's publicly viewable thumbnail.
