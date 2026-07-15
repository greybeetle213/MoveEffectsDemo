To set up, make a folder in UserData/MoveEffects and then put a file labeled move.json in it.
There are two types of tags, structure and player. 
In the moves.json file, make a list for each (assuming you want to use both structure and player tags):
{
	"structures": [],
	"players": []
}
structures - A list of structure tags. 
players - A list of player tags.
##Structure Tags: 
(all optional except "name")
name - The name of the tag. When being read, the name of the folder it is stored in is appended to the front. (ie. the tag "mount" in the folder "excalabur" would be changed to "excalabur/mount". You can refer to this as "mount" from other tags in excalabur, but from another folder you would have to type "excalabur/mount".
startConditions - Structure conditions which must be met for the tag to be applied, but not for it to stay applied.
conditions - Structure conditions which must be met for the tag to be applied, and to stay applied.
onAdded - Effects to be played when the tag is added
whileAdded - Effects to be played while the tag is added
onDestroyed - Effects to be played when the structure the tag is applied to is destroyed.
##Structure Conditions:
	combo - A combo in notation, only supporting modiefiers (eg. "SUK"). This is true if the sequence of moves done on the structures ends with the given combo. The structure's move history is cleared if no moves have been done on the structure for half a second.
	hasStates - A list of states. This is true if the structure has all of them. The possible states are: flicked, held, doubleHeld, parried, grounded, touchingPlayer, touchingStructure, mounted, exploded, spawning, onFloor, hitstop, ownerChanged (true if the last person to modify the structure just changed(
	hasTags - A list of tags. This is true if the structure has all of them
	speed - The magnitude of the speed the structure is going. This has the properties min, max, relative(explained later)
	verticalSpeed - The vertical speed of the structure
	horizontalSpeed - The magnitude of the horizontal speed of the structure
	position - The maginitude of the position of the structure (only useful with relative=true)
	verticalPosition - The vertical position of the structure
	horizontalPosition - The magnitude of the horizontal position of the structure
	height - The difference between the vertical position of the structure, and the height is was when it last touched the ground
	structureType - The type of the structure as in the game files: Wall, RockCube, Pillar, Disc, Ball
	not - A structure condition. This is true if the structure condition is not
	or - A list of structure conditions. This is true if any of them are.
	touchingStructures - A list of structure conditions. This is true if the structure is touching a structure fufilling each condition on the list. (Determined by seeing if there is a structure for the first condition, if there is removing it from the list of structures it is considering, then moving onto the next condition)
	touchingPlayer - Player condition. This is true if the structure is touching a player fufulling the conditions.
	flickedBy - player condition. This is true if the structure is flicked by a player fufilling the condition
	heldBy - player condition. This is true if the structure is held by a player fufilling the condition.

relative - For all conditions that are numbers (eg. position, speed, height) this can be set to true if the condition is inside another condition (eg. because of touchingStructures). If set to true, the number is relative to the property of the structure the condition it is inside belongs to.

## Effects:
playSound - The path to a .wav file. If there is no slash in the name this is calculated from the directory the move.json file is in. Otherwise it is from UserData/MoveEffects. If in whileAdded, the sound will be played on loop and stopped instantly when the tag is removed.
displayPrefab:
	assetBundle - Path to an asset bundle
	prefab - The prefab from the asset bundle to use
	scale - Change the scale of the object. Thi has properties x,y,z
	position
	rotation
	destroyTime - How long the prefab should be displayed for if it is in onAdded or onDestroyed, and how long it should stay around after the tag is removed if it is in whileAdded.


player tag:
	like structure tag but:
player conditions:
	like structure conditions but without touchingPlayer, flickedBy, heldBy and structureType, and with:
	flicking - list of structure conditions
	holding - list of structure conditions
onAdded and whileAdded do not support displaying prefabs with player tags yet