# Dungeon-MD
A Dungeon-Markdown syntax system for text-adventure games (***Currently Work-In-Progress***)

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

Every Room is stored in its own unique file. The files should have their position in the world in the filename using the format: `X.Y.Z.ANYTEXT.dmd` where 'X', 'Y', and 'Z' are the coordinates of the Room in the world and 'ANYTEXT' is any text that the creator of the Room may choose. It is recommended that 'ANYTEXT' is descriptive of the Room, i.e. the title of the Room.

#### Sections
Each room is separated into 6 Sections. 5 of which are on the ground as follows:

```
+--------------------+
| \     NORTH      / |
|   +------------+   |
|   |            |   |
| W |   CENTER   | E |
|   |            |   |
|   +------------+   |
| /     SOUTH      \ |
+--------------------+
```
And the sixth is the ceiling.

The Center is 5' x 5' (in general, just to make object placement less ambiguous).

Each of the Sections of the Room are used for placement of Objects, Passages, and Creatures/NPCs (useful for drawing Rooms).

The notation for each section is as follows:
| Section | Filename | In File |
| :-----: | :------: | :-----: |
| North   | `n`      | `north`   |
| South   | `s`      | `south`   |
| East    | `e`      | `east`    |
| West    | `w`      | `west`    |
| Center  | `c`      | `center`  |
| Ceiling | `t`      | `ceiling` |

### Objects
Objects are things that can be in Rooms. (E.g. tables, apples, lanterns, etc.)
Each object has a weight, size, temperature, 'passibility', and description.    
An object's filename will be used for defining the name of the object when referenced in the game.

### Passages
Passage files take the format of `X1.Y1.Z1.S1-X2.Y2.Z2.S2.ANYTEXT.dmd`. Similar to rooms, the 'X', 'Y', and 'Z' parts of the filename are the locations of the passage. Passages have two important coordinates: the end and the end. Since passages cannot have forks, branches, etc., they are defined by their ends. Each coordinate uses an X.Y.Z.S order to denote each end of the passage. X, Y, and Z are the coordinates of the rooms that the passage connects to. The S in the coordinate is the Section of the end room that the passage exits into. The game parser will search the room for an object in the specified section that references the passage. The first one found will be used as the exit to the passage. If no referring object is found, the passage is to be indicated as "sealed" and unable to be exited through that end. In the event that an object is locked, the player must be able to unlock or otherwise remove the door from their path in order to exit the passage from the locked end.

---
## Game Tree (File Structure)
The game's data is stored in a file structure as follows:
```
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

## Style
Game files should follow the style presented in the files in each of the `example-game` directory. Some general guidelines are as follows:
* Filenames shall *never* contain spaces or special characters (e.g. `!@#$%^&*()=+<>,./;:'"[]{}\|`).
* All `.dmd` files shall have a maximum line length of 100 characters.
* All `.dmd` files shall have at least 1 empty line at the end of the file.
* Opening `{` brackets shall be on the same line as the element that they are describing.
