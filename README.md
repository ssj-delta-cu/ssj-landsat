# ssj-landsat

This repository holds Landsat8 imagery input data and some derived
projects for the SSJ project.

Because of the size of these files, we use git-lfs to store these data. Users wishing to retrieve these images via a ```git clone``` will need [git-lfs](*https://git-lfs.github.com/) installed on their client system.

* [l8_surface_reflectance_0.3.1](l8_surface_reflectance_0.3.1) - contains the USGS standard surface reflectance product.  Each of the 22 Landsat images for the 2015 water year are included.  Two images are combined, and then the product is clipped to the delta service region.  Data are organized by data, and each date is about 140M in size.
