<!-- This is an example of how I have written release notes in previous roles. Each team I have worked with had their own processes and preferences, this is only one example. -->

# Release Version 2025.9.6

We are pleased to present the following updates in the latest release of our product.

**API**

We have added a brand-new Connector module feature that will enable you to interact with a number of external REST APIs to extract data for use in our product.

**User Interface**

We have made several updates to the color palette used throughout our user interface. All dialog windows and interactive elements now share the same color scheme and we have removed unecessary or confusing colors to improve clarity and usability.

**File Import**

The File Import process has been simplified and expanded to include more formats.

## New Features

### API

Users can now enjoy our brand-new **Connector** module. Using this feature you will be able to configure one or more calls to a range of external REST APIs, such as Google Analytics, to return data for use in our product. Only users with *Configurator* or *Administrator* privileges can configure the Connector, but users of all roles can access and interact with the data that is returned.

The Connector is currently compatible with the following APIs:

- Google (Analytics, Big Query, Sheets)
- Facebook (AdInsights, Content Insights)
- AWS S3
- Microsoft SQL Server
- Spotify

The Connector will be expanded in future releases to access many more APIs, so watch this space!

## Enhancements

### User Interface

As part of our ongoing updates to the interface and appearance of our product, we have streamlined the visual appearance of all UI elements. All elements now use consistent colors and all visual elements share the same modern styling. We have also simplified the UI, using more click-through menus and keyboard shortcuts to greatly improve usability. User interface elements will also adapt correctly when using our product on different device types.

### File Import

The File Import tool has been overhauled and can now import many more file types. Users with the *Administrator* role can connect the File Import tool to a cloud warehouse, such as Amazon S3, to import content from the internet.

The File Import tool now has a dedicated entry in the right-hand sidebar and can be accessed from the File -> Data options menu.

The full list of compatible file types and storage providers are in the user documentation for the File Import tool.

## Bug Fixes

We have resolved the following issues as part of the current release.

### File Import Timeout

Previously, the File Import process could encounter fatal errors which resulted in the process stalling and running until it timed out. The File Import tool has now been completely redesigned and this issue will not occur again.

### Calendar

We have resolved an issue where the Calendar tool would not update correctly when switching between timezones.

### User Roles

We have resolved an issue where *Administrator* users occassionally could not assign new roles to certain users.

## Hotfix 2025.9.6.1

Resolved a potential security vulnerability when remote users accessed our product using a VPN.
