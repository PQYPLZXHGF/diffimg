# diffimg
Get the % difference in images using PIL's histogram + generate a diff image. Images should be the same size.

### Installation

Now available from PyPi: `pip install diffimg`

### Usage

```
>>> from diffimg import diff
>>> diff('mario-circle-cs.png', 'mario-circle-node.png')
0.01866502624671916
```
The [very simple](/diffimg/__init__.py#L11) `diff` function returns a raw ratio instead of a % by default.

```
diff(im1_file, 
     im2_file, 
     delete_diff_file=False, 
     diff_img_file='diff_img.jpg')
```
`im1_file, im2_file`: filenames of images to diff.

`delete_diff_file`: a fill showing the differing areas of the two images is generated in order to measure the diff ratio. Setting this to `True` removes it after calculating the ratio.

`diff_img_file`: filename for the diff image file. Defaults to 'diff_img.jpg' (regardless of inputed file's types)

### As command line tool

`python diffimg image1 image2 [-r/--ratio] [-d/--delete] [-f/--filename DIFF_IMG_FILE]`

`--ratio` outputs a number between 0 and 1 instead of the default `Images differ by X%`.

`--delete` removes the diff file after retrieving ratio/percentage.

`--filename` specifies a filename to save the diff image under. Must use a valid extension.

### Formula 

The difference is defined by the average % difference between each of the channels (R,G,B,A?) at each pair of pixels A<sub>xy</sub>, B<sub>xy</sub> at the same coordinates in each of the two images (why they need to be the same size), averaged over all pairs of pixels. 

For example, compare two 1x1 images _A_ and _B_ (a trivial example, >1 pixels would have another step to find the average of all pixels):

_A_<sub>1,1</sub> = RGB(255,0,0) _(pure red)_

_B_<sub>1,1</sub> = RGB(100,0,0) _(dark red)_

((255-100)/255 + (0/0)/255 + (0/0)/255))/3 = (155/255)/3 = 0.202614379

So these two 1x1 images differ by __20.2614379%__ according to this formula.

## Sample image 1
![Alt text](/mario-circle-cs.png "Image 1")

## Sample image 2
![Alt text](/mario-circle-node.png "Image 2")

## Resulting diff image
![Alt text](/diff_img.jpg "Difference Image")

## Difference percentage output
`Images differ by 1.86650262467%`
