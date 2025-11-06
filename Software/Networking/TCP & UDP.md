---
date: 2024-09-28
tags: 
link: "[[Networking]]"
---

# TCP & UDP

> Internet traffic is composed of data transfers — lots of them — between servers and devices. That data is transferred via two protocols: TCP and UDP.


| **Factor**          | **TCP**                                                               | **UDP**                                                                 |
| ------------------- | --------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Connection type     | Requires an established connection before transmitting data           | No connection is needed to start and end a data transfer                |
| Data sequence       | Can sequence data (send in a specific order)                          | Cannot sequence or arrange data                                         |
| Data retransmission | Can retransmit data if packets fail to arrive                         | No data retransmitting. Lost data can’t be retrieved                    |
| Delivery            | Delivery is guaranteed                                                | Delivery is not guaranteed                                              |
| Check for errors    | Thorough error-checking guarantees data arrives in its intended state | Minimal error-checking covers the basics but may not prevent all errors |
| Broadcasting        | Not supported                                                         | Supported                                                               |
| Speed               | Slow, but complete data delivery                                      | Fast, but at risk of incomplete data delivery                           |

## 📃 Real time use case

- TCP will be used in application where the data need to send accurately
- UDP benefits applications that need to receive data quickly even if accuracy suffers. This is why real-time applications like audio and video streaming will often use UDP.


![[who_initiates_tcp_connection.png]]

## Does TCP use Checksum?

Yes — both TCP/IP and HTTP (indirectly) involve checksums, but in different ways:

### 🧩 1. TCP/IP

✅ Yes, both TCP and IP use checksums.

#### IP Layer (Internet Protocol):

The IPv4 header includes a header checksum to detect corruption in the header (not the payload).

IPv6 does not have a header checksum — it relies on lower and upper layers (like TCP/UDP or link layer) for integrity checking.

#### TCP Layer:

TCP includes a 16-bit checksum field that covers the entire TCP segment, including both the header and data, plus a pseudo-header derived from the IP layer (source/destination IP, protocol, length).

Purpose: Detect errors during transmission (bit flips, corruption).

If checksum fails, the receiver discards the packet, and TCP handles retransmission.

#### UDP:

Also uses a checksum, but it’s optional in IPv4 (mandatory in IPv6).
