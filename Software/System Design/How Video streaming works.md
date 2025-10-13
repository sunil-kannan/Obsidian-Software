---
date: 2024-10-07
tags: 
link: "[[System Design]]"
---

# How Video streaming works

> Have you ever wondered how video streaming works? Whether you're watching your favorite show on Netflix, streaming a live event on YouTube, or video chatting with friends, video streaming is a ubiquitous part of our digital lives.

## Types of Streaming

- There are two types of streaming.
- **On-Demand** - tv shows, and movies in Netflix
- **Live-video** - YouTube videos and live concert.

![[http & rmtp.png]]

### MPEG-Dynamic Adaptive Streaming over (DASH)

- **Moving Picture Experts Group (MPEG)** as an alternative to Apple's HTTP Live Streaming (HLS) protocol.
- MPEG-DASH is similar to HLS, another streaming protocol, in that it breaks videos down into smaller chunks and encodes those chunks at different quality levels. This makes it possible to stream videos at different quality levels, and to switch in the middle of a video from one quality level to another one.
- Dash Streaming is widely used by YouTube and Netflix.
- ##### How does MPEG-DASH work?
	- **Encoding and segmentation:** The origin server divides the video file into smaller segments a few seconds in length. The server also creates an index file – like a table of contents for the video segments. Then the segments are encoded, meaning formatted in a way that multiple devices can interpret. MPEG-DASH allows the use of any encoding standard.
	- **Delivery:** When users start watching the stream, the encoded video segments are pushed out to client devices over the Internet. In almost all cases, a **content delivery network** (CDN) helps distribute the stream more efficiently.
	- **Decoding and playback:** As a user's device receives the streamed data, it decodes the data and plays back the video. The video player automatically switches to a lower or higher quality picture in order to adjust to network conditions – for example, if the user currently has very little bandwidth, the video will play at a lower quality level that uses less bandwidth.

## Adaptive Bitrate Streaming (ABR)

**Adaptive bitrate streaming** is the ability to adjust video quality in the middle of a stream as network conditions change. Several streaming protocols, including MPEG-DASH, HLS, and HDS, allow for adaptive bitrate streaming.

Adaptive bitrate streaming is possible because the ==origin server encodes video segments at several different quality levels==. This happens during the encoding and segmentation processes. A video player can switch from one quality level to another one in the middle of the video without interrupting playback. This prevents the video from stopping altogether if network bandwidth is suddenly reduced.

![[bitrate.png]]


### MPEG-DASH vs HLS
\
- **Device support:** HLS is the only format supported by Apple devices. iPhones, MacBooks, and other Apple products cannot play video delivered over MPEG-DASH.
- **Standardization:** MPEG-DASH is an international standard. HLS was developed by Apple and has not been published as an international standard, even though it has wide support.
