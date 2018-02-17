# DOSBox - Pixel-perfect mod + vsync + savestates

<p align="center"><img src="https://cloud.githubusercontent.com/assets/4263742/23454383/521f32ae-fe6c-11e6-8be2-8f6471b24ed3.png" alt="DOSBox original vs pixel-perfect mod"/></p>

This is a modified version of DOSBox for pixel purists, who like their pixels perfectly square. It also fixes DOSBox's long standing issue with image tearing (VSYNC) and adds savestates!


## Download

Download the Windows version from the [releases tab](https://github.com/bladeSk/DOSBox-pixel-perfect/releases).

In case DOSBox doesn't run, you need to install the [Visual C++ 2017 Runtime Library](https://go.microsoft.com/fwlink/?LinkId=746571).


## Features

### Pixel perfect mode (aka. integer scaling)

This mode makes the rendered image fill as much of your screen as possible while keeping it scaled to the nearest integer. The original DOSBox also uses an aspect ratio "correction" to stretch the image as if you were using a 4:3 monitor, which is disabled and the pixels are always square (1x1, 2x2, 3x3, ...). These features eliminate any uneven pixels and make the resulting image super crisp.

There is another improvement to pixel crispness - the original DOSBox renders a stretched image to a power-of-two texture, which is then stretched to the screen. This mod creates a texture with exact dimensions. This improves the image quality at the cost of breaking compatibility with very old video cards.

### Borderless fullscreen window / VSYNC

A feature used by modern games that relies on the OS to provide VSYNC. This eliminates screen tearing.

### Savestates

Savestates allow you to save (`Alt+F5`) and load (`Alt+F9`) any game whenever you like. Note that this is an experimental feature and some games may crash. The credit for implementing this feature goes to ZenJu, tikalat, ykhwong, gandhig and bruenor41. I used the code found [here](https://www.vogons.org/viewtopic.php?f=32&t=53116) and tweaked it to compile with Visual Studio.

### Ready to use

This build comes with a configuration file with sane defaults. No need to fiddle around with settings, just run it and have fun. The folder `games` is automatically mounted.

## DOSBox config

You can just use the provided config, but if you have your own special `dosbox.conf`, make sure your values match the ones below to use the new features. Savestates work automatically, but you need to rebuild your mapper file, if you use one.

	[sdl]
	fullscreen=true
	fulldouble=true
	fullresolution=desktop
	output=openglnb # pixel-perfect scaling only works with OpenGL!
	pixelperfect=true # set to false to make the image fill as much of the screen as possible
    borderless=true # set to false to disable borderless fullscreen

	[render]
	aspect=true
	scaler=none


## Building

All the dependencies are included in the source code (under `lib`). You need to build them before you can build DOSBox. I used Visual Studio 2017, but older versions should be fine also. The projects you need to build are:

* `lib\libpng-1.6.29\projects\vstudio\vstudio.sln`
* `lib\SDL-1.2.15\VisualC\SDL.sln`
* `lib\SDL_net-1.2.7\VisualC\SDL_net.sln`
* `visualc_net\dosbox.sln`
