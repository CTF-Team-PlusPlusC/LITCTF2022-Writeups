# Flashy Colors

## Problem Statement
Computer pixels are so interesting. Do you know that they are actually made of three lights? It's like each pixel has 3 tiny light switches, red, green, and blue, that can go on or off to create so many different colors.

Anyway, here are some flashy colors for you.
https://drive.google.com/uc?export=download&id=1X7PMv0vi-Cp_xKzYeFd_wxxPGY373jgz

## Solution
Download the file, and open it up. We see that we have a 3bit image, with 1 bit per channel. We do the rest in python (the file is renamed to `fc.png`).

Let's first convert this image to a 10x10 pixel image.
Then we can get the rgb values for each pixel. We convert this to a numpy array. We tried flattening the image row-wise but didn't get anything useful.
Flattening the image column-wise (because that's the next best thing), and removing the first 4 bits (motivated by observing that `L = 01001100`) we get
the flag.

```py
from PIL import Image
import numpy as np

img = Image.open("fc.png")
img.resize((10, 10), Image.NONE).show()
img.resize((10, 10), Image.NONE).save('fc_resize.png')

img = numpy.array(img)[:,:,:3]  # Remove the A channel
img = img.astype(int)
img = img // 255

# Flatten by column
print(img.transpose(1, 0, 2).flatten())
# >>> array([0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1,
#      0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 0, 0,
#      0, 1, 0, 0, 0, 1, 1, 0, 0, 1, 1, 1, 1, 0, 1, 1, 0, 0, 1, 1, 0, 0,
#      0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 0, 1,
#      1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1,
#      1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0,
#      0, 1, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1, 1, 1, 0, 1,
#      0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 1,
#      0, 0, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1,
#      1, 0, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1,
#      0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 1, 1, 0,
#      0, 1, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1, 1, 0, 0, 0, 1, 1, 0, 0, 1, 1,
#      0, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1, 1, 1, 0, 1,
#      1, 1, 0, 0, 1, 0, 0, 1, 1, 1, 1, 1, 0, 1])
print(*img.transpose(1, 0, 2).flatten(), sep="")
# >>> 000001001100010010010101010001000011010101000100011001111011001100000100110101000111010111110100100101011111011011000011000001110110011001010101111101110100011010000011001101110011001100110101111101100110011011000110000100110101011010000111100101011111011000110011000001101100011011110111001001111101

```
Converting the above string (without the first 4 characters) to ascii, we get `LITCTF{0MG_I_l0ve_th3s3_fla5hy_c0lor}`:

<img width="634" alt="image" src="https://user-images.githubusercontent.com/58674441/181069435-f5bdbcee-9d2f-49f3-855b-3105ae0f1591.png">

## Answer:
`LITCTF{0MG_I_l0ve_th3s3_fla5hy_c0lor}`
