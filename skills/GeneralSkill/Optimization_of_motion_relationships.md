# Universal Video Story Relation Compiler Skill V2.2

# 0. Skill Purpose

This Skill is not responsible for directly writing the final video Prompt.

Its sole responsibility is to transform user-provided natural-language story ideas, plot summaries, shot descriptions, dialogue, action instructions, visual concepts, or fragmented notes into a video relation description that is:

* structurally clear
* temporally continuous
* spatially coherent
* causally executable
* state-trackable
* action-executable
* visually continuous
* relation-consistent
* persistently identifiable at the object level
* continuously trackable at the visual-state level

The overall pipeline is:

```text
User Natural-Language Story
→ Story Fact Extraction
→ Plot Relation Layer
→ Entity Map
→ Semantic Identity
→ Perceptual Identity
→ Visual Anchor
→ Initial State
→ Major Event Map
→ Temporal Relations
→ Causal Relations
→ Spatial Relations
→ Interaction Relations
→ Perception / Reveal Relations
→ Execution Relation Layer
→ Micro-Beat
→ Action Dependency
→ State Transition Contract
→ State Lock
→ Visual State Lock
→ Correspondence
→ Occupancy / Contact / Support
→ Physical / Visual Relations
→ Visual Anchor Sufficiency
→ Camera / Audio Relations
→ Continuity Validation
→ Relation Sheet
→ H3 Prompt Skill
→ H3 Prompt
```

This Skill does not aim to make the story more literary or to add large amounts of description.

Its goal is to:

> Reduce relation ambiguity, state jumps, missing causality, spatial conflicts, action compression, object drift, object rebinding, visual identity drift, and environment resets.

---

# 1. Core Architecture: Plot Layer and Execution Layer Must Remain Separate

The relation compilation performed by this Skill has two levels:

```text
PLOT RELATION LAYER
↓
EXECUTION RELATION LAYER
```

## 1.1 Plot Relation Layer

It answers:

> What happens in the story?

Its primary unit is:

```text
Major Event
```

For example:

```text
E1: Character sits down
E2: Character takes out a folding fan
E3: Character opens the fan
E4: Character displays the fan
```

The Plot Layer defines:

* event order
* story causality
* character relationships
* prop relationships
* spatial relationships
* event purpose
* key states
* dependencies between events

The Plot Layer represents global relations.

---

## 1.2 Execution Relation Layer

It answers:

> What necessary intermediate states and execution relations are required for a Major Event to happen reliably?

For example:

```text
E1: Sit down

Standing
→ begin lowering
→ weight shifts to seat
→ body contacts seat
→ seated
```

It may also include:

* Micro-Beat
* Body Mechanics
* Action Dependency
* Contact
* Support
* Correspondence
* Occupancy
* State Lock
* Visual State Lock
* Physical Preconditions
* Perceptual Identity Maintenance

The Execution Layer represents local relations.

---

## 1.3 Hierarchy Discipline

The most important rule is:

> Execution Relations may decompose a Plot Event, but they must not independently create, reorder, replace, or expand Plot Events.

For example, if the user says:

```text
The protagonist sits down, takes out a folding fan, opens it, but does not fan herself; she only displays the fan.
```

The Plot Layer is:

```text
E1 Sit down
E2 Take out the folding fan
E3 Open the fan
E4 Display the fan
```

The Execution Layer may decompose them as:

```text
E1
Standing
→ body lowers
→ weight shifts
→ body contacts the seat
→ seated and stable

E2
Hand approaches fan
→ contact
→ grasp
→ remove from its original position
→ fan enters held state

E3
Maintain stable grip
→ contact fan ribs
→ unfold
→ fan fully open

E4
Keep fan open
→ adjust display position
→ maintain display
```

But it must not automatically promote:

```text
Adjusting the skirt
Looking at the chair
Adjusting the hair
Smiling
```

to new story events.

Only do so when such actions are:

* explicitly requested by the user
* or unavoidable execution conditions required for the requested action to succeed

Even when something qualifies as Necessary Inference, it must remain in the Execution Layer and must not automatically become a new Major Event.

---

# 2. First Principle: Do Not Directly Rewrite the Story

If the user says:

```text
The character turns around and sees a creature.
```

do not immediately rewrite it as:

```text
The character turns around and sees a terrifying creature.
```

First parse it into:

```text
Entity:
Character / Creature

Initial State:
Character facing forward
Creature not directly visible

Major Event:
Character turns

Perception Relation:
Character's visual attention reaches Creature

Result State:
Character is facing the creature
```

Only after relation compilation is complete may the content enter the Prompt-generation stage.

Core principle:

> Story is not a Prompt. Story must pass through relation compilation first.

---

# 3. Second Principle: Story Does Not Equal All Facts

User-provided information falls into three categories.

## Explicit Fact

Facts explicitly stated by the user must be preserved.

## Necessary Inference

Information that must be inferred to make the action, space, or causal chain valid may be added.

## Optional Interpretation

Information that does not affect whether the story works and can reasonably be chosen by the model must not be arbitrarily fixed.

For example:

```text
A walks to the door and opens it.
```

You may infer:

```text
A must approach the door first.
A must establish an executable interaction with the door.
```

But do not add:

```text
A checks a phone first.
A adjusts clothing.
A looks at the doorknob.
```

unless those actions are explicitly requested or are unavoidable execution conditions.

---

# 4. Third Principle: Complete Execution Logic Without Creating Story Facts

It is permitted to fill in:

* intermediate states required to complete an action
* basic spatial relations
* action direction
* visual continuity
* the minimum conditions required by a physical event
* the order of state changes
* necessary body-motion relationships
* necessary contact relationships
* necessary support relationships
* the minimum visual continuity needed to preserve object identity

It is forbidden to invent without authorization:

* new characters
* new dialogue
* new plot events
* new motivations
* new props
* new worldbuilding
* new major visual reveals
* new character relationships
* new story purposes

---

# 5. Entity Map

First identify every video entity that affects the story, action, space, state, or visual result.

Entity types:

```text
PERSON
CREATURE
OBJECT
ENVIRONMENT
LOCATION
CAMERA
LIGHT
SOUND SOURCE
ABSTRACT FORCE
DERIVED PHENOMENON
UI
CROWD
VEHICLE
EFFECT
BODY PART
GARMENT
PROP
```

Entities are not created merely because they are nouns.

Create an Entity only when the entity genuinely affects one or more of:

* story
* action
* space
* state
* perception
* visual result
* object continuity

---

# 6. Entity Is Not the Same as a Visual Element

A “thing” in a story may be:

Actual entities:

```text
person
creature
gun
door
car
folding fan
shoe
cup
phone
```

Environmental entities:

```text
wall
floor
room
street
chair
table
entry area
```

Abstract entities:

```text
mind control
hallucination
abnormal gravity
```

Derived phenomena:

```text
shadow
reflection
mirror image
silhouette in smoke
screen image
```

Perceptual results:

```text
what the character sees
what the character hears
what the character notices as abnormal
```

Do not mechanically turn every noun into an independent Subject.

---

# 7. Semantic Identity

Every important entity that continues to participate in actions, spatial relations, or state changes may receive a Semantic Identity.

Semantic Identity answers:

> What is this entity in the story?

For example:

```text
Object A:
semantic identity = black Mary Jane shoe

Object B:
semantic identity = black Mary Jane shoe

Character:
semantic identity = protagonist
```

Semantic Identity primarily serves:

* story understanding
* relation compilation
* logical correspondence
* state management

But note:

> Semantic Identity is not a reliable visual tracking anchor for video.

This is especially true for two objects that are:

* visually identical
* similar in size
* the same color
* functionally identical
* close together

For example:

```text
Shoe A = semantic “one shoe”
Shoe B = semantic “another shoe”
```

That may be sufficient for human reasoning.

It may not be sufficient for a video model.

---

# 8. Perceptual Identity

Perceptual Identity is a core V2.2 module.

It answers:

> What observable evidence tells the model that this is still the same object in later frames?

Perceptual Identity does not prioritize abstract semantic labels.

Prioritize:

```text
color
shape
silhouette
material
local structure
distinctive accessory
visible orientation
relative position
relationship to other stable objects
```

For example, a Mary Jane shoe may be described as:

```text
Perceptual Identity:
black shoe
rounded toe
single instep strap
visible buckle
same toe shape
same upper silhouette
same initial orientation
```

For two cups:

```text
Cup A:
white body
small blue mark near rim
handle facing camera

Cup B:
white body
no blue mark
handle facing away
```

The purpose of Perceptual Identity is not literary detail.

It has one purpose:

> Establish observable, persistent recognition cues for an entity.

---

# 9. Semantic Identity ≠ Perceptual Identity

These must remain strictly separate:

```text
Semantic Identity
=
what it is
```

versus:

```text
Perceptual Identity
=
why the next frame should still identify it as the same thing
```

For example:

```text
Semantic:
SHOE_A = black Mary Jane shoe

Perceptual:
the same black Mary Jane shoe with the same visible buckle,
toe shape, and strap structure
```

When object continuity matters in the final Prompt:

> Prefer expressing Perceptual Identity.

Semantic Identity may remain as a relation-analysis label, but it must not carry visual tracking by itself.

---

# 10. Visual Anchor

A Visual Anchor is a stable, actually observable recognition feature that a video model can identify from the image.

Examples:

```text
distinctive silhouette
distinctive color block
distinctive clasp

distinctive pattern
obvious material difference
obvious local structure
stable relative position
spatial relationship to a stable environmental object
```

Visual Anchors should not primarily depend on:

```text
left
right
first
second
A
B
R
L
```

These are semantic labels, not stable visual anchors.

---

# 11. Visual Anchor Priority

When multiple continuous objects are easy to confuse, Visual Anchors take priority over directional semantics.

Prefer:

```text
same visible buckle
same toe shape
same red mark
same handle orientation
same distinctive pattern
same relative placement
```

Next:

```text
same semantic object
```

Only then use:

```text
left / right
front / back
first / second
```

These relationships can be auxiliary, but they should not independently carry Object Identity.

---

# 12. Visual Anchor Sufficiency

Visual Anchor Sufficiency is a V2.2 module.

It answers:

> Does the current object have enough observable cues for the video model to keep identifying it over time?

Use three levels:

```text
HIGH
MEDIUM
LOW
```

## HIGH

The object has an obvious visual distinction:

```text
two identical phones
but one has a large red sticker
```

## MEDIUM

The objects are not fully identical but remain distinguishable through factors such as:

```text
different orientation
different position
different neighboring environment
```

## LOW

Two objects have:

```text
almost identical appearance
similar size
nearby positions
complex background
```

For example, two completely identical black Mary Jane shoes:

```text
Visual Anchor Sufficiency = LOW
```

When sufficiency is low, consider:

* adding an establishing shot
* keeping the two objects at different initial orientations
* introducing stable local visual differences
* processing them in separate phases
* reducing the number of similar objects that are active simultaneously
* re-establishing a local anchor after a state transition

---

# 13. Perceptual Identity Maintenance

When the same object participates in multiple events, maintain:

```text
Perceptual Identity
+
Visual Anchor
+
Spatial State
+
Interaction State
```

Do not maintain only:

```text
Object Name
```

For example:

```text
Object A
→ on table
→ picked up
→ held by hand
→ moved toward cup
→ placed beside cup
```

At every phase, the relation analysis must be able to answer:

> Is this still the original Object A?

If the only continuity mechanism is:

```text
Object A
```

with no visual anchor:

> The relation compilation is insufficient.

---

# 14. Initial State

Every story segment must first answer:

> What is the state of the world immediately before the event begins?

For example:

```text
A stands near the door.
The door is closed.
Object A is on the table.
Object B is on the chair.
```

Initial State should include, when relevant:

```text
Semantic Identity
Perceptual Identity
Visual Anchor
Position
Posture
Possession
Contact
Support
Interaction
```

Only record states that are relevant to the story.

---

# 15. Plot Event

First split the user's story into Major Events.

A Major Event must represent:

> an event the user actually wants to happen in the story.

For example:

```text
E1: sit down
E2: take out the folding fan
E3: open the fan
E4: display the fan
```

A Major Event is a Plot-Layer node.

Do not use Micro-Beats as substitutes for Major Events.

---

# 16. Event Atom

An Event Atom is used to analyze observable actions inside an event.

For example:

```text
A runs over and picks up the weapon.
```

It may be decomposed into:

```text
A1: A begins running.
A2: A reaches the weapon.
A3: A stabilizes sufficiently to interact.
A4: A grasps the weapon.
A5: A lifts the weapon.
```

Event Atoms primarily serve relation analysis.

Not every Event Atom must appear in the final Prompt.

---

# 17. Strict Hierarchy Between Major Events and Micro-Beats

Major Event:

> The story event the user actually cares about.

Micro-Beat:

> An intermediate action or state that makes a Major Event continuous and executable.

For example:

```text
Major Event:
Character sits down

Micro-Beat:
Standing
→ begins lowering
→ weight shifts
→ body contacts seat
→ seated and stable
```

The rule is:

```text
Micro-Beat belongs to Major Event.
```

Never assume:

```text
Micro-Beat automatically becomes a new Major Event.
```

unless the user explicitly requests it.

---

# 18. Execution Depth

Action decomposition should not become infinitely deep.

Choose execution depth according to action complexity.

## LOW

Examples:

```text
walk over
turn the head
wave
sit and look ahead
```

Only:

```text
Initial State
→ Action
→ Result State
```

is usually needed.

## MEDIUM

Examples:

```text
open a door
pick up a cup
sit on a chair
pick up a phone
```

Use:

```text
Action Onset
→ Key Intermediate State
→ Interaction
→ Result State
```

## HIGH

Examples:

```text
put on a shoe
tie a shoelace
insert a magazine
put an earring on a character
transfer an object with both hands
remove an object from a vehicle
```

Typical risks include:

* body-part correspondence
* coordinated body motion
* contact relationships
* weight shifts
* multi-step dependencies
* prop continuity
* visual identity drift

At this level, it may be appropriate to establish:

```text
Action Dependency
State Transition
Semantic Correspondence
Perceptual Identity
Visual Anchor
Occupancy
Contact
Support
State Lock
Visual State Lock
Visual Anchor Sufficiency
```

Execution Depth is an internal analysis tool.

Do not automatically put every micro-action into the final Prompt simply because the execution depth is HIGH.

---

# 19. Action Chain

Any key action should use:

```text
Initial State
→ Action Onset
→ Continuous Change
→ Interaction / Reaction
→ Final State
```

For example:

```text
Facing forward
→ begins turning
→ head and torso rotate
→ gaze reaches rear area
→ fully facing backward
```

This prevents the model from generating only the start and end points of an action.

---

# 20. Action Actor

Every major action must explicitly identify:

```text
WHO performs the action
```

Do not write only:

```text
the weapon rises
```

without identifying what causes the movement.

Distinguish among:

```text
Character raises weapon
```

or:

```text
External force moves weapon
```

or:

```text
Weapon fires automatically
```

---

# 21. Action Target

For complex actions, also make the target explicit:

```text
Actor → Action → Target
```

For example:

```text
Character → reaches for → weapon
Character → opens → door
Creature → strikes → wall
```

This reduces incorrect binding to nearby objects.

---

# 22. Motion Source

Separate the sources of motion:

```text
Subject Motion
Object Motion
Environment Motion
Camera Motion
External Force
```

Do not misinterpret Camera Motion as Subject Motion.

---

# 23. Action Dependency

Establish execution dependencies between actions:

```text
Event A
→ ENABLES
→ Event B
```

For example:

```text
Foot enters shoe
→ ENABLES
→ heel placement

Heel placement
→ ENABLES
→ strap fastening
```

Action Dependency is not the same as Temporal Relation.

```text
A happens before B
```

does not automatically mean:

```text
A enables B
```

---

# 24. State Transition Contract

Each complex Major Event may have:

```text
Precondition State
→ Action Onset
→ Intermediate State
→ Completion Condition
→ Result State
```

For example:

```text
Precondition:
shoe is on floor

Action Onset:
hand reaches toward shoe

Intermediate:
hand grasps shoe
foot approaches shoe

Completion:
foot fully enters shoe
heel settles

Result:
shoe is worn
```

Rule:

> Any later event that depends on this event must begin from the previous event's Result State.

---

# 25. State Lock

The purpose of State Lock is:

> Prevent an already-established story state from being overwritten without a cause.

For example:

```text
Object A placed on table
```

may establish:

```text
STATE LOCK:
A.position
A.orientation
A.presence
```

unless a later explicit event changes it.

State Lock is not an absolute physical freeze.

It means:

> Later story content must not change this state without a reason.

---

# 26. Visual State Lock

Visual State Lock is a V2.2 module.

It differs from Semantic State Lock.

Semantic State Lock:

```text
Object A remains Object A.
```

Visual State Lock:

```text
The same visually identifiable Object A
remains visually continuous with the previously established object.
```

For example:

```text
Object A:
same visible buckle
same toe shape
same material
same local structure
```

If Object A has already been worn:

```text
Object A remains visibly attached to the same occupied body part
until an explicit release / removal event occurs.
```

Visual State Lock primarily prevents:

* object rebinding
* object side switching
* silent recreation of a completed object
* a completed object suddenly returning to its original position
* the same object being made to perform the same completed action again

---

# 27. Relationship Between Semantic State Lock and Visual State Lock

When both exist:

```text
Semantic State Lock
=
the story relation must remain valid
```

```text
Visual State Lock
=
the image must allow the model to keep recognizing the same state
```

If only Semantic State Lock is satisfied:

```text
right shoe remains right shoe
```

but visually:

```text
the shoe has been silently regenerated
```

then the relation execution remains insufficient.

Therefore:

> High-complexity object interactions should establish both Semantic State Lock and Visual State Lock.

---

# 28. Correspondence Relation

Use Correspondence to establish entities that must remain paired.

V2.1 divides Correspondence into:

```text
Semantic Correspondence
Perceptual Correspondence
```

## 28.1 Semantic Correspondence

Examples:

```text
left shoe ↔ left foot
right hand ↔ weapon
key ↔ lock
character ↔ assigned seat
```

It serves story logic and semantic structure.

## 28.2 Perceptual Correspondence

Examples:

```text
the same visibly identifiable shoe
→ remains attached to the same sock-covered foot
```

or:

```text
the same phone with the red sticker
→ remains in the same hand
```

Perceptual Correspondence serves visual continuity in video.

---

# 29. LEFT / RIGHT Degradation Rule

LEFT / RIGHT remain valid as ordinary anatomical or spatial descriptions.

For paired feet, paired shoes, and other symmetric body parts that require persistent correspondence:

> **LEFT / RIGHT must not be the primary identity-tracking method; use Foot A / Foot B or another independent Persistent Identity first.**

LEFT / RIGHT are semantic spatial relations, not reliable visual object identity anchors.

Therefore:

```text
left shoe ↔ left foot
```

may be used as an auxiliary relation.

But it must not independently carry:

```text
Object Identity
Object Persistence
Visual Tracking
```

For two similar objects, prioritize:

```text
same identifiable visual object
```

and use:

```text
left / right
```

only as supporting information.

---

# 30. Camera Mirroring / Viewpoint Independence

When the shot involves:

```text
mirroring
left-right flipping
moving the camera to the opposite side
viewpoint rotation
```

do not automatically interpret:

```text
semantic left/right
```

as:

```text
object identity changed
```

Likewise, a change in:

```text
screen-left / screen-right
```

does not mean the object has been reassigned.

Object identity must be determined from:

```text
Perceptual Identity
Visual Anchor
Spatial Continuity
Interaction Continuity
```

---

# 31. Occupancy / Attachment State

Establish occupancy relationships among body parts, objects, containers, and tools.

Examples:

```text
hand = holding object

foot = inside shoe

object = inside drawer

character = seated on chair
```

A basic state transition is:

```text
unoccupied
→ approach
→ contact
→ insertion / attachment
→ occupied
```

Occupancy / Attachment State helps prevent:

* object teleportation
* one hand simultaneously holding conflicting objects
* props disappearing without cause
* a worn object suddenly detaching
* the same object being rebound to another body part

---

# 32. Contact State

When a contact relationship determines whether a later action can occur, establish a Contact State.

Examples:

```text
foot ↔ ground
hand ↔ handle
hand ↔ shoe
body ↔ seat
key ↔ lock
weapon ↔ hand
```

Basic structure:

```text
No Contact
→ Approach
→ Contact
→ Sustained Contact
→ Release
```

A contact-dependent action may occur only after the required contact has been established.

---

# 33. Support / Weight-Bearing Relation

When a character's posture depends on support, establish the current Support State.

Examples:

```text
seated
→ supported by chair

standing
→ supported by both feet

leaning
→ supported by wall

climbing
→ supported by step
```

---

# 34. Physical Preconditions

Check the minimum conditions required before an action can be executed.

Examples:

```text
pick up object
→ object must be reachable

put on shoe
→ shoe must be accessible

open drawer
→ hand must reach drawer

stand
→ a valid support path must exist

sit
→ a stable seating surface must exist
```

Check only the minimum necessary conditions.

Do not turn relation compilation into a physics textbook.

---

# 35. Temporal Relation

Establish temporal relations for events:

```text
BEFORE
AFTER
DURING
OVERLAP
SIMULTANEOUS
CONTINUOUS
INTERRUPTED
REPEATED
```

Temporal order and causality must remain separate concepts.

---

# 36. Causal Relation

Use causal relations such as:

```text
CAUSES
ENABLES
TRIGGERS
PREVENTS
INTERRUPTS
RESULTS_IN
MAINTAINS
```

Do not infer:

```text
A causes B
```

merely because:

```text
A happens before B
```

---

# 37. State Transition Validation

Every dependent event must be checked as:

```text
State A
→ Event
→ State B
```

Then check the next event:

```text
State B
→ Event 2
```

Do not allow:

```text
State A
→ Event 1
→ unexpected State C
→ Event 2 requires State B
```

---

# 38. Spatial Graph

When spatial relations are needed, establish relations such as:

```text
LEFT
RIGHT
FRONT
BEHIND
ABOVE
BELOW
NEAR
FAR
INSIDE
OUTSIDE
BETWEEN
FACING
TOUCHING
BLOCKING
CONTAINING
```

Note:

> A Spatial Relation describes where something is; it does not automatically describe whether two observations refer to the same object.

---

# 39. Spatial Anchor

For complex scenes, first select stable Spatial Anchors such as:

```text
Wall
Floor
Door
Vehicle
Table
Room
Corridor
Building
Horizon
Camera
Chair
Bed
Desk
Step
```

Then locate other entities relative to the Anchor.

For example:

```text
Floor = spatial anchor
Chair = on floor
Character = beside chair
Shoe = beside chair
```

---

# 40. Local Spatial Anchor

When a shot only requires nearby environmental structure, use a Local Spatial Anchor.

For example:

```text
Desk
Chair
Notebook
Drawer
Character
```

Only these local relationships need to remain stable.

Do not force the entire building or environment into the shot.

---

# 41. Spatial Persistence

If the story continues in the same space, then unless the story explicitly changes it, preserve:

```text
spatial layout
relative positions
ground relationships
wall relationships
object relationships
Camera side
```

A shot change must not automatically rearrange the space.

---

# 42. Environmental Continuity

The environment itself is also a persistent state.

By default, preserve:

```text
Architecture
Ground
Walls
Furniture
Local Background
Lighting Context
Major Environmental Objects
Spatial Layout
```

unless there is an explicit:

```text
scene change
location change
time jump
major environmental event
```

---

# 43. Camera Reframing Does Not Equal Scene Reset

Changing the camera from:

```text
wide
→ medium
→ close-up
```

does not mean the world has been regenerated.

If there is no:

```text
cut to new location
scene transition
spatial relocation
```

then:

```text
environment remains persistent
object positions remain persistent
character-object relations remain persistent
support/contact states remain persistent
```

---

# 44. Perception Chain

When the story includes:

```text
sees
hears
notices
discovers
realizes
smells
feels
senses something abnormal
```

establish:

```text
External Event
→ Sensory Input
→ Perception
→ Interpretation
→ Reaction
```

---

# 45. Knowledge State

Separate:

```text
what objectively exists
```

from:

```text
what the character knows
```

They must not be conflated.

---

# 46. Reveal Logic

For any story structure of:

```text
hidden
→ hinted
→ discovered
→ revealed
```

make explicit:

```text
What is hidden?
What is visible?
What causes discovery?
What becomes visible?
What remains hidden?
```

---

# 47. Ambiguity Preservation

When the story intentionally keeps something unknown:

> Do not resolve or explain the unknown content on the user's behalf.

---

# 48. Reality Layer

Complex stories may use distinct reality layers:

```text
REAL
PERCEIVED
HALLUCINATED
RECORDED
REFLECTED
PROJECTED
DREAM
MEMORY
```

Do not collapse these into one layer.

---

# 49. Physical / Visual Relation

Enable this module when the visual result depends on physical or geometric relationships.

Examples:

```text
Shadow
Reflection
Water
Glass
Smoke
Fire
Cloth
Collision
Destruction
Weight
Gravity
Projectile
Lighting
```

Basic structure:

```text
Source
→ Mechanism
→ Result
```

---

# 50. Interaction Graph

Establish relationships between characters and objects, or between characters:

```text
LOOKS_AT
TOUCHES
HOLDS
PUSHES
PULLS
FOLLOWS
CHASES
AVOIDS
ATTACKS
SUPPORTS
BLOCKS
HANDS_TO
TAKES_FROM
RECEIVES
GIVES
RELEASES
GRASPS
INSERTS
REMOVES
WEARS
FASTENS
```

Complex interactions must explicitly identify both sides of the relation.

---

# 51. Multi-Character Logic

In multi-character scenes, distinguish:

```text
who acts
who reacts
who remains still
who is responsible for the next event
who observes whom
who holds the object
who interacts with whom
```

Do not assume every character is an active agent at the same time.

---

# 52. Possession Transfer

When the story includes:

```text
handing over
passing to someone
receiving
stealing
dropping
switching hands
```

the transfer of Possession must be explicit.

Basic structure:

```text
A holds object
→ A extends object
→ B reaches object
→ B grasps object
→ A releases object
→ B holds object
```

---

# 53. Prop Continuity

The following prop attributes are states:

```text
position
orientation
holder
open state
closed state
whether it exists
whether it has been set down
whether it has been picked up
```

V2.2 additionally requires checking:

```text
Perceptual Identity
Visual Anchor
Visual State Lock
```

Do not allow, without cause:

```text
appears
disappears
teleports
changes side
changes orientation
changes owner
```

In particular:

> After an object is picked up, moved, placed, worn, or transferred, it must still be recognizable as the same object established earlier.

---

# 54. Similar-Object Continuity

This is a V2.2 module.

When a scene contains two or more objects with:

```text
similar appearance
same function
similar size
same color
```

actively evaluate:

```text
Visual Anchor Sufficiency
```

If it is insufficient:

```text
increase observable object distinctiveness
or reduce the number of simultaneously active similar objects
or process them in separate phases
or re-establish a local Visual Anchor
```

For example, with two identical black shoes:

Do not use only:

```text
Shoe A
Shoe B
```

Instead establish:

```text
Shoe A:
same visible buckle orientation
same initial local position
same toe silhouette

Shoe B:
different initial local orientation
different local position
different visible surface cues
```

---

# 55. Object Rebinding Prevention

This is a V2.2 module.

Do not allow:

```text
Object A
→ event 1
→ becomes worn
→ event 2
→ is treated as Object B
```

unless the user explicitly describes:

```text
exchange
transfer
removal
replacement
```

When no explicit exchange event exists:

> An established Object Identity must not be rebound to another target.

---

# 56. Active Object Isolation

When multiple similar objects exist:

> Do not keep every similar object as an active interaction object in every shot.

For example, with two shoes:

```text
Phase 1:
active object = Shoe A
Shoe B = passive background object

Phase 2:
active object = Shoe B
Shoe A = completed worn state
```

This reduces the chance that the model rematches:

```text
Object A
```

with:

```text
Object B
```

---

# 57. State Lock Hierarchy

V2.1 divides State Lock into:

```text
Semantic State Lock
Visual State Lock
Physical State Lock
```

## Semantic State Lock

The story relation must remain valid.

## Visual State Lock

The object's identity and visible state must remain continuous in the image.

## Physical State Lock

The physical state must persist, including states such as:

```text
attached
inside
held
supported
worn
grounded
```

For complex object interactions, at minimum check:

```text
Semantic
+
Visual
+
Physical
```

---

# 58. Correspondence Priority

The priority of correspondence is:

```text
Perceptual Correspondence
>
Semantic Correspondence
>
LEFT / RIGHT Auxiliary Relation
```

This does not mean semantic relations are unimportant.

It means:

> When the goal is visual object continuity in video, observable identity is better suited to visual execution than abstract left/right labels.

---

# 58A. Paired Foot Identity Protocol

When the story involves:

* putting on shoes
* removing shoes
* changing shoes
* tying shoelaces
* fastening ankle straps
* putting on socks or hosiery
* removing socks or hosiery
* persistent foot-to-shoe correspondence
* two visually similar feet participating in the same action

enable:

```text
Foot A
Foot B
Shoe A
Shoe B
```

The core assumption of this protocol is:

> **A model cannot reliably use “left foot / right foot” as a stable visual identity.**

Therefore, for paired feet that require persistent tracking, wearing, or correspondence:

> **LEFT / RIGHT must not be the primary anchor for Foot Identity.**

Do not establish the primary video execution relation as:

```text
left foot → Shoe A
right foot → Shoe B
```

Instead establish:

```text
Foot A ↔ Shoe A
Foot B ↔ Shoe B
```

Where:

* Foot A and Foot B are two independent Persistent Entities.
* Shoe A and Shoe B are two independent Persistent Entities.
* A / B are tracking labels within the current video and do not represent anatomical left/right.
* Under mirroring, rotation, viewpoint changes, cuts, or occlusion, A / B must never be reinterpreted as the other foot.

---

## 58A.1 Establishing Foot A / Foot B

Foot A / Foot B must not exist as arbitrary numbers alone.

The Initial State must establish at least one observable visual or spatial anchor and the shoe correspondence at the same time.

Recommended structure:

```text
Foot A
→ initially paired with Shoe A
→ located in the established local starting position
→ covered by the same hosiery state
```

```text
Foot B
→ initially paired with Shoe B
→ occupies the other established foot position
→ covered by the same hosiery state
```

Once established:

> Later execution must prioritize the fixed Foot A / Foot B to Shoe A / Shoe B Correspondence instead of repeatedly identifying them as “the left foot” or “the right foot.”

---

## 58A.2 A / B Are Persistent Identities, Not Left/Right Substitutes

Strictly distinguish:

```text
LEFT / RIGHT
=
anatomical spatial description
```

from:

```text
Foot A / Foot B
=
persistent visual execution identity
```

For example:

```text
Foot A = the foot initially paired with Shoe A
Foot B = the other independently tracked foot
```

Even if:

* the camera moves to the opposite side
* the composition is mirrored
* the character rotates
* the feet cross
* the camera reframes
* one foot becomes temporarily occluded

still:

```text
Foot A remains Foot A
Foot B remains Foot B
```

Do not swap identity merely because the visual left/right relationship changes.

---

## 58A.3 Foot Identity Must Be Bound to Shoe Correspondence

For shoe-wearing actions, the strongest relation is not merely:

```text
Foot A
```

but:

```text
Foot A ↔ Shoe A
Foot B ↔ Shoe B
```

If Shoe A has already been established with Foot A as:

```text
OCCUPANCY:
Shoe A on Foot A
```

then, before an explicit shoe-removal event:

* Shoe A must not reappear as a separate unworn object.
* Shoe A must not move to Foot B.
* Foot A must not perform “enter Shoe A” a second time.
* Shoe B must not be misinterpreted as the shoe corresponding to Foot A.
* The completed state of Foot A must not reset because of a camera change.

---

## 58A.4 One Active Foot / One Active Shoe

For high-risk actions involving two similar feet and two similar shoes:

> **Default to the One Active Pair Policy.**

That is:

```text
ACTIVE:
Foot A + Shoe A
```

After completion:

```text
LOCKED:
Foot A + Shoe A
```

Then:

```text
ACTIVE:
Foot B + Shoe B
```

This reduces:

* the two shoes being swapped
* the same foot being used to put on both shoes
* a completed shoe reappearing on the floor
* one shoe becoming bound to two feet
* the two feet being incorrectly merged into one action target

---

## 58A.5 Action Dependency for Shoe-Wearing

Shoe-wearing should use:

```text
Initial Foot State
→ Shoe Contact
→ Foot Entry
→ Forefoot Seating
→ Heel Placement
→ Shoe Adjustment
→ Strap Interaction
→ Strap Fastening
→ Worn State
```

If an ankle strap exists, also make explicit:

```text
Shoe A
→ attached ankle strap
→ hand contact
→ strap lifted
→ strap guided around same ankle
→ fastening point engaged
→ strap lies flat
```

The identity of Foot / Shoe / Strap must remain stable throughout the entire chain.

Do not treat:

```text
Foot A enters Shoe A
→ generic finished shoe
```

as sufficient.

The continuation must preserve:

```text
same Foot A
+
same Shoe A
+
same visible shoe structure
+
same ankle strap
```

---

## 58A.6 Completed Foot State Lock

When:

```text
Shoe A is fully worn on Foot A
```

establish:

```text
Semantic State Lock:
Foot A ↔ Shoe A
```

and:

```text
Visual State Lock:
the same visibly identifiable Shoe A
remains attached to the same visibly tracked Foot A
```

If the next story phase begins processing Foot B:

```text
Foot A + Shoe A = completed and inactive
Foot B + Shoe B = active
```

Later Prompts should not describe Foot A as entering a shoe, searching for a shoe, or waiting for another shoe.

---

## 58A.7 Occlusion / Viewpoint / Mirror Rule

A foot may be obscured by:

* a hand
* a skirt or garment hem
* the shoe opening
* a temporary camera crop
* moving the camera to the opposite side
* body rotation

None of these automatically permits Foot Identity rebinding.

If Foot A was already:

```text
paired with Shoe A
```

before occlusion, then when it becomes visible again:

> It must continue to be interpreted as the same Foot A.

Under a mirrored composition:

```text
Foot A ≠ newly visible left-side foot
Foot B ≠ newly visible right-side foot
```

A / B identities do not change with screen-side placement.

---

## 58A.8 Final Prompt Translation Rule for Paired Feet

When translating the relation analysis into a final Prompt, for paired-foot shoe-wearing or shoe-correspondence actions:

Prefer:

```text
Foot A / Shoe A
Foot B / Shoe B
```

rather than:

```text
left foot / right foot
```

However, A / B must not be used in isolation.

Also provide:

* corresponding shoe
* established local position
* current action state
* previous completion state

For example:

```text
Foot A, the foot already paired with Shoe A, remains fully shod and inactive.
Foot B now becomes the only active foot for Shoe B.
```

This is more reliable for visual continuity than:

```text
left foot stays still while right foot puts on the shoe
```

---

# 58B. Hosiery / Sock Textile Layer Protocol

When the character wears:

* pantyhose
* thigh-high stockings
* socks
* dance tights
* ballet tights
* other foot-covering textile garments

the Relation Skill should treat hosiery as:

> **an independent, explicitly identifiable textile layer, not merely a body-surface color.**

Hosiery is not:

```text
painted skin
```

and not:

```text
body-colored shading
```

It is:

```text
Body / Foot
↓
Hosiery Textile Layer
↓
Shoe
```

This layer order must remain persistent.

---

## 58B.1 Minimum Textile Identity

Unless the user explicitly specifies another material, hosiery should have at least:

```text
real textile thickness
soft fabric surface
opaque material
subtle textile texture
slight natural folds
slight natural ease
soft light diffusion
```

The fabric should:

* communicate real textile thickness
* have a soft textile surface
* show slight natural folds
* have a small amount of natural ease
* show subtle compression at the shoe opening, instep, ankle, heel, and similar contact areas

It must not:

* become excessively loose
* develop exaggerated wrinkles
* become a heavy cotton sock unless specified
* destroy the intended hosiery shape merely to make the material texture obvious

The goal is:

> **Make the model clearly perceive that the foot is covered by hosiery, rather than perceiving the foot itself as having changed color to the hosiery color.**

---

## 58B.2 Opaque Does Not Mean Anatomically Skin-Tight

Even fully opaque hosiery must not become:

```text
white foot
black foot
colored foot
```

In other words:

> **Opaque ≠ skin-like tightness.**

Hosiery may follow the overall foot contour, but it must not individually reproduce:

* individual toes
* toe joints
* toenails
* skin folds
* individual toe separation
* highly anatomical foot-surface detail

Especially around the toes:

> **The hosiery must form one continuous, smooth, recognizable textile silhouette at the front of the foot.**

Allowed:

```text
soft compression
subtle fabric folds
gentle textile tension
```

Not allowed:

```text
five individual toe bumps
toe outlines
toenail shapes
skin-colored gaps
bare-foot anatomy rendered in hosiery color
```

---

## 58B.3 Toe Area Visual Rule

This is one of the most important visual rules for hosiery.

When toes are covered by hosiery, the correct state is:

```text
continuous hosiery-covered toe silhouette
```

The incorrect state is:

```text
individual toes visible through the hosiery
```

Other incorrect states include:

```text
white bare-foot appearance
black bare-foot appearance
skin-shaped colored foot
```

Therefore:

> **The toe area must appear as a continuous hosiery silhouette, not as a set of toe contours tinted with hosiery color.**

Hosiery may be:

```text
white
black
pink
beige
colored
```

but regardless of color:

> **Color alone must never carry Hosiery Identity.**

Establish the identity through:

```text
textile surface
fabric thickness
soft folds
continuous toe coverage
```

---

## 58B.4 Hosiery Perceptual Identity

For hosiery that remains visible across multiple moments, establish:

```text
Semantic Identity:
hosiery garment covering the foot
```

and also:

```text
Perceptual Identity:
same opaque textile layer
same material character
same color block
same continuous toe coverage
same ankle / foot coverage
```

When the shot changes:

* hosiery remains the same textile layer
* it must not suddenly become bare skin
* it must not suddenly become a different material
* it must not transform from textile into skin-colored surface
* it must not change from naturally eased fabric into extreme skin-tight “hosiery-colored skin”

---

## 58B.5 Hosiery and Shoe Contact

During shoe-wearing, the stable layer order is:

```text
Foot
↓
Hosiery
↓
Shoe
```

Therefore:

* the shoe visually contacts the hosiery
* bare skin should not visually pass through the hosiery and directly contact the shoe
* the shoe opening may naturally compress the hosiery
* hosiery may show slight natural compression around the opening, instep, and ankle
* the hosiery and shoe boundaries must remain distinguishable
* the shoe must not merge with hosiery into one continuous material
* the shoe must not swallow the hosiery and erase its material identity

For an open shoe opening:

> The visible foot inside the shoe must still appear covered by hosiery.

An open shoe opening must not automatically reveal bare toes.

---

## 58B.6 Hosiery State Lock

If the Initial State shows the character already wearing hosiery, default to:

```text
HOSIERY STATE LOCK:
the same hosiery remains on the same feet
until an explicit removal event occurs.
```

Without an explicit removal event:

* bare feet must not appear without cause
* one foot must not suddenly lose hosiery while the other remains covered
* hosiery must not become partially transparent
* toes must not suddenly become visible
* hosiery color must not change randomly
* hosiery must not suddenly acquire skin-like material properties

If the character initially wears white pantyhose:

> White is only a color attribute. The textile-layer identity, coverage relationship, and continuity are the core state.

---

## 58B.7 Hosiery Does Not Need Artificially Strong Texture

Hosiery Identity should not be created through excessive texture density.

Do not require:

```text
large visible weave pattern
heavy textile grain
exaggerated fabric wrinkles
```

Prioritize:

```text
clear material boundary
soft opaque surface
subtle fabric thickness
slight natural folds
continuous toe silhouette
```

The final goal is:

> **The model should be able to identify from the scene structure that this is a foot wearing hosiery, rather than a bare foot painted in the hosiery color.**

---

## 58B.8 Final Prompt Translation Rule for Hosiery

When translating into the final Prompt, prefer:

```text
an opaque textile hosiery layer covering the entire foot,
with a soft matte fabric surface, slight natural ease and subtle folds;
the toe area forms one continuous fabric-covered silhouette without visible individual toes, toenails, skin, or anatomical toe separation
```

rather than only:

```text
white tights
```

or:

```text
opaque tights
```

because:

> A color word or opacity word by itself is insufficient to establish Hosiery Perceptual Identity.

---

# 59. Body Mechanics

Human movement should be checked for:

```text
weight shift
foot-to-ground contact
arm trajectory
grasp relationship
shoulder movement
pelvic movement
torso movement
head movement
body support
```

Body Mechanics belongs to the Execution Layer.

---

# 60. Action Compression Control

Video models may compress:

```text
A → B → C → D
```

into:

```text
A → D
```

Therefore, critical intermediate states must be preserved.

For example:

```text
shoe on floor
→ hand reaches shoe
→ hand grasps shoe
→ shoe moves toward foot
→ sock-covered foot enters shoe
→ heel settles
→ strap fastens
→ worn state
```

rather than only:

```text
character puts on shoe
```

---

# 61. Action Observability

Relation analysis may be extremely complete.

The final Prompt should contain only:

```text
the relations the model actually needs to observe and execute
```

Therefore:

```text
Relation Analysis ≠ Final Prompt
```

---

# 62. Execution Relations Must Not Modify Plot Relations

If the Plot Layer has already established:

```text
E1 Sit down
E2 Take the fan
E3 Open the fan
E4 Display the fan
```

the Execution Layer may decompose those actions.

It must not independently create:

```text
E1.5 Adjust the skirt
E2.5 Look at the camera
E3.5 Smile
```

unless:

```text
explicitly requested by the user
```

or:

```text
Necessary Inference
```

Even then, Necessary Inference remains in the Execution Layer.

---

# 63. Plot Event Order Is Authoritative

If the user explicitly provides:

```text
A → B → C → D
```

the Execution Layer must not reorder it as:

```text
A → C → B → D
```

If the original story contains a conflict, report:

```text
TEMPORAL / CAUSAL CONFLICT
```

rather than silently rewriting the story.

---

# 64. Plot Event Purpose Is Authoritative

If the user says:

```text
Open the folding fan
Do not fan with it
Only display it
```

do not add:

```text
fan moves air
dress reacts to wind
hair moves from airflow
character waves the fan
```

---

# 65. Action Exclusion Constraint

When the user explicitly states:

```text
do not fan
do not drink
do not attack
do not leave
do not speak
```

these are not ordinary negative prompts.

They are:

```text
Action Exclusion Constraints
```

For example:

```text
Fan opens
→ fan remains displayed
→ no fanning action
```

Translate such instructions into behavioral and state constraints rather than merely stacking negative keywords.

---

# 66. Camera Relation

Camera is an independent entity.

At minimum distinguish:

```text
Camera Position
Camera Orientation
Camera Motion
Framing
Shot Size
Camera Side
```

---

# 67. Camera Continuity

If there is no explicit cut, then:

```text
Camera Side
```

should remain stable by default.

If the story requires:

```text
front → rear
```

there must be either:

```text
camera movement
```

or:

```text
explicit cut
```

---

# 68. Camera and Visual Anchor Relationship

When camera framing changes:

> Re-check whether the current Object Identity still has enough Visual Anchor information.

For example:

```text
wide shot:
two shoes are clearly distinguishable

close-up:
only one shoe is visible
```

At this point:

> Do not assume that the other shoe's visual identity remains automatically established.

When needed:

```text
re-establish a local visual anchor
```

or:

```text
reintroduce an establishing view
```

---

# 69. Local Spatial Anchor

When a shot only requires nearby environmental structure, a local Spatial Anchor may be used.

Examples:

```text
driver door
desk drawer
shoe area
bed edge
entry step
```

---

# 70. Audio Relation

Distinguish among:

```text
Diegetic Sound
Non-Diegetic Music
Dialogue
Ambient Sound
Object Sound
Environment Sound
Communication Sound
```

Sound events must maintain temporal relationships with the corresponding visual events.

---

# 71. Dialogue Relation

At minimum, dialogue should establish:

```text
Speaker
Target
Dialogue Content
Temporal Position
Scene Position
Voice Source
```

If the user has not provided dialogue:

> Do not invent dialogue.

---

# 72. Relationship Between Perception and Action

For example:

```text
hears a sound
→ turns around
```

should be represented as:

```text
External Sound
→ Sensory Input
→ Perception
→ Reaction
```

---

# 73. Continuity Check

The final analysis must check:

## Identity Continuity

Is character identity consistent?

## Semantic Object Continuity

Is the object still the same story object?

## Perceptual Identity Continuity

Does the object still have sufficient visual recognition cues?

## Visual State Continuity

Is the object's visible state continuous?

## Physical State Continuity

Is its physical state continuous?

## State Continuity

Does the result of the previous event become the starting point of the next event?

## Temporal Continuity

Does the event order remain valid?

## Causal Continuity

Do actions have the necessary causes and preconditions?

## Spatial Continuity

Do character, object, and environment positions remain consistent?

## Object Continuity

Do props suddenly appear, disappear, move, change hands, or change orientation without cause?

## Object Rebinding Continuity

Is an already-established object incorrectly reinterpreted as another object?

## Body Continuity

Do body parts undergo impossible jumps?

## Foot Pair Continuity

For scenes involving both feet, check:

```text
Foot A remains Foot A
Foot B remains Foot B
Foot A ↔ Shoe A
Foot B ↔ Shoe B
```

Check:

* whether A / B are swapped
* whether they are incorrectly reinterpreted as left/right identities
* whether a completed Foot A becomes active again
* whether Shoe A is rebound to Foot B
* whether both feet are incorrectly merged into one action target
* whether mirroring, rotation, occlusion, or viewpoint changes cause identity swaps

## Hosiery Continuity

If socks or pantyhose are present, check that:

```text
Body / Foot
↓
Hosiery Textile Layer
↓
Shoe
```

remains valid.

Check:

* whether hosiery remains an independent textile layer
* whether its recognizable material characteristics remain stable
* whether bare feet suddenly appear
* whether it suddenly becomes a “bare foot in hosiery color”
* whether visible toes, toe separation, or toenail contours appear
* whether the toe area retains a continuous hosiery silhouette
* whether the hosiery suddenly becomes excessively skin-tight
* whether the shoe visually merges with the hosiery into a single material

## Contact Continuity

Does established contact persist without cause being lost?

## Support Continuity

Does the support relationship remain valid when the character's posture changes?

## Correspondence Continuity

Do paired relationships remain stable?

## Environment Continuity

Does the environment suddenly reset when the camera changes?

## Camera Continuity

Are camera-position changes supported by an event?

## Audio Continuity

Does the sound belong to the correct source?

## Visual Anchor Sufficiency

Does every high-risk object have enough observable identity cues?

---

# 74. Similar-Object Audit

The final Continuity Check must additionally ask:

```text
Are there multiple similar Objects?
```

If:

```text
Object Count > 1
AND
Visual Similarity = HIGH
```

then check:

```text
Perceptual Identity
Visual Anchor
Spatial Anchor
Active Object
State Lock
Object Rebinding
```

Paired feet and shoes must also be treated as independent high-risk objects when both are simultaneously involved.

If any check is insufficient, report:

```text
VISUAL OBJECT IDENTITY RISK
```

---

# 75. Relation Conflict Priority

When different relations conflict, use this priority:

```text
Explicit User Fact
>
Plot Event Order
>
Required Causal Logic
>
Physical Logic
>
Perceptual Identity
>
Visual State Continuity
>
State Continuity
>
Spatial Continuity
>
Execution Logic
>
Semantic Left / Right Relation
>
Optional Interpretation
```

Note:

LEFT / RIGHT must not override explicit visual identity cues.

---

# 76. Necessary Inference Boundary

Necessary Inference may do only two things.

### A. Make an event executable

For example:

```text
pick up a cup
→ hand must contact the cup
```

### B. Preserve continuity

For example:

```text
character is already holding the cup
→ later scenes assume continued possession
```

Necessary Inference must not create:

* new plot
* new characters
* new dialogue
* new motivations
* new story significance

---

# 77. Minimum Relation Sheet Structure

After relation compilation, the result should contain at least:

```text
1. Story Facts
2. Entity Map
3. Semantic Identity
4. Perceptual Identity when needed
5. Visual Anchor when needed
6. Initial State
7. Major Event Map
8. Temporal Relations
9. Causal Relations
10. Spatial Relations
11. Interaction Relations
12. Perception / Reveal Relations
13. Execution Relations when needed
14. State Transition Map
15. Continuity Check
```

For high-complexity actions, also add:

```text
Action Dependency
Semantic Correspondence
Perceptual Correspondence
Occupancy
Contact
Support
Physical Preconditions
Semantic State Lock
Visual State Lock
Physical State Lock
Visual Anchor Sufficiency
Active Object Isolation
```

For paired-foot / paired-shoe scenes, also add:

```text
Foot A / Foot B Identity
Shoe A / Shoe B Correspondence
One Active Pair State
Completed Foot State Lock
Foot Pair Continuity
```

For sock / hosiery scenes, also add:

```text
Hosiery Textile Layer
Hosiery Perceptual Identity
Hosiery State Lock
Toe Area Visual State
Body / Foot → Hosiery → Shoe Layering
```

Do not force every module to be enabled merely for formality.

---

# 78. Module Activation Principles

For ordinary stories:

```text
Entity
State
Event
Temporal
Causal
Spatial
```

For complex interactions:

```text
+ Interaction
+ Execution
+ Correspondence
+ Occupancy
```

For complex human movement:

```text
+ Body Mechanics
+ Contact
+ Support
```

For paired feet / paired shoes:

```text
+ Paired Foot Identity
+ Foot A / Foot B Correspondence
+ Shoe A / Shoe B Correspondence
+ One Active Pair Policy
+ Foot State Lock
```

For multiple similar objects:

```text
+ Perceptual Identity
+ Visual Anchor
+ Visual State Lock
+ Similar-Object Audit
+ Active Object Isolation
```

For socks / hosiery:

```text
+ Hosiery Textile Layer
+ Hosiery Perceptual Identity
+ Hosiery State Lock
+ Textile / Body Separation
+ Continuous Toe Silhouette
```

For suspense or mystery:

```text
+ Perception
+ Knowledge
+ Reveal
+ Reality Layer
```

For special visual phenomena:

```text
+ Derived Phenomenon
+ Physical / Visual Relation
```

Do not mechanically activate every module merely for the sake of completeness.

---

# 79. High-Risk Object Detection

The following conditions should automatically increase Object Continuity risk:

```text
Two or more identical or highly similar objects
Multiple characters wearing identical or highly similar clothing
Both hands performing similar operations simultaneously
Symmetrical left/right objects
Both feet and both shoes participating in an action
Foot entering or leaving a shoe
Hosiery covering the foot during a close-up
Rapid shot changes
Extreme close-ups
Mirrored compositions
Similar-looking backgrounds
An object temporarily leaving the frame
An object becoming occluded
An object entering a body part or container
An object being removed from a body part or container
```

When these conditions occur:

> Prioritize Perceptual Identity + Visual Anchor rather than adding more abstract numbering.

For paired feet:

> Prioritize fixed Foot A / Foot B + Shoe A / Shoe B correspondence.

---

# 80. Continuity After an Object Leaves the Frame

If an object temporarily leaves the frame, do not assume:

```text
object still automatically identifiable
```

Determine whether continuity is sufficient from:

```text
last visible state
spatial continuity
next visible state
perceptual anchor
```

If it is insufficient:

> Re-establish a Local Visual Anchor or an explicit state handoff when the object appears again.

---

# 81. Continuity After Occlusion

When an object is completely occluded by a body, piece of furniture, hand, or another object, establish:

```text
last visible identity
→ occlusion
→ expected persistent state
→ reappearance
```

Unless the story contains:

```text
transfer
removal
replacement
```

the object's identity should remain unchanged by default.

For Foot A / Foot B:

> Occlusion affects visibility, not Persistent Identity.

For established Shoe A / Shoe B:

> Occlusion affects visibility but does not permit rebinding to the other foot.

---

# 82. Mirroring and Symmetric Objects

For structures such as:

```text
left shoe / right shoe
paired earrings
gloves for two hands
symmetrical tools or weapons
earpieces for two ears
```

the following principle applies:

> Mirror symmetry does not imply interchangeable visual identity.

Prioritize:

```text
Visual Anchor
+
Interaction History
+
Spatial Continuity
```

For paired body parts such as the feet, prioritize:

```text
Foot A / Foot B
+
Corresponding Shoe A / Shoe B
```

Do not rely only on:

```text
left / right
```

---

# 83. Rotation and Viewpoint Changes

When an object undergoes:

```text
rotation
camera orbit
perspective change
mirror
viewpoint change
```

do not conclude that its identity changed merely because its two-dimensional screen position changed.

As long as:

```text
Perceptual Identity
+
State Continuity
+
Physical Continuity
```

still hold:

> It remains the same object.

For Foot A / Foot B:

```text
rotation
mirror
camera orbit
viewpoint change
```

must not change A / B.

---

# 84. Similar Objects Must Not Automatically Share State

For example:

```text
Shoe A = worn
Shoe B = grounded
```

The two objects must not inherit each other's state merely because both are:

```text
black Mary Jane shoes
```

Do not automatically assign:

```text
worn
```

to:

```text
Shoe B
```

Every object must have an independent State.

---

# 85. One Event, One Active Object Policy

When a single action phase deals with only one highly similar object:

> Keep only one Active Object whenever practical.

For example:

```text
Phase 1:
Shoe A = ACTIVE
Shoe B = PASSIVE

Phase 2:
Shoe A = LOCKED WORN STATE
Shoe B = ACTIVE
```

This does not mean a shot may contain only one physical object.

It means:

> Within the same action phase, only one similar object should be the primary Interaction Target.

---

# 86. Prompt Translation Principle

Before passing the Relation Sheet to the H3 Prompt Skill, the following distinction applies.

Within the Relation Sheet:

```text
Semantic Identity
```

may remain as an analysis label.

However, the final Prompt should preferentially express:

```text
same visually identifiable object
same visible structure
same spatially anchored object
same previously established worn item
```

rather than heavily relying on:

```text
Object A
Object B
Left
Right
First
Second
```

especially when those labels cannot be directly verified from the image.

For paired-foot shoe-wearing scenes, prefer:

```text
Foot A
Foot B
Shoe A
Shoe B
```

while also binding:

```text
current state
corresponding shoe
local position
interaction history
```

Do not write only:

```text
Foot A
```

without explaining its relationships.

---

# 87. The Final Prompt Must Not Mechanically Copy the Relation Sheet

A Relation Sheet may contain:

```text
Shoe A
Shoe B
Semantic Correspondence
Perceptual Correspondence
Visual Anchor
State Lock
```

The final Prompt does not need to reproduce every analysis field verbatim.

The H3 Prompt Skill should choose the most effective expression according to:

```text
relation risk
execution complexity
Prompt length
H3 readability
```

---

# 88. Final Working Procedure

For any user-provided story, execute the following strictly:

```text
Step 1
Extract Explicit Facts

Step 2
Build Entity Map

Step 3
Establish Semantic Identity

Step 4
Determine whether Perceptual Identity is needed

Step 5
Establish Visual Anchor

Step 6
Establish Initial State

Step 7
Build the Plot Relation Layer

Step 8
Determine Major Events

Step 9
Build Temporal / Causal / Spatial / Interaction Relations

Step 10
Identify Major Events that require Execution Decomposition

Step 11
Build Execution Relations

Step 12
Only when necessary, establish:
Action Dependency
State Transition
Occupancy
Contact
Support
Correspondence
State Lock
Visual State Lock
Physical State Lock

Step 13
If paired feet / paired shoes are involved:
Establish Foot A / Foot B
Establish Shoe A / Shoe B
Establish fixed Correspondence
Enable One Active Pair Policy

Step 14
If socks / hosiery are involved:
Establish Hosiery Textile Layer
Establish Hosiery Perceptual Identity
Establish Hosiery State Lock
Check Body / Foot → Hosiery → Shoe

Step 15
Check Similar-Object Risk

Step 16
Check Visual Anchor Sufficiency

Step 17
Establish Active Object Isolation

Step 18
Check whether Plot Layer and Execution Layer remain within their boundaries

Step 19
Check Identity / Visual / State / Spatial / Object / Camera / Environment Continuity

Step 20
Check Foot Pair Continuity and Hosiery Continuity when applicable

Step 21
Form the Relation Sheet

Step 22
Pass the Relation Sheet to the H3 Prompt Skill to determine how the final H3 Prompt should express it
```

---

# 89. Final Hard Rules

The following rules must always hold:

```text
1. Plot Layer defines WHAT happens.

2. Execution Layer defines HOW that event can reliably happen.

3. Execution Layer is subordinate to Plot Layer.

4. Micro-Beat belongs to a Major Event.

5. Micro-Beat must not automatically become a new Major Event.

6. Execution decomposition must not create new plot facts.

7. A completed semantic state must persist until an explicit event changes it.

8. A completed visual state must persist until an explicit event changes it.

9. A completed physical state must persist until an explicit event changes it.

10. Semantic Identity does not guarantee visual identity tracking.

11. Perceptual Identity should be established for high-risk repeated objects.

12. Visual Anchor is preferred over abstract numbering for object continuity.

13. LEFT / RIGHT are semantic relations, not sufficient object identity anchors.

14. Correspondence must remain stable unless an explicit transfer or reassignment occurs.

15. Object possession must have explicit continuity.

16. Contact must exist before contact-dependent actions.

17. Support must exist for support-dependent posture changes.

18. Camera reframing does not reset the spatial world.

19. Subject movement does not imply environment disappearance.

20. Temporal order is not automatically causality.

21. Similar objects require independent state.

22. Similar objects should not all be Active Interaction Targets simultaneously.

23. An object must not be rebound to another target without an explicit reassignment event.

24. A visually completed object must not be silently recreated as a new object.

25. Occlusion does not automatically permit identity reassignment.

26. Mirror / rotation / viewpoint change does not automatically change object identity.

27. Necessary Inference may complete execution logic but may not expand the story.

28. Final Prompt may contain only the execution detail necessary for reliable generation.

29. Relation analysis can be more complete than the final Prompt.

30. Never replace user-authored plot logic with model-preferred choreography.

31. When ambiguity is intentional, preserve the ambiguity.

32. If a relation is not required for story, execution, continuity, or visual result, do not force it into the Relation Sheet.

33. For high-risk similar-object interaction, Visual Anchor Sufficiency must be checked.

34. Semantic State Lock and Visual State Lock are separate concepts.

35. A strong semantic relation cannot compensate for a weak visual anchor.

36. Object identity should be maintained through observable continuity, not labels alone.

37. For paired foot interactions, do not use LEFT / RIGHT as the primary foot identity; use Foot A / Foot B with fixed Shoe A / Shoe B correspondence.

38. Foot A / Foot B are persistent execution identities, not replacements for anatomical left/right labels; their identity must be anchored by observable state, local position, and shoe correspondence.

39. Once Foot A ↔ Shoe A and Foot B ↔ Shoe B are established, camera mirroring, viewpoint changes, rotation, crossing, or occlusion must not swap A / B identities.

40. For two similar shoes and two similar feet, prefer One Active Foot / One Active Shoe Policy to reduce object rebinding and repeated-action errors.

41. A completed Shoe A on Foot A remains attached and inactive until an explicit removal event; it must not be silently reset, recreated, or assigned to Foot B.

42. When hosiery is present, treat it as an independent perceptual textile layer between body / foot and shoe.

43. Hosiery must have observable textile identity: material thickness, soft fabric surface, subtle natural folds, slight natural ease, and non-skin-like light response.

44. Opaque hosiery must not become an anatomical skin-tight representation of the foot; the toe area must form a continuous textile-covered silhouette rather than individual toe contours.

45. Hosiery identity must not depend on color alone; white hosiery must not become a “white bare foot,” and black or colored hosiery must not become a “black or colored bare foot.”

46. Unless an explicit removal event occurs, hosiery coverage remains state-locked: no sudden bare skin, visible toes, toenails, toe separation, material change, or random color change.

47. During shoe-wearing, the perceptual layer order is Body / Foot → Hosiery → Shoe, and the shoe must not visually merge with or erase the hosiery layer.
```

---

# 90. Core Example: Putting on Two Identical Shoes

User input:

```text
She puts on one shoe first, then the other.
```

Incorrect relation compilation:

```text
Shoe_R → right foot
Shoe_L → left foot
```

This is insufficient on its own.

Correct:

```text
Entity:
Shoe A
Shoe B
Character
Foot A
Foot B
```

Semantic Identity:

```text
Shoe A:
black Mary Jane shoe

Shoe B:
black Mary Jane shoe
```

Perceptual Identity:

```text
Shoe A:
black rounded toe
single strap
visible buckle
initial orientation A
initial ground position A

Shoe B:
black rounded toe
single strap
visible buckle
initial orientation B
initial ground position B
```

Initial State:

```text
Shoe A = grounded
Shoe B = grounded

Foot A = sock-covered
Foot B = sock-covered
```

Phase 1:

```text
Shoe A = ACTIVE
Shoe B = PASSIVE
```

Action:

```text
hand approaches Shoe A
→ hand grasps Shoe A
→ sock-covered Foot A approaches
→ sock-covered Foot A enters Shoe A
→ heel settles
→ strap fastens
```

State:

```text
Shoe A:
worn
attached
VISUAL STATE LOCKED

Shoe B:
grounded
untouched
PASSIVE
```

Phase 2:

```text
Shoe A:
LOCKED WORN STATE
not active
not manipulated

Shoe B:
ACTIVE
```

Action:

```text
hand approaches remaining loose Shoe B
→ grasps Shoe B
→ sock-covered Foot B approaches
→ Foot B enters Shoe B
→ heel settles
→ strap fastens
```

Final:

```text
Shoe A = same previously worn object
Shoe B = same previously loose object
```

The core execution logic is not:

```text
right shoe → right foot
left shoe → left foot
```

It is:

```text
same visually identifiable Shoe A
→ worn state

remaining visually identifiable Shoe B
→ worn state
```

Left/right relations are only auxiliary explanations.

---

# 91. Core Example: Two Identical Postcards

User input:

```text
She picks up one of the postcards on the table.
```

If two identical postcards are on the table:

Incorrect:

```text
Card A
Card B
```

That is not sufficient.

Correct:

```text
Card A:
upper card in the visible stack
slightly rotated
small red corner mark

Card B:
lower card
different visible edge alignment
```

Then:

```text
Card A
→ touched
→ grasped
→ lifted
→ held
→ remains the same card
```

A later shot must not treat:

```text
Card B
```

as the card that has been picked up:

```text
Card A
```

---

# 92. Core Example: Two Identical Cups

```text
Cup A:
handle facing camera
small highlight on rim

Cup B:
handle turned away
position closer to plate
```

If A is taken away:

```text
Cup A
→ grasped
→ lifted
→ held
```

then:

```text
Cup B
→ remains grounded
```

until an explicit action changes B.

---

# 93. Boundary with the H3 Prompt Skill

This Skill is responsible for:

```text
what the story is
how events are related
why an action can occur
how states change
how space remains consistent
how objects maintain visual identity
how high-risk objects obtain Visual Anchors
what intermediate states execution requires
```

The H3 Prompt Skill is responsible for:

```text
how to convert the Relation Sheet into an H3-executable Prompt
```

Therefore:

```text
Relation Skill
≠
H3 Prompt Writer
```

This Skill should not independently decide:

* final English wording
* final shot copy
* final negative Prompt
* final H3 six-section structure
* final Prompt length
* final visual rhetoric
* final output protocol

---

# 94. Boundary with the Relation Audit Skill

Relation Skill:

> Builds the correct relations.

For paired-foot shoe-wearing and hosiery scenes, Relation Skill must first establish:

```text
Foot A ↔ Shoe A
Foot B ↔ Shoe B
Body / Foot → Hosiery → Shoe
```

Foot A / Foot B do not carry anatomical left/right meaning; hosiery has its own independent Visual / Perceptual Identity.

Auditor:

> Checks whether the final Prompt still preserves these relations.

For example:

```text
Relation Skill:
the same visually identifiable shoe must remain attached to the same sock-covered foot.
```

Auditor:

```text
Check whether the Prompt introduces:
same shoe → new foot
```

Another example:

```text
Relation Skill:
Shoe B remains on the floor while Shoe A is worn.
```

Auditor:

```text
Check whether the Prompt makes Shoe B disappear,
reappear, or exchange identity with Shoe A.
```

---

# 95. Boundary with the Output Formatting Skill

This Skill is not responsible for the final output protocol.

When an Output Formatting Skill is activated, it is responsible for fields and structures such as:

```text
HUMAN_SUMMARY
MACHINE_DATA
META
MEDIA_ASSIGNMENT
AUDIO
DIALOGUE
DIALOGUE_BY_SPEAKER
PROMPT
VALIDATION
FINAL ANCHOR
```

This Skill provides only the upstream relation-compilation result.

It must not override the Output Formatting Skill's protocol.

---

# 96. Final Goal

The final goal of this Skill is not:

> to break a simple action into as many actions as possible.

Nor is it:

> to force a semantic label onto every object.

It is:

> **Without changing the user's story, add only the relations that are genuinely necessary to make video generation stable, continuous, physically executable, and capable of consistently identifying the same visual object over time.**

Final principle:

```text
The story determines:
WHAT

Execution relations determine:
HOW

Perceptual identity determines:
WHICH VISUAL ENTITY CONTINUES

The Prompt determines:
HOW TO EXPRESS IT TO H3

The Auditor determines:
WHETHER THE FINAL PROMPT STILL SATISFIES IT
```

Final relation architecture:

```text
WHAT
↓
SEMANTIC ENTITY
↓
PERCEPTUAL ENTITY
↓
VISUAL ANCHOR
↓
PAIRED-BODY CORRESPONDENCE
↓
TEXTILE / MATERIAL LAYER
↓
SPATIAL / INTERACTION STATE
↓
EXECUTION
↓
STATE TRANSITION
↓
VISUAL STATE LOCK
↓
CONTINUITY VALIDATION
↓
H3 PROMPT
```

As long as these layers remain clearly separated, increasing story complexity and increasingly precise action decomposition should not easily produce identity drift merely because objects are similar, the scene is mirrored, the camera changes sides, or an object is temporarily occluded.
