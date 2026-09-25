# Default Weapons

A collection of 32 ready-to-use weapons (rifles, SMGs, pistols, shotguns, snipers, vintage guns, melee and a grenade) built with the meshes already included in the nanos world Default Asset Pack. No extra downloads needed.

Each weapon is fully configured with damage, recoil, sounds, animations, particles and magazine, and they all show up automatically in the [Sandbox](https://github.com/nanos-world/nanos-world-sandbox) Spawn Menu.

![AK47 with reddot](https://i.imgur.com/K8qK3OG.png)


## Available Weapons

| Category | Classes |
|---|---|
| Rifles | `AK47`, `AK74U`, `AR4` (AR-15), `GE36` (Gewehr 36), `GE3` (Gewehr 3), `AK5C`, `SA80`, `ASVal`, `DC15S` |
| SMGs | `AP5` (MP5), `SMG11` (MAC-10), `UMP45`, `P90` |
| Pistols | `Glock`, `DesertEagle`, `M1911`, `Makarov` |
| Shotguns | `Moss500`, `Ithaca37`, `Rem870`, `SPAS12` |
| Sniper Rifles | `AWP` |
| Vintage | `ColtPython`, `Lewis`, `Sten`, `BAR`, `StG44`, `M1Garand` |
| Melee | `Knife`, `Crowbar`, `BaseballBat` |
| Grenades | `G67` |


## Installation

Add it to the `packages_requirements` of your game-mode or package `Package.toml`:

```toml
packages_requirements = [
    "default-weapons",
]
```


## Usage

Every weapon is a global class that takes a location and a rotation (they are also available in the exported `NanosWorldWeapons` table):

```lua
-- Server side
local ak47 = AK47(Vector(0, 0, 100), Rotator())
```


## Examples

Give a weapon to a player's character:

```lua
local character = player:GetControlledCharacter()
local weapon = DesertEagle(Vector(), Rotator())
character:PickUp(weapon)
```

Attach a red dot sight and align it:

```lua
local my_ak47 = AK47(Vector(0, 0, 300), Rotator())

-- The AK47 mesh has no sight socket, so we offset the red dot manually
my_ak47:AddStaticMeshAttached("sight", "nanos-world::SM_T4_Sight", "", Vector(23, 0, 12))

-- Zoom a bit more when aiming down sights
my_ak47:SetSightFOVMultiplier(0.35)

-- Align the camera with the red dot center (each weapon needs its own offset)
my_ak47:SetSightTransform(Vector(0, 0, -2), Rotator(0, 0, 0))
```

![AK47 with reddot perfectly aligned](https://i.imgur.com/QeoHPBB.png)

Create your own variant by inheriting from any weapon:

```lua
GoldenDeagle = DesertEagle.Inherit("GoldenDeagle", {
	name = "Golden Deagle",
	category = "pistols",
})

function GoldenDeagle:Constructor(location, rotation)
	DesertEagle.Constructor(self, location, rotation)

	self:SetDamage(200)
	self:SetMaterialColorParameter("Tint", Color(1, 0.8, 0))
end
```
