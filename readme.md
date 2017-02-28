# DOSBox - Pixel-perfect mod

This is a modified version of the original DOSBox for pixel purists, who like their pixels perfectly square.

This mod add a pixel-perfect mode, which makes the rendered image fill as much of your screen as possible while keeping the pixels square and scaled to the nearest integer (e.g. 1x1, 2x2, 3x3, ...). This makes the resulting image super crisp and super blocky, as it should be.


## Download

You can find the Windows binary in the `releases` tab. 0.74 is the latest stable version (which is pretty old), SVN is the latest, but potentially unstable version.


## Modifications

The main feature is the automatic snapping of scale to the nearest integer. There are other improvements as well. Pixels are generally crisper, as original DOSBox renders a stretched image to a power-of-two texture, which is then stretched to the screen. This mod makes creates a texture with exact dimensions, which may cause issues with some _very_ old video cards, but improves the quality of the image.

The original `aspect=true` setting tries to mimic a 4:3 monitor by stretching non 4:3 resolutions to this aspect ratio, thus making the pixels rectangular. This behavior is disabled and pixels are _always_ square.

`pixelperfect` option is added to the `[sdl]` section of `dosbox.conf`, so that you can enable or disable pixel-perfect scaling. When disabled, the image is stretched proportionally to fill the screen.


## DOSBox config

You can just use the config provided with the binary. If you have your own special `dosbox.conf`, make sure the values match the ones below to get the desired effect:

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

The project should be buildable in Visual Studio 2015 (any edition will do) without any configuration whatsoever. Open `visualc_net/dosbox.sln` and build the project.
