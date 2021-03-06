
# swJumpPad
Improved JumpPad/Kicker Actor that calculates jump force automatically.

Developed for the Unreal Tournament w00t Instagib community.
http://www.extremew00t.com/news.html

*  Does not require additional Trigger/LiftExit/LiftCenter actors.
*  Familiar placing procedure - just like Teleporters.
*  Path links visible in UnrealEd.
*  Bot support.
*  Can be disabled/enabled with Triggers.
*  Support for on-jump special effects.
*  Allows jump angle and destination randomisation.
*  Supports custom vertical gravity, ie: LowGrav mutator.
 
## One-way JumpPad Tutorial:
1. swJumpPads are placed like Teleporters:
1. TWO swJumpPad actors are required: Source and Destination.
1. In Source swJumpPad set "URL" to some name.
1. In Destination swJumpPad set "Tag" to that name.
1. Adjust JumpAngle if neccessary.
Congratulations, you have set up a one-way bot-friendly JumpPad.

## Tips:
* JumpAngle will be limited to 1-89 degrees.
* If the JumpAngle is too low, a theoretically valid one will be calculated ingame and warning message will be broadcasted every time someone jumps.
* For testing precision, doublejump into JumpPad from distance, this way you won't accidentially disrupt your jump with movement keys.
* Ignore other Teleporter properties other than URL, it's not a teleporter.
* If you want to change jump parameters, change them in the Source JumpPad, not the Destination one.
* bTraceGround requires that there are no holes under the center of Destination JumpPad. If there is one, ie if the JumpPad is placed on edge of a cliff, players will be launched at the ground level in the hole, ie bottom of the cliff. To fix this move Destination JumpPad away from the edge or disable bTraceGround.

### Angle random modes:

1. AM_Random   
Uses random value from range ( JumpAngle, JumpAngle+AngleRand )
 
1. AM_Extremes
Uses JumpAngle then JumpAngle+AngleRand then repeat. Lets suppose that two players walk into JumpPad one after another. Player who jumped  first may arrive at target location *later* than player who jumped  second if the jump angle of second player was significatly flatter.
    
1. AM_Owned        
Team==TeamNumber uses JumpAngle, other teams use JumpAngle+AngleRand

### bLogParams acronyms:

* A   = Angle
* IV  = Impact velocity in Z plane
* IS  = Impact velocity in XY plane
* IH  = Impact height
* T   = Time in ms
* P   = Peak height
* V   = Jump velocity
* G   = Gravity
* U   = URL
* PN  = Player Name
* N   = Source JumpPad name
* D   = Destination JumpPad name


#### Source JumpPad Properties
```
var(JumpPad) float          JumpAngle;          // Jump angle

var(JumpPad) byte           TeamNumber;         // Team number
var(JumpPad) bool           bTeamOnly;          // Other teams can't use it

var(JumpPad) float          TargetZOffset;      // Target location height offset
var(JumpPad) vector         TargetRand;         // Target location random range
var(JumpPad) bool           bTraceGround;       // Find ground below JumpPad and use it as target location

var(JumpPad) float          AngleRand;          // Jump angle random range
var(JumpPad) EAngleMode     AngleRandMode;      // Jump angle random range mode

var(JumpPad) bool           bDisabled;          // Disable, triggering JumpPad toggles this

var(JumpPadFX) class<Actor> JumpEffect;         // Spawn this actor at JumpPad when someone jumps
var(JumpPadFX) class<Actor> JumpPlayerEffect;   // Spawn this actor at jumping player
var(JumpPadFX) name         JumpEvent;          // Trigger this event when someone jumps
var(JumpPadFX) sound        JumpSound;          // Play this sound when someone jumps
var(JumpPadFX) bool         bClientSideEffects; // Spawn effects only on clients

var(JumpPadDebug) float     JumpWait;           // Disable JumpPad for JumpWait seconds after jump
var(JumpPadDebug) bool      bLogParams;         // Display jump parameters in log and ingame
```


