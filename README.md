# Dungeon-MD
A Dungeon-Markdown syntax system for text-adventure games

---
## Game Elements

### World
The world is made up of Rooms in a 3D grid, like the way blocks are located in *Minecraft*.
The grid is defined as being made up of Rooms.
Each Room has a location determined by its coordinate triplet: `X.Y.Z`. The spawn point in the world is always `0.0.0` which is at 'sea level' (represented by `Z = 0`). Anything below this point will be considered underground in the event that the Parser does not find an associated Room document while anything above is assumed to be air. (At `Z = 0` it is considered a 'field' that the player can simply wander in.)
When a Room document is present, however, it will override the default Room, allowing for the creation of a single part of the world without having to create a separate Room file for each coordinate location in the entire world.

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
## Game Tree (File Structure)
The game's data is stored in a file structure as follows:
```batch
game-root
├───creatures
├───npcs
├───objects
├───passages
├───player
└───rooms
```

The game-root can be any name, since the Parser will take it as an argument when it is run. The subfolders are less negotiable.
Contained within each of the subfolders (e.g. 'creatures') is a `.dmd` file specifying that particular element's data for the game's initial state.
- `creatures` is the folder for any animal types
- `npcs` is the folder for any NPCs
- `objects` is for things like apples, baskets, torches (i.e. any object)
- `passages` stores all the types of passages that can be used in a Room (e.g. a wooden_door)
- `player` stores the player's data (such as inventory, health, etc.) and any game state changes
- `rooms` stores the documents representing each of the Rooms in the World

---
## Game Parser
The game Parser is a program that is capable of reading the various `.dmd` files in the game's structure, interpreting them, generating the game's textual output, taking and processing user input, etc. (i.e. everything needed to run the game).

### Errors

Errors (unless fatal) should be handled in a way as to try to keep the game going if possible. For example, if an object is not found in the Game Tree but is being requested by a Room, then the Parser should continue running the game, ignoring the missing element and logging the event to the program's log file.
