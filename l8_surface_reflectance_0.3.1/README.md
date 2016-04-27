#  L8SR Surface Reflectance

Landsat 8 Surface Reflectance data are generated from the [L8SR algorithm](http://landsat.usgs.gov/documents/provisional_l8sr_product_guide.pdf).

The retrieved images were combined from scenes, 44033 and 044034.  Bands 1 through 7  were combined into a single relfectance image of 7 bands.  Additionally a few cloud mask images are also included.  They were then clipped using the gdal software package.  The [Makefile](Makefile) offers more detailed information.
