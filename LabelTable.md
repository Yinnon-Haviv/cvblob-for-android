To deal with the problem of multiple label numbers per blob, it is important to record when two differently labelled sections of a blob meet.

![http://www.labbookpages.co.uk/software/imgProc/files/labelTable.png](http://www.labbookpages.co.uk/software/imgProc/files/labelTable.png)

One approach is to create a label table (not to be confused with the label buffer) that links together all the labels within a blob. When a new label number is added to the label buffer, the label table value is initialised to label's number. Subsequently, the label table value is updated with the minimum label within the kernel. The image to the right helps demonstrate this.

The label table before it is updated for the currently kernel position is shown. It can be seen that label number 2 has already been associated with label 1 as they are part of the same blob. The label number for the pixel is calculated, in this case it will be 3. The table value for each label number referenced by the neighbours is then updated with the calculated label number.

The final label table for the reference image is shown below.
![http://www.labbookpages.co.uk/software/imgProc/files/finalTable.png](http://www.labbookpages.co.uk/software/imgProc/files/finalTable.png)

It is easy to extract the labels for each blob from this table. Label 4 is associated with label 1 via label 3.

| **Blob** |	**Labels** |
|:---------|:-----------|
|1         |	1, 2, 3 & 4 |
|2         |	5          |
|3         |	6          |
|4         |	7, 8 & 10  |
|5         |	9          |

## Blob Position and Mass ##

A similar approach is used to calculate each blob's position, size and mass. The complete algorithm including these calculations is described in the example program source code.