# Convert Image to Matrix

Convert Image to Matrix

## Usage

``` r
firstLayerNotWhite(img_data)
```

## Arguments

- img_data:

  magick image object.

## Value

Integer matrix.

## Examples

``` r
library(magick)
#> Linking to ImageMagick 6.9.12.98
#> Enabled features: fontconfig, freetype, fftw, heic, lcms, pango, raw, webp, x11
#> Disabled features: cairo, ghostscript, rsvg
#> Using 4 threads

img <- system.file(package = "spatialist", "Kevin.jpg")
img_raw <- image_read(path = img)
img_data <- image_data(img_raw)
is.matrix(firstLayerNotWhite(img_data))
#> [1] TRUE
```
