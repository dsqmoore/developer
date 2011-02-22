---
layout: master
title: Raindrops
categories: mac 
---

# Raindrops

Raindrops are an essential part of the CloudApp ecosystem: they enable ways for
the user to work with an application that may not fully work with the
pasteboard. They are essentially plug ins that hook into CloudApp and allow
you to respond to the raindrop hotkey being triggered, in addition to being
able to initiate file uploads.

## How can Raindrops be used?

To give you an idea about how raindrops can be used, and what functionality
they can provide, two first-party raindrops can be examined. The Photoshop
raindrop will allow the frontmost document in Photoshop to be uploaded to
CloudApp when the raindrop hotkey is pressed. Adobe applications do not write
to the system pasteboard until the application becomes inactive. Therefore,
copying a section of a document and hitting the clipboard hotkey will lead to
unexpected results. A raindrop, therefore, would make a lot of sense. Another
place where a raindrop would be useful is with auto-uploading of screenshots.
Our Screenshot raindrop will watch the user’s screen shot folder for new files,
check them to see if they are screenshots, and then upload them if so.

Raindrops, by default, are only running (since as of 1.5, they are a separate
process) while their target application is running. However, if *downpour* is
enabled, the raindrop will be running at all times. This is useful for
raindrops like auto-uploading of screenshots that needs to be constantly
running.

## Great! Now how do I make one?

Raindrops are Cocoa bundles. You can create one by going to *File > New
Project* in Xcode.

Make sure the Framework is Cocoa. Name it however you wish, and then the
project will be created.

Next, create a new file, subclass of NSObject. Add CLRaindropProtocol.h and
CLRaindropHelperProtocol.h to your project, under Classes.

Now go into Info.plist and set the value of the Principal Class key to
TestRaindrop, or whatever you named your class.

#import “CLRaindropProtocol.h” in TestRaindrop.h (or whatever you named your
class) and declare that TestRaindrop implements CLRaindropProtocol.

Now, in TestRaindrop.m (again, whatever you named your class), you have a few
options.

First off, if you plan to be able to trigger uploads on your own (without being
first triggered by the raindrop hotkey), you need to implement:

    - (id)initWithHelper:(id <CLRaindropHelperProtocol>)helper;

Keep a reference of the helper for later.

If you want to be able to give upload info to Cloud, you need to implement:

    - (NSString *)pasteboardNameForTriggeredRaindrop;

What is all this pasteboard name stuff?

Cloud 1.5 has a new focus on the pasteboard.  We have found that it is a great
way to transfer data, and handle it in a way the user expects.  As a result,
all upload data input into Cloud will be handled using pasteboard.

Whenever you pass upload data to us, it’ll be in the form of a pasteboard name.
In the context of what most people will want to do, it’ll be:

    NSPasteboard *pasteboard = [NSPasteboard pasteboardWithUniqueName]; //Write pasteboard items here

    return [pasteboard name];

or.....

    [self.helperObject handlePasteboardWithName:[pasteboard name]];

    NSPasteboard *pasteboard = [NSPasteboard pasteboardWithUniqueName]; //Write pasteboard items here

    return [pasteboard name];

or.....

    [self.helperObject handlePasteboardWithName:[pasteboard name]];

## Raindrop Metadata

Every raindrop bundle **must** have a Raindrop.plist file in their Resources
folder.

Available Keys:

Key: CLRaindropCreator
Value: The creator of the raindrop. Currently this data is not displayed in the UI, but it may be in the future.

Key: CLRaindropName
Type: String
Value: The name of the raindrop.  This will be displayed in the Preferences window and used in other places throughout the UI.

Key: CLRaindropDescription
Type: String
Value: A brief description of the raindrop, and we mean brief.  This will be cut off in the Preferences UI if too long, in an attempt to have developers keep it short and sweet.

Key: CLRaindropURL
Type: String
Value: This is a URL that would be opened if they want more information about the raindrop or its developer.  Currently this is not used in the UI, but may be used in the future.

Key: CLRaindropTargetBundleID
Type: String
Value: If this raindrop should respond to the raindrop hotkey, this *must* be in Raindrop.plist.  This is the bundle identifier of the application for whom you want to be triggered for.  For example, if you want to have the raindrop be triggered when Finder is in front, this value would be “com.apple.Finder” without quotes.

Key: CLRaindropDownpourEnabled
Type: Boolean
Value: If your raindrop needs to be running at all times (instead of only while the target application is open), this should be YES.

## Great! Do you have a central repository of raindrops?

Yes! We will be filling this section in with more information as we are able to share it.
