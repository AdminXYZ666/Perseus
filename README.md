# Perseus
Fancy name for a simple native library that patches Azur Lane scripts.  
Does not rely on offsets, so game updates shouldn't break it so long as no security measures are introduced.

Feel free to suggest new features.

## Loading the library
Add the following method to `UnityPlayerActivity`, anywhere above its `onCreate`:
```smali
.method private static native init(Landroid/content/Context;)V
.end method
```
And these lines to its `onCreate`:
```smali
	const-string v0, "Perseus"

	invoke-static {v0}, Ljava/lang/System;->loadLibrary(Ljava/lang/String;)V

	invoke-static {p0}, Lcom/unity3d/player/UnityPlayerActivity;->init(Landroid/content/Context;)V
```
(Preferably without replacing other variables, such as between `.locals 2` and `const/4 v0, 0x1`.)

## Config
Settings can be found inside `Perseus.ini`, located within the game's external files directory (`/sdcard/Android/data/{package-name}/files/`).  
If you're unsure of your region's package name, just look it up. All of them include "AzurLane" though.

An example with some values changed:
```ini
# [*] Delete the file to reset it. Restart the game to apply any changes.
# [*] Options can be one of the following types:
#      [1] Bool - e.g. "true" or "false" - Keys: All "Enabled"s, ExerciseGodmode, FastStageMovement, RemoveBuffs, RemoveEquipment and RemoveSkill.
#      [2] Whole numbers or false to disable changes - If you need an example you're five - Keys: All the ones not mentioned above.
# [*] "Enabled"s apply to the entirety of their section, if they're disabled everything will be.
# [*] If the game crashes, this file is most likely misconfigured.

original repo: github.com/Egoistically/Perseus.

[Aircraft]
Enabled=true
Accuracy=false
AccuracyGrowth=false
AttackPower=false
AttackPowerGrowth=false
CrashDamage=false
Hp=10
HpGrowth=false
Speed=1

[Enemies]
Enabled=true
AntiAir=false
AntiAirGrowth=false
AntiSubmarine=false
Armor=false
ArmorGrowth=false
Cannon=false
CannonGrowth=false
Evasion=false
EvasionGrowth=false
Hit=false
HitGrowth=false
Hp=false
HpGrowth=false
Luck=false
LuckGrowth=false
Reload=false
ReloadGrowth=false
RemoveBuffs=true
RemoveEquipment=true
RemoveSkill=false
Speed=false
SpeedGrowth=false
Torpedo=false
TorpedoGrowth=false

[Misc]
Enabled=true
ExerciseGodmode=false
FastStageMovement=true

[Skins]
Enabled=true

[Weapons]
Enabled=false
Damage=false
ReloadMax=false
```
Enabling the Skins mod gives you all skins in-game, as if you had bought them. They are persistent between restarts.

## Credits
* Library built upon [Android Hooking Patching Template](https://github.com/LGLTeam/Android-Hooking-Patching-Template).
* Most mods based on [Azur Lane Scripts Autopatcher](https://github.com/n0k0m3/Azur-Lane-Scripts-Autopatcher).