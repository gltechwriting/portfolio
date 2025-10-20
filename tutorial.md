<!-- This document is based on a walkthrough I wrote for my previous employer Matillion and describes how to connect to Spotify's API to extract data about a given artist. Matillion's Data Loader product is designed to extract data from one or more APIs, perform various transformations, and load the resulting modified data into a cloud warehouse. As such, this example could be applied to any cloud data provider the user could want to use and describes a complete beginning-to-end process any user could follow. I have modified this example to remove anything specific to Matillion, and changed to the context to be similar to the other examples. -->

# Connector Module Worked Example

The following guide describes how to use the Connector module. The Connector module can extract data from any compatible REST API. Because the module has no endpoints or authentication details, you will need to acquire and provide this information yourself.

The example we are going to follow uses the Spotify API to perform a fairly basic data extraction call. The guide is written to effectively guide you through the process, including authentication steps.

Refer to Spotify's [Web API](https://developer.spotify.com/documentation/web-api) documentation for more information.

## Authentication

You will require an **access token** to be able to make calls to Spotify's API, which first requires a valid user account and the creation of an app. For reference, the process we are following is documented [here](https://developer.spotify.com/documentation/web-api/tutorials/getting-started), but we will go through it fully for clarity.

1. Log in to the Spotify [developer dashboard](https://developer.spotify.com/dashboard) using your Spotify account. If you don't have one, you will need to create one.
2. Click **Create App** to begin creating a new App. Complete the fields as required. We used our Dashboard URI as the Redirect URI but anything can be used. Click **Save**.
3. You will return to the main dashboard for your app. Click **Settings** in the top-right corner to view the **Basic Information** for your app, including the **Client ID** and **Client Secret**. You will need to click **View client secret** to access the client secret.
4. Make copies of both the Client ID and Client Secret.

**Important:** You will not be able to view the Client Secret again after this point. Ensure you have made a copy for future reference.

You will now need to make a POST request to Spotify's API through your preferred API client. We will use [Postman](https://www.postman.com/).

1. Configure a POST request to the Spotify token request endpoint:
`https://accounts.spotify.com/api/token`
2. Add a header entry as follows:
Key: `Content-Type`, Value: `application/x-www-form-urlencoded`
3. Add the following HTTP body, replacing the placeholder values with your own Client ID and Client Secret. If you are using Postman, you can use the body as Raw.
`grant_type=client_credentials&client_id=<your-client-id>&client_secret=<your-client-secret>`
4. Send your request.

A successful request should return the access token formatted as follows:

```
{
    "access_token": "BQCRUpmOZF5XvXGKNsdsTBAVc4NpL_7y8DSZTv_BG56rJvRfS5wYR9HFzKphgRqMCDnTnFn97KBmtqtPRrtL0ANVcezyjFsz0B6JAU1kOK3wFUA19EE",
    "token_type": "Bearer",
    "expires_in": 3600
}
```

**Note:** The token expires after one hour but this will be sufficient for our example. You can re-send the POST request to receive a new token as required. Make a copy of the access token, as we can now begin configuring the Connector module.

## Compose the Endpoint

We are going to use the [Get Artist's Top Tracks](https://developer.spotify.com/documentation/web-api/reference/get-an-artists-top-tracks) endpoint. This is a relatively simple endpoint that will return the top tracks for a specified artist for a given geographic region. Refer to the linked document for full information regarding the endpoint and response data.

The endpoint URL is: `https://api.spotify.com/v1/artists/{id}/top-tracks`

As you can see, the endpoint first requires a single parameter: {id}. This is the **artist_id** of the artist you want to query, and is gathered as follows:

1. Locate your chosen artist in the Spotify client.
2. Click the three dots ... near the top of the artist's page, and click **Share -> Copy link to artist**.
3. Paste the copied link into a text editor, and you should see the following:
`https://open.spotify.com/artist/06HL4z0CvFAxyc27GXpf02?si=r_2RdlprRwSsQhSM63VKFw`
The artist ID is the string after *ht<span>tps://open.spotify.com/artist/* and before the question mark **?**. For example:
ht<span>tps://open.spotify.com/artist/**06HL4z0CvFAxyc27GXpf02**?si=r_2RdlprRwSsQhSM63VKFw
4. Copy the artist ID.

Additionally, you will need to specify a geographic region by using a **country code**. The country code is the two-digit [ISO 3166-1 alpha-2 country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) for the relevant country. For example, a country in the United Kingdom would use the code `GB`. We will detail how to add this parameter later on, but for now make a note of the country code you want to use.

We now have everything we need to compose the GET request for our connector: the access token for authentication, the endpoint URL, and the artist ID and country code required for that endpoint.

## Create a Connector Module

1. Select **Edit Mode** to access the dashboard **Toolbox**.
2. Drag-and-drop a **Connector** module from the toolbox onto the dashboard.
3. Click **Edit** on the module to access the configuration settings.
4. Complete the configuration as decribed in [Connector Module Configuration Guide](link) up until the point where you are required to configure the endpoint, as we will use the details from the earlier stages of this guide.

### Configure the request

1. If not already, set the request type to **GET** from the drop-down menu.
2. Paste the endpoint URL from earlier into the address field:
`https://api.spotify.com/v1/artists/{id}/top-tracks`
3. Within the **Authentication** tab, select **Bearer Token** from the **Authentication** Type drop-down menu.
4. Paste the access token you generated earlier into the Token text field. You can generate a new one if your original has expired.
5. Select the **Parameters** tab. Here you can see a parameter already in place for the {id} parameter in the endpoint. Paste your chosen artist ID into the **Value field**.
6. Now we need to add the country code. Click **Add a Parameter** to add a new parameter. We will define our query for the United Kingdom, so configure it as follows: Name: `market`, Value: `GB`.

At this point the Connector module is configured. We can test the connection by click Send to make your GET request to the `Get All Artist's Top Tracks` endpoint.

A successful result should return a large body of text, part of which is shown below. Now that we know our endpoint is configured correctly, we can now **Save** it and complete the process. The Connector module is now added to the dashboard with our API call configured and working correctly.

```
{
    "tracks": [
        {
            "album":
                {
                    "album_type": "album",
                    "artists":
                                [
                                    {
                                        "external_urls": {
                                                           "spotify": "https://open.spotify.com/artist/06HL4z0CvFAxyc27GXpf02"
                                                        },
                                        "href": "https://api.spotify.com/v1/artists/06HL4z0CvFAxyc27GXpf02",
                                        "id": "06HL4z0CvFAxyc27GXpf02",
                                        "name": "Taylor Swift",
                                        "type": "artist",
                                        "uri": "spotify:artist:06HL4z0CvFAxyc27GXpf02"
                                    }
                                ]
                }
        }
]
}
```

You can return to the Connector module at any point to add further endpoints and edit existing ones following the process above.