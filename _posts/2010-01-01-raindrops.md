---
layout: master
title: Raindrops
categories: mac 
---

# Raindrops

Raindrops are an essential part of the CloudApp ecosystem: they enable ways for
the user to work with an application that may not fully work with the
pasteboard. They are essentially plug ins that hook into CloudApp and allow
you to respond to the Raindrop hotkey being triggered, in addition to being
able to initiate file uploads.

## How can Raindrops be used?

To give you an idea about how Raindrops can be used, and what functionality
they can provide, two first-party Raindrops can be examined. The
[Photoshop Raindrop](https://github.com/cloudapp/raindrops/tree/master/Photoshop)
will allow the frontmost document in Photoshop to be uploaded to CloudApp when the
Raindrop hotkey is pressed. Adobe applications do not write to the system pasteboard
until the application becomes inactive. Therefore, copying a section of a document and
hitting the clipboard hotkey will lead to unexpected results. A Raindrop, therefore,
would make a lot of sense. Another place where a Raindrop would be useful is with
auto-uploading of screenshots. Our
[Screenshot Raindrop](https://github.com/cloudapp/raindrops/tree/master/Screenshots) will
watch the user’s screen shot folder for new files, check them to see if they are
screenshots, and then upload them if so.

## Great! Now how do I get started?

Raindrops are Cocoa bundles. You can create one by going to *File > New > New
Project…* in Xcode and selecting the *Bundle* template from the *Framework & Library*
group. Make sure that your bundle uses the Cocoa framework.

Next, create a new file, subclass of `NSObject`. Add `CLRaindropProtocol.h` and
`CLRaindropHelperProtocol.h` to your project, under Classes. [You can find both files
on github](https://github.com/cloudapp/raindrops). The class you just created must
implement `CLRaindropProtocol`.

Now go into `Info.plist` and set the value of the `Principal Class` key to
`MyClass`, or whatever you named the class you created in the previous step. Edit the
build settings of your project to use `raindrop` as the `Wrapper Extension`.

Last but not least, add an empty Property List `Raindrop.plist` file to your project. Every
Raindrop must define [Raindrop-specific metadata](/raindrops-metadata/).

You now have everything in place and properly configured to build your Raindrop. Hooray!

## Two Different Kinds of Raindrops

We already talked about two Raindrops, Photoshop and Screenshots, remember? Well, it turns out
that those two Raindrops represent two different kinds of Raindrops. The Photoshop one uploads
content as soon as the user **triggers** it using the hotkey. The Screenshot Raindrop, on the other
hand, does upload **without being triggered** by the hotkey as soon as it detects a new screenshot.
As the latter one is constantly working in the background, we decided to label all Raindrops of
that kind as *downpour*. Fancy, eh?

Obviously, the way you implement those two Raindrops differs. But never fear! We’ll walk you through.

### Non-downpour Raindrops

Non-downpour Raindrops are fairly simple to implement. The `CLRaindopProtocol` protocol defines the
`pasteboardNameForTriggeredRaindrop` method which gets called as soon as the user
triggers your Raindrop. Your job is it to create a new `NSPasteboard` object, add content to it
and return its name. Here’s a quick example:

    @implementation MyClass
    
    - (NSString *)pasteboardNameForTriggeredRaindrop
    {
        // Assuming that doSomething returns the path to a file
        NSString *path = [self doSomething];
        NSURL *fileURL = [NSURL fileURLWithPath:path];
        
        // Create pasteboard with unique name
        NSPasteboard *pasteboard = [NSPasteboard pasteboardWithUniqueName];
        
        // Add an item
        NSPasteboardItem *item = [[NSPasteboardItem alloc] init];
        [item setString:[fileURL absoluteString] forType:(NSString *)kUTTypeFileURL];
        [pasteboard writeObjects:[NSArray arrayWithObject:item]];
        [item release];
        
        // Return the pasteboard name
        return [pasteboard name];
    }
    
    @end

Non-downpour Raindrops always have a target bundle identifier, which you **must** define using
[Raindrop metadata](/raindrops-metadata). CloudApp uses this bundle identifier to determine which
Raindrop to invoke if the user hits the hotkey. For example, if the user triggers a Raindrop
while Finder is the active application, it triggers the Raindrop that defines `com.apple.Finder`
as its target bundle identifier. CloudApp also takes care of launching end terminating your
Raindrop if the target application of your Raindrop launches or terminates.

### Downpour Raindrops

Implementing a downpour Raindrop requires a bit more work but still, CloudApp is doing nearly
all the heavy lifting for you. In contrast to non-downpour Raindrops, you are now responsible to
trigger an upload. You therefore need some kind of contact person who you can tell *“Hey there, I
have something to upload for you!”*. That’s where the `initWithHelper:` method comes in handy. The
`helper` object implements `CLRaindropHelperProtocol` and responds to `handlePasteboardWithName:`.
You can call this method at any given time to trigger an upload. As you probably already figured, it is
therefore a good idea to keep a reference to the `helper` object for later.

The rest of the implementation is almost similar to the non-downpour one. Once your Raindrop decides
to upload something, it creates a new `NSPasteboard` object, adds content and tells the helper the name
of that pasteboard. Again, here’s a quick example:

    @implementation MyClass
    
    - (id)initWithHelper:(id <CLRaindropHelperProtocol>)helper
    {
        if ((self = [super init])) {
            // Assuming that the MyClass @interface defines an _helper instance variable
            _helper = [helper retain];
        }
        return self;
    }
    
    - (void)eventCallback:(NSString *)path
    {
        // Something happend and you detected that this is of interest for your raindrop
        // Assuming that your raindrop passes the path of an existing file in
        NSURL *fileURL = [NSURL fileURLWithPath:path];
        
        // Create pasteboard with unique name
        NSPasteboard *pasteboard = [NSPasteboard pasteboardWithUniqueName];
        
        // Add an item
        NSPasteboardItem *item = [[NSPasteboardItem alloc] init];
        [item setString:[fileURL absoluteString] forType:(NSString *)kUTTypeFileURL];
        [pasteboard writeObjects:[NSArray arrayWithObject:item]];
        [item release];
        
        // Trigger upload
        [_helper handlePasteboardWithName:[pasteboard name]];
    }
    
    - (void)dealloc
    {
        [_helper release];
        [super dealloc];
    }
    
    @end

You **must** explicitly declare a Raindrop as downpour and describe what the downpour action
does using [Raindrop metadata](/raindrops-metadata).

## Supported Pasteboard Content

As you’ve seen, Raindrops make heavy use of `NSPasteboard` to exchange content with CloudApp. The following
section lists all content types that are currently supported by CloudApp.

- One or more items that conform to `kUTTypeFileURL` and reference an existing file for file uploads
- Exactly one item that conforms to `kUTTypeImage` and contains image data for an image file upload
- Exactly one item that conforms to `kUTTypeURL` and contains an URL for a bookmark
- Exactly one item that conforms to `kUTTypeText` and contains text for a text file upload

If the pasteboard item references an existing file (which is the case for `kUTTypeFileURL`), CloudApp uses
the filename to name the upload. If the item contains only content data (which is the case for everything
else), you’ll have to pass along a filename using `@"public.url-name"` as the pasteboard item type.
 
## More Examples

We’ve open-sourced all our [Raindrops on github](https://github.com/cloudapp/raindrops). Go ahead and
use them to get an idea how a complete Raindrop implementation looks like!
