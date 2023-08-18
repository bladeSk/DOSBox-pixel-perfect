## ℹ️ Notice

This repository has been archived, since more modern DOSBox forks with integer scaling exist now. Most notably [DOSBox-X](https://github.com/joncampbell123/dosbox-x) - not only does it support pixel-perfect rednering (via `output=openglpp`), there are also save states, GUI, Windows 98 support, 3fdx Voodoo 1 emulation, better OPL emulation [and more](https://dosbox-x.com/wiki/DOSBox%E2%80%90X%E2%80%99s-Feature-Highlights). I recommend using DOSBox-X as a more future-proof option, but this repository will be kept archived for anyone interested.

Original readme below.

---

# DOSBox - Pixel-perfect mod + vsync + savestates

<p align="center"><img src="https://cloud.githubusercontent.com/assets/4263742/23454383/521f32ae-fe6c-11e6-8be2-8f6471b24ed3.png" alt="DOSBox original vs pixel-perfect mod"/></p>

This is a modified version of DOSBox with focus on **super crisp visual output**. It uses integer scaling to produce homogenous pixels, supports VSYNC, plays nice with high-DPI displays and adds other enhancements like **savestates**.

## 💾 [Download](https://github.com/bladeSk/DOSBox-pixel-perfect/releases/download/r4019.3/dosbox-pixel-perfect-SVNr4019.3-win.zip)

Get the [latest Windows version](https://github.com/bladeSk/DOSBox-pixel-perfect/releases/download/r4019.3/dosbox-pixel-perfect-SVNr4019.3-win.zip) or check the _releases_ tab.

In case DOSBox doesn't run (`VCRUNTUME140.dll missing` error), you need to install the [Microsoft Visual C++ 2017 Runtime Library](https://go.microsoft.com/fwlink/?LinkId=746571).

## Features

### Pixel perfect mode (aka. integer scaling)

This mode makes the rendered image fill as much of your screen as possible while keeping it scaled to the nearest integer. GPU scaling is used instead of relying on software scalers.

The original DOSBox also renders a stretched image to a power-of-two texture, which is then stretched to the screen. This mod creates a texture with exact dimensions. This improves the image quality at the cost of breaking compatibility with very old video cards.

When `aspect=false`, square pixels are produced (1x1, 2x2, 3x3, etc.), which is what works best for most (but not all) games.

When `aspect=true`, the aspect ratio is approximated using rectangular pixels. For instance 320x200 on a 1920x1080 resolution will use 4x5 pixels. This yields a 4:3.125 aspect ratio instead of the intended 4:3, but the difference is only 4%.

### Borderless fullscreen window / VSYNC

A feature used by modern games that relies on the OS to provide VSYNC. This eliminates screen tearing.

### High-DPI support

This DOSBox fork is DPI-aware. When using 150% scaling, the image is no longer blurred.

### Savestates

Savestates allow you to save (`Alt+F5`) and load (`Alt+F9`) any game whenever you like. Note that this is an experimental feature and some games may crash. The credit for implementing this feature goes to ZenJu, tikalat, ykhwong, gandhig and bruenor41. I used the code found [here](https://www.vogons.org/viewtopic.php?f=32&t=53116) and tweaked it to compile with Visual Studio.

### Ready to use

A configuration file with sane defaults is provided. No need to fiddle around with settings, just run it and have fun. The folder `games` is automatically mounted.

The only thing you may want to adjust per-game is the speed of the emulator (`Ctrl+F11`/`Ctrl+F12`). Some games require very low speed (ie. Lemmings needs \~6000 cycles), some may require more speed.

## DOSBox config

You can just use the provided config, but if you have your own special `dosbox.conf`, make sure your values match the ones below to use the new features. Savestates work automatically, but you need to rebuild your mapper file, if you use one.

	[sdl]
	fullscreen=true
	fulldouble=true
	fullresolution=desktop
	output=openglnb # ⚠ important: pixel-perfect scaling only works with OpenGL!
	pixelperfect=true # set to false to make the image fill as much of the screen as possible
	borderless=true # prevents screen tearing; set to false to disable borderless fullscreen

	[render]
	aspect=false # change to true if circles in your game look like ellipses
	scaler=none


## Building

All the dependencies are included in the source code (under `lib`). You need to build them before you can build DOSBox. I used Visual Studio 2017, but older versions should be fine also. Build the projects in the following order:

* `lib\libpng-1.6.29\projects\vstudio\vstudio.sln` - use the "Release Library" configuration
* `lib\SDL-1.2.15\VisualC\SDL.sln`
* `lib\SDL_net-1.2.7\VisualC\SDL_net.sln` - requires MFC to be installed
* `visualc_net\dosbox.sln` - requires SDL.dll built in the previous step to be copied next to the .exe file
