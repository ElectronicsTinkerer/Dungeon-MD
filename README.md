# Dungeon-MD
A Dungeon-Markdown syntax system for text-adventure games

## World
The world is made up of Rooms in a 3d grid, like the way blocks are located in *Minecraft*.

---
## Rooms
Rooms are 10' x 10' x 10' chunks of the world.
Each room is separated into 5 Sections as follows:

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

Each of the side Sections of the Room are recommended to be about 2-3' wide (useful for drawing Rooms) and are used for placement of Objects and creatures/NPCs.
