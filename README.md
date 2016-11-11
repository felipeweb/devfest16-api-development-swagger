#DevFestSP '16
*Programando com Swagger e Go (API development with Swagger)*

In this sample was used as example an instagram api that comes within Swagger sample folder.
The following code written in Go was generated using [Mercurius](https://github.com/novatrixtech/mercurius)

# Go API Server for 

The first version of the Instagram API is an exciting step forward towards making it easier for users to have open access to their data. We created it so that you can surface the amazing content Instagram users share every second, in fun and innovative ways.  Build something great!  Once you've [registered your client](http://instagram.com/developer/register/) it's easy to start requesting data from Instagram.  All endpoints are only accessible via https and are located at `api.instagram.com`. For instance: you can grab the most popular photos at the moment by accessing the following URL with your client ID (replace CLIENT-ID with your own): ```   https://api.instagram.com/v1/media/popular?client_id=CLIENT-ID ``` You're best off using an access_token for the authenticated user for each endpoint, though many endpoints don't require it. In some cases an access_token will give you more access to information, and in all cases, it means that you are operating under a per-access_token limit vs. the same limit for your single client_id.   ## Limits Be nice. If you're sending too many requests too quickly, we'll send back a `503` error code (server unavailable). You are limited to 5000 requests per hour per `access_token` or `client_id` overall. Practically, this means you should (when possible) authenticate users so that limits are well outside the reach of a given user.  ## Deleting Objects We do our best to have all our URLs be [RESTful](http://en.wikipedia.org/wiki/Representational_state_transfer). Every endpoint (URL) may support one of four different http verbs. GET requests fetch information about an object, POST requests create objects, PUT requests update objects, and finally DELETE requests will delete objects.  Since many old browsers don't support PUT or DELETE, we've made it easy to fake PUTs and DELETEs. All you have to do is do a POST with _method=PUT or _method=DELETE as a parameter and we will treat it as if you used PUT or DELETE respectively.  ## Structure  ### The Envelope Every response is contained by an envelope. That is, each response has a predictable set of keys with which you can expect to interact: ```json {     \"meta\": {         \"code\": 200     },     \"data\": {         ...     },     \"pagination\": {         \"next_url\": \"...\",         \"next_max_id\": \"13872296\"     } } ```  #### META The meta key is used to communicate extra information about the response to the developer. If all goes well, you'll only ever see a code key with value 200. However, sometimes things go wrong, and in that case you might see a response like: ```json {     \"meta\": {         \"error_type\": \"OAuthException\",         \"code\": 400,         \"error_message\": \"...\"     } } ```  #### DATA The data key is the meat of the response. It may be a list or dictionary, but either way this is where you'll find the data you requested. #### PAGINATION Sometimes you just can't get enough. For this reason, we've provided a convenient way to access more data in any request for sequential data. Simply call the url in the next_url parameter and we'll respond with the next set of data. ```json {     ...     \"pagination\": {         \"next_url\": \"https://api.instagram.com/v1/tags/puppy/media/recent?access_token=fb2e77d.47a0479900504cb3ab4a1f626d174d2d&max_id=13872296\",         \"next_max_id\": \"13872296\"     } } ``` On views where pagination is present, we also support the \"count\" parameter. Simply set this to the number of items you'd like to receive. Note that the default values should be fine for most applications - but if you decide to increase this number there is a maximum value defined on each endpoint.  ### JSONP If you're writing an AJAX application, and you'd like to wrap our response with a callback, all you have to do is specify a callback parameter with any API call: ``` https://api.instagram.com/v1/tags/coffee/media/recent?access_token=fb2e77d.47a0479900504cb3ab4a1f626d174d2d&callback=callbackFunction ``` Would respond with: ```js callbackFunction({     ... }); ``` 

## Overview
This server was generated by the [swagger-codegen]
(https://github.com/swagger-api/swagger-codegen) project.  
By using the [OpenAPI-Spec](https://github.com/OAI/OpenAPI-Specification) from a remote server, you can easily generate a server stub.  
-

To see how to make this your own, look here:

[README](https://github.com/swagger-api/swagger-codegen/blob/master/README.md)

- API version: v1
- Build date: 2016-11-11T02:07:43.046-02:00


### Running the server
To run the server, follow these simple steps:

```
go run main.go
```

