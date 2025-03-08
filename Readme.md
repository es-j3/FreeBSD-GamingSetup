### To start,
Hello! Thanks for visiting this readme. If you are currently on Linux or Windows, I'd recommend you do *NOT* switch to FreeBSD for the purpose of gaming, unless you have a lot of time on your hands. 

Currently, there are many different methods for gaming on FreeBSD. Including many platforms like Steam, GOG, Epic Games and more running great with several options available on FreeBSD. There are also many popular games like Minecraft that are even native on FreeBSD, with more performance than even Linux and Windows. 

This readme will mainly cover all of the known ways of getting many popular gaming launchers working on FreeBSD. Including but not limited to: Steam, GOG, Epic Games, Bare Proton.

### Steam
The most popular launcher that is covered here, I'd say. There are three popular options, and I will provide each of them, with their pros and cons.

#### Linuxulator Steam Utils
[The GitHub Page](https://github.com/shkhln/linuxulator-steam-utils)

```
pkg install linux-steam-utils
```
Pros: Very matured, great for running Linux Games

Cons: Proton support isn't the best, AMD and Intel performance is Limited

#### Mizutamari

[The Codeberg Page](https://codeberg.org/Alexander88207/Mizutamari)

```
pkg install Mizuma
```
Pros: Windows Game Support is good

Cons: March 2024 build of Steam, not sure how long that'll last

#### steam-bottler
> Expect some bias, because this is my project!

[The GitHub Page](https://github.com/es-j3/steam-bottler)

Pros: Good Windows game support, uses Proton

Cons: Random crashess

### GOG & Epic Games
Mizutamari, is in fact more than a Steam runner. It's also a "User-friendly Wine front-end primarily for FreeBSD." In other words, a general Wine Front-end. It also provides GOG installation options than Steam.

Installing GOG through Mizutamari should be simple enough.
```
Mizuma Install GOG-Galaxy
```
It seems that CEF seems to be troublesome again, specifically for Epic Games.
```
Mizuma Install Epic-Games
```
Install this through WINE, and then run it using Wine-Proton. You can change the Wine path in the Mizutamari configuration file.

### Did you know, you can run Wine-Proton standalone in FreeBSD? Here's how you can do that.
First, we must install and configure Wine-Proton, and Winetricks (For dxvk and fonts)
```
pkg install wine-proton winetricks && /usr/local/wine-proton/bin/pkg32.sh install wine-proton mesa-dri
```

Now, we can setup our Prefix for Proton.
```
WINEPREFIX=~/.wine-proton WINE=/usr/local/wine-proton/bin/wine winetricks dxvk corefonts
```

To run applications, we simply run:
```
WINEPREFIX=~/.wine-proton /usr/local/wine-proton/bin/wine /path/to/your/application.exe # --no-sandbox if it's electron/chromium
```

Proton doesn't make us application shortcuts by default, so we need to make one ourselves. Below is a simple example of a desktop shortcut
```
[Desktop Entry]
Comment=Launches steam-bottler configurator application
Exec=sh -c 'WINEPREFIX=~/.wine-proton /usr/local/wine-proton/bin/wine ~/.wine-proton/drive_c/Program\ Files/Some_application/run.exe
Icon=freebsd
Categories=Game;
Name=Cool Application
StartupNotify=false
Terminal=false
TerminalOptions=
Type=Application" > ~/.local/share/applications/App.desktop'
```

Hope this is useful.
