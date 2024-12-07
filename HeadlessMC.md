---
layout: default
---

# Headless Minecraft Client

## Preface
This is one of my biggest projects, with over 10,000 lines of code, 200+ classes (files) and well over 200 hours of work atleast. My personal use for this project was mostly to monitor worlds for fun and interesting statistics. These statistics would be gathered while scanning IPs for servers which is where the idea originally came from. All of the code was written by myself (except if otherwise mentioned)

This project emulates a Minecraft client connection to a Minecraft Server in Java using the [Netty Networking Library](https://netty.io/). The Headless client connects to the Minecraft server over a TCP connection (usually on port 25565). The Minecraft Protocol is heavily detailed [here](https://wiki.vg/), this project could not have been without this. The Headless Client performs a secret key exchange with the server and can connect over an encrypted connection (using AES), additionally if packet compression is requested, the packets are inflated / deflated (using ZLib compression)

## Development



This project has been written from the ground up to be multi-threading compatible (ie. support multiple instances). The client is therefore capable of handling multiple concurrent instances from the same terminal. As mentioned above, the client was originally meant to simply connect to the server and collect some statistics. This was quite simple for a client, my 7950X3D could handle about 700 instances at the same time, the main limitation being blocking I/O (network connections as they each required an additional thread).

After a few weeks, my original goals of being able to connect to a server where accomplished, originally I had no intentions of making them aware of their surroundings (Entities, Blocks and Items) as these were not useful for collecting statistics; I decide to implement these functionalities to learn more about the protocol and TCP standards.

The main aspect which I aspired to add was pathfinding. Pathfinding seemed like a great way to expand my knowledge, I had written previous implementations of pathfinding algorithms (Dijkstra's) however I knew that it was horribly ineficient. I ended up implementing A* which is similar to Dijkstra's but uses heuristics to improve the search a lot. The specifics can be seen in the repository's README. This implementation worked but A* really wasn't meant for heavy infinite games like Minecraft, more so for maps and such. This implementation was too slow for running many parallel bots. With some extra research I found [Baritone](https://github.com/cabaletta/baritone), an open source Minecraft mod implementing pathfinding. I adapted it's pathfinding calculations (A modified A* algorithm), to work within my Headless environment and immediately the execution times were much quicker. With this, the client can handle many instances all pathing at the same time, and they can all work on automated tasks such as mining specific blocks. 

## Pathfinder Executor Code Example
```java
    private void findNextPath() {
        for (int i = 0; i < MAX_RETRY; i++) {
            instance.getLogger().logUser("Trying to find path!");
            Pathfinder pathfinder = new Pathfinder(instance.getPlayer().getBlockPos(), goal, new CalculationContext(instance.getWorld(), new BlockBreakTickCache(instance.getPlayer().getInventory())));
            currentPath = pathfinder.calculate();
            if (currentPath != null) {
                instance.getLogger().logUser("Next block at " + instance.getWorld().getBlock(currentPath.positions().getLast()));
                instance.getLogger().logUser("Found path! Going to " + currentPath.positions().getLast() + " type : " + instance.getWorld().getBlock(currentPath.positions().getLast()));

                break;
            }
            instance.getLogger().logUser("Failed to find path!");
        }
        //handle no path found
        if (currentPath == null) {
            isFinished = true;
            return;
        }
        positions = currentPath.positions();
        positionIndex = 0;
        if (currentPath instanceof Path) isLast = goal.isInGoal(currentPath.getDest());
        readyMove = true;
    }
```

## Post Completion

This project taught me many new concepts which I wasn't well-versed in before (TCP networking, pathfinding, encryption, compression, efficient communication over the internet), this was the goal of the project. If I were to redo this project once again, I would write it in C++, not only because of the better memory management (I am looking at you garbage collector), low level access and networking but mostly for the faster execution times. This would have been a much bigger endeavour but perhaps worth the performance benefit.



<style>
.button {
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

.repo {
 padding: 8px 25px;
 background-color: #008CBA;
} /* Blue */


.repo {
  background-color: white;
  color: black;
  border: 2px solid #008CBA;
}

.repo:hover {
  background-color: #008CBA;
  color: white;
}

.back {
  padding: 12px 100px;
  background-color: #aa0405;
} /* Red */

.back {
  background-color: white;
  color: black;
  border: 2px solid #aa0405;
}

.back:hover {
  background-color: #aa0405;
  color: white;
}
</style>

<a target="_blank" href="https://github.com/Hypericat/HeadlessMC"> <button class="button repo">Visit Repository</button></a>

<a href="./"> <button class="button back">Back</button></a>