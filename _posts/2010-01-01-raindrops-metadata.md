---
layout: master
title: Raindrops Metadata
categories: mac 
---

# Raindrops Metadata

Every Raindrop bundle **must** have a `Raindrop.plist` file in their Resources folder and **must**
define all required keys. The following is all available keys.

## General Keys

### CLRaindropCreator
- **Type:** String
- **Value:** The creator of the Raindrop
- **Note:** *Optional*. Currently this data is not displayed in the UI, but it may be in the future.

### CLRaindropName
- **Type:** String
- **Value:** The name of the Raindrop
- **Note:** *Required*. This will be displayed in the Preferences window and used in other places throughout the UI.

### CLRaindropDescription
- **Type:** String
- **Value:** A brief description of the raindrop, and we mean brief
- **Note:** *Required*. This will be cut off in the Preferences UI if too long, in an attempt to have developers keep it short and sweet.

### CLRaindropURL
- **Type:** String
- **Value:** A URL that provides further information about the raindrop or its developer
- **Note:** *Optional*. Currently this is not used in the UI, but may be used in the future.

## Non-downpour Keys

The following keys are only required for non-downpour Raindrops.

### CLRaindropTargetBundleID
- **Type:** String
- **Value:** The bundle identifier of the application for whom you want to be triggered when it is frontmost.
- **Note:** *Required*. For example, if you want to have the raindrop be triggered when Finder is in front, this value would be `com.apple.Finder`

## Downpour Keys

The following keys are only required for downpour Raindrops.

### CLRaindropDownpourEnabled
- **Type:** Boolean
- **Value:** Indicates that your Raindrop uses downpour
- **Note:** *Required*.

### CLRaindropDownpourActionDescription
- **Type:** String
- **Value:** A very brief description what the downpour action of your raindrop does
- **Note:** *Required*. This will be presented in the dropdown UI to let the user enable or disable downpour raindrops quickly.
