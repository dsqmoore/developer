---
layout: master
title: Stream Items
categories: items
---

# Stream Items

Connect to a socket and listen as items for an account are created, updated, and
deleted in real time. That's right. No more polling the
[list items API][list-items] looking for changes!

We use [Pusher] for websocket support. Grab an
[open source API library][pusher-libs] in the langage of your choice and follow
along. The examples below make use of their JavaScript client to connect to a
socket and listen for events on a channel.


## Gather Socket Details

The first step is to gather some details about the socket in order to connect.
These details are available via the [view account details] endpoint. Here's an
excerpt:

    {
      "socket": {
        "auth_url": "http://my.cloudapp.local/pusher/auth",
        "api_key":  "36b8e92a50487f79cbb3",
        "app_id":   "4072",
        "channels": {
          "items": "private-items_1"
        }
      }
    }


## Configure Pusher

Next, pass this data along to Pusher and subscribe to the channel. Assuming the
response from the above API call was stored in the variable named `account`,
it would look something like:

    // Use JSONP because it's a cross-domain request.
    Pusher.channel_auth_transport = 'jsonp';
    Pusher.channel_auth_endpoint  = account.socket.auth_url;


## Subscribe and Listen

Now let's get down to business. Subscribe to the items channel and listen for
one of more of the events `"create"`, `"update"`, or `"delete"` which will be
dispatched as items are, you guessed it, created, updated, or deleted.

    var itemsChannel = new Pusher(account.socket.api_key)
                             .subscribe(account.socket.channels.items)

    itemsChannel.bind('create', function(data) { });
    itemsChannel.bind('update', function(data) { });
    itemsChannel.bind('delete', function(data) { });

The `data` passed to the above callback handlers is idential to the
[list items API][list-items].

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



[list-items]: /list-items
[pusher]: http://pusherapp.com
[pusher-libs]: http://pusherapp.com/docs/libraries
[pusher-docs]: http://pusherapp.com/docs
[view account details]: /view-account-details
