# subfits
Makes subsets of huge multi-dimensional FITS datasets

subfits uses python memory mapping and StreamingHDU to handle Flexible Image Transport System (FITS) multi-dimensional datasets on systems with less memory than the size of the dataset being read or written (respectively).

**Purpose**: Make a subimage of a large multi-dimensional FITS file without reading the whole file into memory. Will not overwrite existing file. Will only itemize input FITS file if no output specified. The output dataset is written in chunks.

**Conventions**: Pixels start at 1, following FITS convention for CRPIX. Specify a start and end pixel OR start and end world coordinate for each dimension in the order in which the dimensions appear in the FITS file (e.g. min,max,min,max,...). Unspecified min/max or min/max=0 means default to min/max of that dimension. 

**Limits**: maximum number of dimensions = 9; maximum voxels before chunking output (approx) 250e6 (configurable). Tested on 500GB ASKAP/WALLABY FITS cubes. 

**Useage**: subfits -i <input file> -o <output file> -p/w <x1,x2,y1,y2,z1,z2> -s <dx,dy,dz> -r OR subfits --in=<input file> --o=<output file> --pix/world=<x1,x2,y1,y2,z1,z2> --skip=<dx,dy,dz> -r 

```
OPTIONS          DESCRIPTION

-?     ?        help
-i     in=      input file (FITS format)
-o     out=     output file
-p     pix=     pixels (e.g. 0,100,0,100,0,10)
-r     remove   remove dummy axes
-d     skip=    skip (e.g. 2,2,2)
-w     world=   world (e.g. 120.0,100.0,-20,-10.0,0,0)
```
