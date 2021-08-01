# Documentation of the code.

I have tried to use expressive variable and function names to ensure that the code is easy to follow.

There are a number of things that you should consider if you wish to make changes which are covered here.  You'll also find some useful advice for changes you can make to extend the game.

## Combat

The function which gets the players combat option is `CombatGet`.  This gives the user 800ms to respond.  You can increase this to give the player more time to make a choice and decrease it to require faster reflexes.

You can add new ways of performing physical attacks by updating `PhysicalAttack` and more spells can be added in `CastSpell`.

If you want to change how monsters behave, then you can update `MonsterPsiAttack` and `MonsterPhysicalAttack`.

## Scenes

The variable `scenes` contains a stack of scene maps.  Each time the player enters a scenario (woods, swamp, or a building floor), the current scene map, player location, and a number of scenario flags are pushed onto this stack.  When the player exits a scenario, the previous scenario is popped from the stack so that the player finds themself in the same position as before.

If you ever add any flags or attributes that are dependent on the scenario, then you can ensure they are preserved correctly by adding them to the stack.  This is done in the `PushScene` and `PopScene` functions.

## Scenarios

Currently, there are two main scenarios: woods and swamps.  You can create new scenarios if you wish.  These are added to The Valley in `SetupValley` by specifying the character to use in the local `scenes` variable.

For each new scenario character, you will need to update `NewSceneFor` in order to specify how to create the appropriate map.

Standard scenarios can be created using `SceneMap`.  Buildings can be created using `CreateBuilding`.

## Buildings

You can create new building types easily enough.  There are variables (`inWoods`, `inLair`, `inTemple`, `inTower`) to determine which scenario the building is in and you can use this in `NewSceneFor` in order to determine the specific building to create.

You will need to update `SpecialFind` in order to determine the sorts of things that can be found.

If you decide to create a new type of building with multiple levels, then you will need to change `HandleStairs` accordingly.

## Character Options

The `playerTypes` variable contains the characteristics of each character the player can choose.  The "dolt" is what the player will be assigned if they don't select the appropriate option!  The numbers for each type are: psi gain and physical gain (determining how quickly the character recovers from combat), initial strength, initial psi, the maximum stamina, strength, and psi the character can reach.

If you add new character types, leave "dolt" as the last option and update `ReadType` accordingly.

## Monsters

The list of available monsters is given in the `monsterTypes` variables.  For each monster, the values are: monster name, type, physical and psi strength.  The actual initial monster physical and psi strength will be based on these values and are set in `SelectMonster`.

If you add more monsters, then leave the two lake monsters at the end of the list.  If you add lake monsters, then you will need to change the two `RANDINT` calls in `SelectMonster` accordingly.

## Graphics

The file `PETSCII.png` contains the character set exactly as it appeared on the Commodore PET.  If you wish to change the look of any of the characters used in scenes then you can update this file.  Note that each character is 8x8 pixels.  You will need to make significant changes to the display routines if you want to change this!
