---
layout: default
---

# Headless Minecraft Client

## Preface
This is one of my biggest projects, with over 10,000 lines of code, 200+ classes (files) and well over 200 hours of work atleast. My personal use for this project was mostly to monitor worlds for fun and interesting statistics. These statistics would be gathered while scanning IPs for servers which is where the idea originally came from. All of the code was written by myself (except if otherwise mentioned)



This project emulates a Minecraft client connection to a Minecraft Serverin Java using the [Netty Networking Library](https://netty.io/). The Headless client connects to the Minecraft server over a TCP connection (usually on port 25565). The Minecraft Protocol is heavily detailed [here](https://wiki.vg/), this project could not have been without this. The Headless Client performs a secret key exchange with the server and can connect over an encrypted connection (using AES), additionally if packet compression is requested, the packets are inflated / deflated (using ZLib compression)

This project has been written from the ground up to be multi-threading compatible (ie. support multiple instances). The client is therefore capable of handling multiple concurrent instances from the same terminal. As mentioned above, the client was originally meant to simply connect to the server and collect some statistics. This was quite simple for a client, my 7950X3D could handle about 700 instances at the same time, the main limitation being blocking I/O (network connections as they each required an additional thread).

After a few weeks, my original goals of being able to connect where accomplished, originally I had no intentions of making it aware of it's surroundings (Entities, Blocks and Items)






[back](./)
