# Whistler

## What it does

Whistler is an incremental painting program. Takes a source image and begins painting a copy of it, gradually getting closer to the source image starting from a blank canvas image.

A gallery of some photographs created by Whistler alongside the originals can be found [here](http://blainmaguire.com/projects#whistler)

## How it works

A two dimensional colored Bézier surface is used to create brushstrokes. No textures are used. Brushstrokes are randomized within various limits (like the minimum and maximum size).

A random brushstroke is painted. The newly painted area is compared with the original image. If this area is now closer to the original image it is kept, otherwise it is reverted to how it was previously.

## How to use it

Navigate to the folder where you have saved whistler. A minimal example would be:

    $ python whistler.py /some/path/mypicture.jpg
    
This is using all the defaults. If you ctrl+c the application (or the autosave kicks in) a file called poly_mypicture.jpg.bmp will be created in /some/path. This file will be reloaded the next time the program runs and it will continue from it.

    $ python whistler.py ~/images/pic.jpg --alpha 0.0125 --xmax 2 --ymax 2 --xmin 4 --ymin 4
    
The above example specifices an alpha value of 1.25% (range is between 0-1). The maximum width and height for a brushstroke is half the image width and height. Likewise the smallest brushstroke must be at least a quarter of the image width and height.

The default of using a divisor of image width and height for specifying the range for brushstrokes works well enough for a variety of image resolutions. However, sometimes you may want to specify an exact pixel value.

    $ python whistler.py ~/images/pic.jpg -p --xmax 1024 --ymax 1024 --xmin 200 --ymin 200

Using the -p (or --usepixels) option tells the program all brushstroke size arguments are in pixels and aren't divisors of image width or height. If you just want pixels for specific sizes you can leave this out and specify flags like --usepixels-ymin.

You may be wondering why the default extension is .bmp. PNG was considered and save files compress well for early approximations. However, with PNG, as the save file becomes more complex and more photo-like it takes up a lot more space than an original jpg image. You override this default with the --ext option.

## Requirements

This program is written entirely in Python and uses PIL (python imaging library) and numpy. Argparse is also used for command line arguments. Python 2.7+ is recommended to get up and running quickly and older versions of python will require extra effort.

## Some Creative Ideas

Just by changing different values like the brush sizes or alpha value can give drastically different results. Stopping and starting the program at different intervals with different values can also give some interesting results. e.g. alternating between small brush sizes with high alpha and large brush sizes with low alpha.

As the save files are images themselves it opens up a number of possibilities. One is making multiple copies of the save file as it runs and then blending them together in different ways using image manipulation software. Enhancing colors or adjusting levels can also give interesting results.

## License

Two clause BSD license. See LICENSE for more details.
