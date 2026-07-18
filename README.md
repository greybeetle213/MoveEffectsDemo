## How to use
To set up, make a folder in UserData/MoveEffects and then put a file labeled move.json in it.
There are two types of tags, structure and player. 
In the moves.json file, make a list for each (assuming you want to use both structure and player tags):
```
{
	"structure": [],
	"player": []
}
```
**structure** - A list of structure tags. <br>
**player** - A list of player tags.<br>
## Structure Tags: 
(all optional except "name")<br>
**name** - The name of the tag. When being read, the name of the folder it is stored in is appended to the front. (ie. the tag "mount" in the folder "excalabur" would be changed to "excalabur/mount". You can refer to this as "mount" from other tags in excalabur, but from another folder you would have to type "excalabur/mount".<br>
**startConditions** - Structure conditions which must be met for the tag to be applied, but not for it to stay applied.<br>
**conditions** - Structure conditions which must be met for the tag to be applied, and to stay applied.<br>
**onAdded** - Effects to be played when the tag is added<br>
**whileAdded** - Effects to be played while the tag is added<br>
**onDestroyed** - Effects to be played when the structure the tag is applied to is destroyed.<br>
## Structure Conditions:
**combo** - A combo in notation, only supporting modiefiers (eg. "SUK"). This is true if the sequence of moves done on the structures ends with the given combo. The structure's move history is cleared if no moves have been done on the structure for half a second.<br>
**hasStates** - A list of states. This is true if the structure has all of them. The possible states are: **flicked, held, doubleHeld, parried, grounded, touchingPlayer, touchingStructure, mounted, exploded, spawning, onFloor, hitstop, ownerChanged** (true if the last person to modify the structure just changed)<br>
**hasTags** - A list of tags. This is true if the structure has all of them<br>
**speed** - The magnitude of the speed the structure is going. This has the properties min, max, relative(explained later)<br>
**verticalSpeed** - The vertical speed of the structure<br>
**horizontalSpeed** - The magnitude of the horizontal speed of the structure<br>
**position** - The maginitude of the position of the structure (only useful with relative=true)<br>
**verticalPosition** - The vertical position of the structure<br>
**horizontalPosition** - The magnitude of the horizontal position of the structure<br>
**height** - The difference between the vertical position of the structure, and the height is was when it last touched the ground<br>
**structureType** - The type of the structure as in the game files: Wall, RockCube, Pillar, Disc, Ball<br>
**not** - A structure condition. This is true if the structure condition is not<br>
**or** - A list of structure conditions. This is true if any of them are.<br>
**touchingStructures** - A list of structure conditions. This is true if the structure is touching a structure fufilling each condition on the list. (Determined by seeing if there is a structure for the first condition, if there is removing it from the list of structures it is considering, then moving onto the next condition)<br>
**touchingPlayer** - Player condition. This is true if the structure is touching a player fufulling the conditions.<br>
**flickedBy** - Player condition. This is true if the structure is flicked by a player fufilling the condition<br>
**heldBy** - Player condition. This is true if the structure is held by a player fufilling the condition.<br>
<br>
**relative** - For all conditions that are numbers (eg. position, speed, height) this can be set to true if the condition is inside another condition (eg. because of touchingStructures). If set to true, the number is relative to the property of the structure the condition it is inside belongs to.<br>

## Effects:
**playSound** - The path to a .wav file. If there is no slash in the name this is calculated from the directory the move.json file is in. Otherwise it is from UserData/MoveEffects. If in whileAdded, the sound will be played on loop and stopped instantly when the tag is removed.<br>
**displayText** - only works in whileAdded and is mostly there to be used as a placeholder<br>
### displayPrefab:<br>
**assetBundle** - Path to an asset bundle<br>
**prefab** - The prefab from the asset bundle to use<br>
**scale** - Change the scale of the object. This has properties x,y,z<br>
**position**<br>
**rotation**<br>
**destroyTime** - How long the prefab should be displayed for if it is in onAdded or onDestroyed, and how long it should stay around after the tag is removed if it is in whileAdded.<br>

<br>

## Player Tag:
Like structure tag but:
### Player Conditions:
Like structure conditions but without touchingPlayer, flickedBy, heldBy and structureType, and with:<br>
**flicking** - list of structure conditions<br>
**holding** - list of structure conditions<br>
the only player states are touchingStructure and onFloor<br>
onAdded and whileAdded do not support displaying prefabs with player tags yet<br>
