## DXT3/5 images look fine, but DXT1 images come out black! What's going on? ##

By default, squish tries to preserve both colour _and_ alpha information.  In DXT3/5 these are encoded independently, but DXT1 can only represent zero alpha when all the colour channels are zero too.

As a side-effect, when a pixel with zero alpha is compressed to DXT1, this forces the colour channels to zero.  If you are not using the alpha channel, you should set a non-zero value for the pixel alpha values, like 255 (i.e. fully opaque).

_In future there may be a flag added to DXT1 mode to ignore the alpha channel completely (and allow 0 or 255 arbitrarily in the output), but this default behaviour will not be changed._