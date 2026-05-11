---
date: "2026-05-11"
tags: 
link:
---

# SFU (Selective Forwarding Unit)

> An SFU is a real-time media server used in video conferencing systems like:

- Zoom
- Google Meet
- Microsoft Teams
- Discord
- Slack Huddles

The SFU acts like an intelligent packet router for audio/video streams.

Instead of every participant sending video directly to every other participant, each participant sends their stream to the SFU.

The SFU then forwards the stream to the required participants.


## Encoding Video is Expensive
Encoding video in server is expensive, so in SFU the client itself will send the data in a different format and based on the 
```
720p  -> High Quality
360p  -> Medium Quality
180p  -> Low Quality
```
for thousands of users:

CPU usage would become massive.
Latency would also increase significantly.
So modern systems push this work to the sender client.


# What SFU Actually Does

The SFU mainly:

- receives RTP packets
- tracks participant bandwidth
- tracks device capability
- chooses suitable stream
- forwards packets

It behaves more like:

```
smart packet router
```

than a video processor.

