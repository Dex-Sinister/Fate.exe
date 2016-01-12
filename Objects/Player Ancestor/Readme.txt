The Player Ancestor is the most variable part of Fate.exe. It's the object most likely to change between different games, or even across a game's life cycle.

Attributes on the Player Ancestor determine obvious details like number of skill points, amount of refresh, and skill cap. They also determine many of the 'dials' that differ one Fate game from another, such as number of default stress boxes, how many stunts you get per point of refresh, and whether your skills need to obey the column rules.

Throughout this document, I'll use the default Fate Core setup as examples to illustrate what each attribute does.

@@
@@ Aspects
@@

@@ Aspects are stored in one attribute per player: the _aspects attribute. Each aspect has a name and a note. The format is 'name1`note1|name2`note2...|nameN`noteN'.

@@ By default, a Fate Core character can have up to 5 aspects: The High Concept, Trouble, and three others.
@@ This is a dial, and can be changed. The _aspects`data`max attribute on each player (and the Player Parent) is an integer determining the maximum number of aspects.

&_aspects`data`max Player Parent=5

@@ Some aspects may be special. In FAE and Fate Core, the first aspect is the High Concept and the second is the Trouble. Other Fate-based games have different terminology. The attribute _aspects`data`names stores special names for numbered aspects. The format is '<number1>.<name1>|<number2>.<name2>...|<numberN>.<nameN>'. If an aspect number is not mentioned in this attribute, it won't be given a special name.

&_aspects`data`names Player Parent=1`High Concept|2`Trouble|3`Other Aspects


@@
@@ Skills
@@

@@ Approaches are equivalent to other Fate games' skills. For the sake of portability, code and documentation will refer to approaches as skills.

@@ Each player (and the player parent) stores a _skills`data`list attribute. This attribute is a |-separated list of the skills in use on a particular game. The | is used in case of skills with spaces in the names. To change the skill list, change this attribute.

&_skills`data`list Player=Careful|Clever|Flashy|Forceful|Quick|Sneaky

@@ Skills are stored in the _skills`skills attribute, which has the format '<skill1 name>`<skill1 rating>|<skilll2 name>`<skill2 rating>...|<skillN name>`<skillN rating>', and is set by chargen commands.

@@ Many Fate games place a cap on the bonus a skill can achieve. This is stored in the attribute _skills`data`cap, as an integer. If the number is <= 0, the player is treated as having an unlimited skill cap.

&_skills`data`cap Player=4

@@ In Fate.exe code, significant milestones are handled by the _skills`data`points attribute. A Fate Core character starts with 4 Average, 3 Fair, 2 Good, and 1 Great skill - the equivalent of 20 skill points. Skill points increase with significant+ milestones, and determine how many skills the player can have, and how high.

&_skills`data`points Player=20

@@ Some versions of Fate use a 'columns' system in their skills. You can only have as many skills at Great as you have at Good, and as many as you have at Fair, and so on. Whether a game obeys the column rules is determined by the boolean in the player ancestor's _skills`data`columns attribute.
@@ Fate Core does use columns, so it is set to 1.

&_skills`data`columns Player=1


@@
@@ Stress
@@

@@ N.B.: Any time an attribute name incorporates a stress track name, all spaces must be replaced with underscores.
@@ Second note: All active stress attributes (boxes, toughness, extra consequences) will be in _stress`tracks`<track>`<attribute> attributes. This will allow them to be wiped with _stress`tracks`**.
@@ Consequences will go in _stress`data`cons`<level> or in _stress`tracks`<track>`mild`#.

@@ Numerous attributes affect stress tracks: their length, how many there are, any bonus boxes, any bonus consequences, and so on.
@@ +stress commands outside chargen will, if not given <stress> input, assume the character's first stress track. (For FAE: the basic, single Stress track. For Fate Accelerated: The lone 'Stress' track. For Fate Core: Physical stress. Customised games may have different choices.)

@@ _stress`data`tracks: List of stress track names and their associated skills. Format is 'stress1`skill1|stress2`skill2...|stress3`skill3'. If a stress track has no associated skill, then the skill will always be assumed to be Mediocre (+0) when determining stress tracks.
&_stress`data`tracks Player=Physical`Physique|Mental`Will

@@ _stress`data`minimum stores the number of boxes you have before bonuses from skills, stunts, and so forth.
&_stress`data`minimum Player=2

@@ _stress`<track>`bonus stores the number of bonus boxes a character has for that stress track.
@@ _stress`<track>`override stores a FIXED number of boxes a character's base track will have, superseding all skills and bonuses.
@@ _stress`<track>`toughness stores a number of special bonus boxes placed at the end of the character's stress track. This is for compatibility with The Dresden Files RPG's Toughness powers, and games that may use similar.
@@ _stress`<track>`cons stores a number of extra mild consequence slots for a stress track.

@@ On the player object, _stress`data`cons lists the general-use consequences and their shift values. The format is <con1>`<shift1>|<con2>`<shift2>...|<conN>`<shiftN>.
&_stress`data`cons Player=Mild`2|Moderate`4|Severe`6|Extreme`8

@@
@@ Stunts
@@

@@ _refresh: Number of refresh points.
@@ _stunts`data`free: Number of free stunts. 
@@ _stunts`data`stunts-refresh: Stunts:refresh ratio.
&_refresh Player=3
&_stunts`data`free Player=3
&_stunts`data`stunts-refresh Player=1:1

@@ _stunts`stunts: The actual stunts taken. Format: codename~showname~cost~note~del|nextstunt.


@@
@@ Initiative
@@

@@ _init`data`conflicts: This is a |-separated list of conflicts, and the skills that work to establish initiative in those conflicts. The first skill determines basic turn order, while the rest are used for breaking ties. The format is <conflict1>`<skill1a>`<skill1b>...|<conflict2>`<skill2a>`<skill2b>...
@@ In Fate Core, physical initiative is determined with Notice (with ties broken by Athletics, then Physique), while mental initiative is determined by Empathy (with ties broken by Rapport, then Will).
&_init`data`conflicts Player Ancestor=Physical`Notice`Athletics`Physique|Mental`Empathy`Rapport`Will

@@ _init`data`roll: This is 0 or 1. It determines whether players use their flat skill rating (default) or roll the dice to determine initiative.
&_init`data`roll Player Ancestor=0

@@ _init`data`<conflict_name>`bonus: A numerical modifier for the basic skill rating used in that conflict.
@@ _init`data`<conflict_name>`speed: A number of 1 or above. Represents the Dresden Files RPG 'speed' powers, with 0 being no speed, 1 being Inhuman Speed, 2 being Supernatural Speed, and 3 being Mythic Speed. Determines the 'Supreme Initiative' and 'Super Supreme Initiative' that allow beings with those powers to always go first.
@@ These attributes do not need to be set on the Player Ancestor, but are changed on a per-player basis.
