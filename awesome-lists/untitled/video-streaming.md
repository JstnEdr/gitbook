---
description: Advice and best practices around video streaming
---

# Video Streaming

From Modern Logic / Microsoft  
  
For 10 minute videos \(assuming they are 1080p or higher\) they definitely will want to have adaptive bitrate playback.  Progressive will not be performant.  
  
I'll start by saying that Mux might be a good choice if the customer has very low utilization, based on their pricing model.  It's hard to use Azure Media Services to do this for much less than $100 a month.  Bitmovin is popular but they start out at $5000 a year.  AWS also has similar services.  
  
Discussing the Azure scenario - there's two workflows you'd use.  You'll need an Azure subscription, and create a storage account and a Media Services account.   
  
First would be the encoding workflow - this is about content preparation. Read this page to get an idea of the workflow [Encoding video and audio with Media Services - Azure Media Services v3 \| Microsoft Docs](https://docs.microsoft.com/en-us/azure/media-services/latest/encoding-concept).    
  
You use [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases#:~:text=Azure%20Media%20Services%20Explorer%20is%20a%20test%20tool,v5%20for%20the%20AMS%20v3%20API%20%28recommended%20version%29.) or the portal web UI to run a test encode of one of the content items to see roughly what it takes to do so.  Since you are new to this use the [AdaptiveStreaming ](https://docs.microsoft.com/en-us/azure/media-services/latest/autogen-bitrate-ladder)preset which picks the bitrate ladder for you.  The output is put in an "output asset" which you can later use to get the URLs needed to stream.  
  
For playback, you'll need to enable a standard [Streaming Endpoint](https://docs.microsoft.com/en-us/azure/media-services/latest/streaming-endpoint-concept).  They cost about $2.50/day to run and you can think of this as the service that serves up your content.  You pay for bandwidth either at the data transfer rate or if you turn on CDN at the CDN rate.  Be sure to turn off the streaming endpoint   Note that this pricing works differently than the Mux pricing which is a per minute price.  I can walk you through how to estimate that if you get to that point.  
  
To play a video, you create a streaming locator, which is a policy object that controls what the player can do with your endpoint.  You use that to [create a streaming URL](https://docs.microsoft.com/en-us/azure/media-services/latest/create-streaming-locator-build-url) that is the input to the player.  The [AMP demo page](https://ampdemo.azureedge.net/) lets you paste the URL into a live player to try things out.  I haven't looked at players lately but ones I used to deal with outside of the Azure one are JW Player and video.js.  
  
Note that the streaming above is "open" in that it is easy for someone to use the debug console, grab the URL, and stream the content themselves.  There are two levels of content protection -- a lightweight AES-128 crypt system that provides basic protection but can be bypassed if you know how browsers work, and a more hardcore DRM solution that is platform-integrated and approved for movie distribution.  The latter comes with the hassles of a locked down solution.

