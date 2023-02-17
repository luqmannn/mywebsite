---
title: Install DOOM Eternal Mods in Linux
type: page
description: Enhance your gaming experience
topic: doom
---

### Introduction

DOOM Eternal is a wonderful game to be played, but it comes with a few quirks that prevent it from being much enjoyable game especially when you played it at the highest difficulty (Ultra Nightmare) over and over. There is a way to change the game using modding tools which replace certain assets, changing the default value or simply adding new things like new game mode that does not available in the game.

First, you need to download [EternalModInjectorShell](https://github.com/leveste/EternalBasher/releases/tag/v6.66-rev2.9) zip or tar file and extract it. Go to **Steam** >> **Library**, find the game and right click on **Manage** >> **Browse local files**. Open the extracted zip file and you'll see there are 3 items:
- base folder (These are the patch manifest files that we'll copy and replace to the base folder of the game)
- Mods folder (All the fancy mods that you want in zip file)
- Injector shell script

Below are some of the mods I personally use:
- [No more intro in the base campaign (no more King Novik speech) and DLC (TAG1 and TAG2)](https://www.nexusmods.com/doometernal/mods/97?tab=files&file_id=4523)
- [No more camera sequences](https://www.nexusmods.com/doometernal/mods/97?tab=files&file_id=4526)
- [Custom UI colour pack](https://www.nexusmods.com/doometernal/mods/138?tab=files)
- [Quality of life fundamentals](https://www.nexusmods.com/doometernal/mods/752?tab=files&file_id=5488), contain many fixes including:
     - No campaign intro popup delay.
     - No escalation warnings for TAG2.
     - HUD low health de-crapifier.
- [Gameplay fundamentals](https://www.nexusmods.com/doometernal/mods/752?tab=files&file_id=5502), contain many gameplay affecting fixes including:
     - Better Marauders, no more of his BS where he will raise shield when hit by other demons projectiles.
     - Crucible restack all your resources.
     - Chainsaw savagery

Open base folder in injector diretory, copy everything inside and paste it into the base folder of DOOM Eternal that you find earlier from Steam by browse local files. Put every single mods zip file that you downloaded straight into Mods folder, copy the Mods folder into the same root directory of DOOM Eternal. Then, copy the injector shell script to the same root directory of the game. Open terminal and make the injector shell script executable using the command `chmod +x EternalModInjectorShell.sh`. To start the modding, run the script using the command `./ EternalModInjectorShell.sh`

### Manage all the mods

So at some point you polluted DOOM Eternal with so much mods until the game become [a big giant meme](https://www.youtube.com/watch?v=jqNN1bDlTcM) and you want to remove some or most of it. I present to you, EternalModManager. You can install it using the flatpak command below:

```{sh}
flatpak install flathub com.powerball253.eternalmodmanager
```

With this tool you can simply untick the box to remove certain mods, it will remove unwanted mods into separate DisabledMods folder. Then run mod injector to simply execute the process. Thank you to everyone in DOOM Modding community that made modding is possible in Linux and all modders that made really cool mods.

Check out other cool mods:
- [Keeps the blood, gibs, and kills much longer](https://www.nexusmods.com/doometernal/mods/1)
- [Simple reskin of the Gargoyle](https://www.nexusmods.com/doometernal/mods/354)
- [Custom PB scope](https://www.nexusmods.com/doometernal/mods/205)
- [Less bullshit waveblast](https://www.nexusmods.com/doometernal/mods/142)