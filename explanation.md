<!-- This document is an example of a topic I wrote for my previous employer Evolutionizer. Their EVO-Cloud product uses a dashboard to host one or more modules that each perform a single specific function such as displaying a list, peforming financial calculations, and so on. By combining several modules on the dashboard, users can create multi-stafe processes to achieve their goals. The aim of topics like this was to describe a module in isolation without referencing how to create or configure it, as that information was written in a dedicated configuration manual. The topic concludes with several examples of how the module would be configured and used within a dashboard to help give users the full context of its application. I have removed anything specific to Evolutionizer and kept the content generic.-->

# Using the Connector Module

![moduleheader](https://github.com/gltechwriting/gltechwritingrepo/blob/main/Portfolio/images/connectormoduleheader.png)

## Overview

The **Connector** module lets users program one or more API calls to a compatible external REST API. You can then use data returned by the Connector module throughout our product in other modules, such as a **List** module to display data or a **Transformation** module to perform one or more operations against the data. The Connector module is typically used with platforms such as Google to report traffic data to our product pages, though it can be used to do anything the target API will allow.

**Note:** Only users with the *Configurator* or *Administrator* role can configure the Connector module.

## Compatibility

The Connector is currently compatible with the following APIs:

- Google (Analytics, Big Query, Sheets)
- Facebook (AdInsights, Content Insights)
- AWS S3
- Microsoft SQL Server
- Spotify

## Using the Connector Module

The Connector module has a wide range of uses and you will see one in every dashboard. While each Connector module is specific to the dashboard it is used in, you will interact with it the same way throughout our product. We will guide you through the interface and some common examples in this topic.

### Interface and Appearance

The following screenshot shows the Connector module on a dashboard with all interface options active. The example below has been configured to return traffic statistics for our homepage from Google Analytics. As such, the module has only been configured to make a single GET request and there is no filtering applied.

**Note:** If you do not have the *Configurator* or *Administrator* user roles, all of the fields described below will be read only.

![modulecallouts](https://github.com/gltechwriting/gltechwritingrepo/blob/main/Portfolio/images/connectormoduleheadercallouts.png)

|Number|Item|Description|
|---|---|---|
|1|Module type|Connector module.|
|2|Module title|In this case, "Our Homepage Traffic Statistics".|
|3|Request field|Choose the request type, from GET, POST, and PUT. Enter the API URL. Use 'Send' to make the request.|
|4|Export|Select this to export the configuration file for this module. You can then import the configuration file using another Connector module to duplicate the configuration.|
|5|Schedule|Use the drop-down menus to select a frequency. The module will run automatically according to the specified frequency.|
|6|Headers|Enter header values here.|
|7|Parameters|Enter parameter values here.|
|8|Authorization|Enter any authentication details here.|
|9|Body|Enter body text here.|
|10|Search field|Enter a partial or complete string to filter data within the module.|
|11|Response field|The JSON response from the server.|
|12|Status|Status code of the response.|

## Connector Module Examples

### Google Analytics

The following example shows a Connector module configured to return site traffic data from Google Analytics.

![example](https://github.com/gltechwriting/gltechwritingrepo/blob/main/Portfolio/images/connectormoduleheaderexample.png)

Modules like this are very useful for reporting detailed, up-to-date information about traffic to our website. We are able to see in real-time the impact of product releases, news items, etc as they happen.

### Spotify

We have designed an example using a Connector module configured to return data about a specific artist from Spotify. The full example was built using the walkthrough described in the [Connector Module Worked Example](https://github.com/gltechwriting/gltechwritingrepo/blob/main/Portfolio/how-to-guide.md), which uses the [Get Artist's Top Tracks](https://developer.spotify.com/documentation/web-api/reference/get-an-artists-top-tracks) endpoint. Some of our users are involved in social media, so returning statistics about music artists is helpful when creating content for our audience.

## Useful Information

- You can configure the Connector module to automatically make API calls according to a defined schedule, or manually by users when required.
- You can save and export a Connector module configuration for quick and easy re-use elsewhere.
- You can include as many Connector modules on a dashboard as required. You should always be considerate of the potential impact on traffic and latency if you are making too many requests to the same target on the same dashboard.