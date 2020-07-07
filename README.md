# Dungeon-MD
A Dungeon-Markdown syntax system for text-adventure games

## World
The world is made up of Rooms in a 3d grid, like the way blocks are located in *Minecraft*.
The grid is defined as being made up of Rooms.
---
## Rooms
Each room is defined in a separate file.
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

Every Room is stored in its own unique file. The files should have their position in the world in the filename using the format: `X.Y.Z.ANYTEXT.dmd` where 'X', 'Y', and 'Z' are the coordinates of the Room in the world and 'ANYTEXT' is any text that the creator of the Room may choose. It is recommended that 'ANYTEXT' is descriptive of the Room, i.e. the title of the Room.

## Objects
Objects are things that can be in Rooms. (E.g. tables, apples, )
