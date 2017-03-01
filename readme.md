# DOSBox - Pixel-perfect mod

<p align="center"><img src="https://cloud.githubusercontent.com/assets/4263742/23454383/521f32ae-fe6c-11e6-8be2-8f6471b24ed3.png" alt="DOSBox original vs pixel-perfect mod"/></p>

This is a modified version of the original DOSBox for pixel purists, who like their pixels perfectly square.

This mod add a pixel-perfect mode, which makes the rendered image fill as much of your screen as possible while keeping the pixels square and scaled to the nearest integer (e.g. 1x1, 2x2, 3x3, ...). This eliminates any uneven pixels and makes the resulting image super crisp.


## Download

You can download the Windows binary from the [releases tab](https://github.com/bladeSk/DOSBox-pixel-perfect/releases). 0.74 is the latest stable version (which is pretty old), SVN is the latest, but potentially unstable version.


## Modifications

There are other improvements, apart from making the pixels even. Pixels should be generally crisper, as original DOSBox renders a stretched image to a power-of-two texture, which is then stretched to the screen. This mod makes creates a texture with exact dimensions, which may cause issues with some _very_ old video cards, but improves the quality of the image.

The original `aspect=true` setting tries to mimic a 4:3 monitor by stretching non 4:3 resolutions to this aspect ratio, thus making the pixels rectangular. This behavior is disabled and pixels are _always_ square.

`pixelperfect` option is added to the `[sdl]` section of `dosbox.conf`, so that you can enable or disable pixel-perfect scaling. When disabled, the image is stretched proportionally to fill the screen.


## DOSBox config

You can just use the config provided with the binary. If you have your own special `dosbox.conf`, make sure your values match the ones below to get the desired effect:

	[sdl]
	fullscreen=true
	fulldouble=true
	fullresolution=desktop
	output=openglnb # pixel-perfect scaling only works with OpenGL!
	pixelperfect=true

	[render]
	aspect=true
	scaler=none


## Building

The project should be buildable in Visual Studio 2015 (any edition) without any configuration whatsoever. Open `visualc_net/dosbox.sln` and build the project.
