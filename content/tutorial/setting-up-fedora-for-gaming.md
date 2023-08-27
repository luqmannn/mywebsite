---
title: Setting Up Fedora 37 for Gaming

date: 2023-02-26
type: page
categories:
    - DOOM
tags:
    - Eternal
    - Game
    - Fedora
---

### Install Steam
```{sh}
sudo dnf config-manager --set-enabled rpmfusion-nonfree-steam
sudo dnf install steam
```
- Open Steam > Settings > Steam Play > **Enable Steam Play** for all and supported titles.

### Install ProtonUp-Qt to use ProtonGE (custom version of Proton)
Proton is a tool for use with the Steam client which allows games which are exclusive to Windows to run on the Linux operating system. It is based on WINE, which is a cross compatability layer that allows Windows program to interface with Linux. The difference between ProtonGE and Valve's Proton is it provides many things that Valve's Proton does not including:
- Nvidia CUDA support for PhysX and NVAPI.
- Various upstream WINE patches backported.
- Various upstream WINE patches backported

You can read all of the details in [here](https://github.com/GloriousEggroll/proton-ge-custom)
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
Piper is a GTK+ application to configure gaming mice. It is merely a frontend, the list of supported devices depends on libratbag which you can check [here](https://github.com/libratbag/libratbag/tree/master/data/devices). The device-specific protocols usually have to be reverse-engineered and the features available may vary to the manufacturer's advertized features.
```{sh}
sudo dnf install piper
```

### Install GOverlay for performance monitoring
GOverlay is an opensource project that aims to create a Graphical UI to help manage Linux overlays. Basically if you want to benchmark and monitor all sort of stuff including FPS, temperature and utilization during gaming sessions.
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
