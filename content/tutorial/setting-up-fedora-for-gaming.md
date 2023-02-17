---
title: Setting Up Fedora 37 for Gaming
type: page
description: How to setup Linux distribution as a gaming PC
topic: linux
---

### Install Steam
```{sh}
sudo dnf config-manager --set-enabled rpmfusion-nonfree-steam
sudo dnf install steam
```
- Open Steam > Settings > Steam Play > **Enable Steam Play** for all and supported titles.

### Install ProtonUp-Qt to use ProtonGE (custom version of Proton)
```{sh}
flatpak install flathub net.davidotek.pupgui2
```
- We use ProtonUp-Qt to install and manage Proton-GE for Steam and Wine-GE for Lutris
- Open ProtonUp-Qt > Add version > Compatability tool: **Proton-GE** > Version: **Latest** > Install

### Configure DOOM Eternal on Steam
- Download and install **DOOM Eternal** then add this parameter to  launch options to enjoy the game when you play it so many times. 
```
+com_skipIntroVideo 1 
+com_skipKeyPressOnLoadScreens 1 
+r_antialiasing 0 
+com_skipSignInManager 1
```

### Install Piper to configure gaming mice
```{sh}
sudo dnf install piper
```

### Install GOverlay for performance monitoring
```{sh}
sudo dnf install goverlay
```

### In game settings
**Gameplay** | **Toggle**
--- | ---
Glory Kill Highlight | On
Tutorials			 | Off
In-Game Tips		 | Clutter
Sentinel Armor		 | On
Empowered Demons	 | Off **(Required)**
Double Dash Input	 | Hold*
Photo Mode			 | Clutter

**Weapon** | **Toggle**
--- | ---
Auto-Switch Weapon Empty | Off
Auto-Switch Weapon New	 | Off
Classic Weapon Pose		 | Off*
Weapon Bob				 | Clutter

**Accessibility** | **Toggle**
--- | ---
Environmental Screen Shake | Off

**UI** | **Toggle**
--- | ---
UI Color Profile		| Preference
Menu Confirmation Time	| 0.1

**HUD** | **Toggle**
--- | ---
Hud Mode				| Full
Hud Scale				| Preference
Hud Opacity				| Preference
Crosshair Style			| Dot*
Presets					| Custom
Compass					| Clutter
Keycard Stock			| Clutter
Interaction Prompts		| On
Boss Health Bar			| On
Objective Markers		| Clutter
Demonic Corruption Meter| **On (Required)**
Blood Punch Gauge		| **On (Required)**
Active Runes			| Category Specific*
Dash					| **On (Required)**
Weapon Info				| **On (Required)**
Health/Armor Info		| **On (Required)**
Equipment Info			| **On (Required)**
Power Ups				| On
Extra Lives				| Off
Hud Opacity	z			| Preference
(Patch 5+) Reticle Ability Indicator	| Preference

**Notifications** | **Toggle**
--- | ---
Center Notifications	| Category Specific*
Side Notifications		| On*
In-Menu Notifications	| Off
Update Notifications	| Preference
Weapon Refill Numbers	| Preference
Health/Armor Pickups	| Preference
Doom Level Increase		| Clutter
Mission Challenges		| Category Specific*
Speakers				| Clutter
