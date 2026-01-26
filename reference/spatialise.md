# Spatialise Images

Main function.

## Usage

``` r
spatialise(
  path,
  return.type = c("raw", "flatten", "data", "matrix", "heatmap", "xy", "point", "jitter",
    "spatial", "visium"),
  downsample = 150,
  jitter = 1,
  point.size = 1,
  img2matrix.FUN = firstLayerNotWhite,
  invert = FALSE,
  extras = list()
)
```

## Arguments

- path:

  Path to the input file.

- return.type:

  Type of image to return.

- downsample:

  Integer resolution or \`FALSE\`.

- jitter:

  Amount of jitter.

- point.size:

  Point size

- img2matrix.FUN:

  Function converting image data to a matrix.

- invert:

  Use negative of the image.

- extras:

  List of options for sub-functions.

## Value

A \`ggplot\` object.

## Examples

``` r
kevin <- spatialise(
  path = system.file(package = "spatialist", "Kevin.jpg")
)
print(kevin)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 WEBP    1140   1140 sRGB       FALSE    69414 72x72  

kevin <- spatialise(
  path = system.file(package = "spatialist", "Kevin.jpg"),
  return.type = "flatten",
  extras = list(
    image_flatten = list(operator = "Threshold")
  )
)
print(kevin)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 WEBP    1140   1140 sRGB       FALSE        0 72x72  
```
