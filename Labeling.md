The overall goal is to label each pixel within a blob with the same label number. The first stage in achieving this is to iterate through all the pixels, checking the label number of neighbouring pixels as you go. The image below shows the labelling kernel and how it is applied.

![http://www.labbookpages.co.uk/software/imgProc/files/kernel.png](http://www.labbookpages.co.uk/software/imgProc/files/kernel.png)

A buffer of equal dimensions as the original image (i.e. one buffer location per pixel) is needed to store the pixel labels. The buffer is initialised to all zeros, which equates to unlabelled. Scanning from top left to bottom right, the labelling kernel is applied per pixel (pixel position X). This is used to check the labels of neighbouring pixels (pixels A, B, C & D). The kernel shape means only neighbours that have already been labelled will be checked. The process for labelling pixels is described below:
```
l = 1                              // Initial Label number
for each pixel
  if pixel X is foreground
    if neighbours A,B,C & D are unlabelled (equal to zero)
      label pixel X with l
      increment l
    else
       num = neighbour label A,B,C & D with least value, not including 0
       label pixel X and pixels A, B, C & D if foreground with num
    end if
  end if
done
```
The images below shows an input monochrome image and the result of the labelling process. It is immediately obvious that the labelling process sometimes gives multiple labels to the same blob. To understand why this happens, take a look at the blob comprising labels 1, 2, 3 & 4. When the kernel reaches the first pixel labelled 2, it has no way of knowing at this stage that is is connected to those labelled 1. However, this is is easily resolved.

The solution is to keep a note which labels refer to the same blob when the two labelled sections eventually connect. This is described in the next section.

![http://www.labbookpages.co.uk/software/imgProc/files/blobLabels.png](http://www.labbookpages.co.uk/software/imgProc/files/blobLabels.png)