# Dungeon-MD
A Dungeon-Markdown syntax system for text-adventure games

---
## Game Elements

### World
The world is made up of Rooms in a 3d grid, like the way blocks are located in *Minecraft*.
The grid is defined as being made up of Rooms.

### Rooms
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

Each of the side Sections of the Room are recommended to be about 2-3' wide (useful for drawing Rooms) and are used for placement of Objects, Passages, and creatures/NPCs.

Every Room is stored in its own unique file. The files should have their position in the world in the filename using the format: `X.Y.Z.ANYTEXT.dmd` where 'X', 'Y', and 'Z' are the coordinates of the Room in the world and 'ANYTEXT' is any text that the creator of the Room may choose. It is recommended that 'ANYTEXT' is descriptive of the Room, i.e. the title of the Room.

### Objects
Objects are things that can be in Rooms. (E.g. tables, apples, lanterns, etc.)
Each object has a weight, size, temperature, and description.


---
## File Structure
The game's data is stored in a file structure as follows:
```batch
game-root
├───creatures
├───npcs
├───objects                             ├───passages                                                                            └───rooms
```

The game-root can be any name, since the Parser will take it as an argument when it is run. The subfolders are less negotiable.
Contained within each of the subfolders (e.g. 'creatures') is a `.dmd` file specifying that particular element's data for the game's initial state.

---
## Game Parser
The game Parser is a program that is capable of reading the various `.dmd` files in the game's structure, interpreting them, generating the game's textual output, taking and processing user input, etc. (i.e. everything needed to run the game).
