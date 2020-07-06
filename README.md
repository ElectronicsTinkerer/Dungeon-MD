# Dungeon-MD
A Dungeon-Markdown syntax system for text-adventure games

## World
The world is made up of Rooms in a 3d grid, like the way blocks are located in *Minecraft*.

---
## Rooms
Rooms are 10' x 10' x 10' chunks of the world.
Each room is separated into 5 sections as follows:

```
+--------------------+
|       NORTH        |
|--------------------|
|   |            |   |
| W |   CENTER   | E |
|   |            |   |
|--------------------|
|       SOUTH        |
+--------------------+
```
When the
