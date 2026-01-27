# Spatialise yourself!

**Compiled date**: 2026-01-27

**Last edited**: 2020-04-20

**License**: MIT + file LICENSE

## Introduction

*[spatialist](https://github.com/kevinrue/spatialist)* is an *R*
package.

Once installed, the package can be loaded and attached to your current
workspace as follows:

``` r

library(spatialist)
```

Other helpful libraries.

``` r

library(ggplot2)
```

## Demonstration

### Input file

``` r

input_file <- system.file(package = "spatialist", "Kevin.jpg")
```

### Output types

#### Raw image

``` r

kevin <- spatialise(
  path = input_file
)
print(kevin)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 WEBP    1140   1140 sRGB       FALSE    69414 72x72
```

![Raw image.](spatialist_files/figure-html/raw-1.png)

#### Flattened image

``` r

kevin <- spatialise(
  path = input_file,
  return.type = "flatten",
  extras = list(
    image_flatten = list(operator = "Modulate")
  )
)
print(kevin)
#> # A tibble: 1 × 7
#>   format width height colorspace matte filesize density
#>   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
#> 1 WEBP    1140   1140 sRGB       FALSE        0 72x72
```

![Flattened image.](spatialist_files/figure-html/flatten-1.png)

#### Image data

``` r

kevin <- spatialise(
  path = input_file,
  return.type = "data"
)
kevin
#> 3 channel 1140x1140 bitmap array: 'bitmap' raw [1:3, 1:1140, 1:1140] ff ff ff ff ...
```

#### Processed matrix

``` r

kevin <- spatialise(
  path = input_file,
  return.type = "matrix"
)
dim(kevin)
#> [1] 1140 1140
```

#### Heat map

``` r

spatialise(
  path = input_file,
  return.type = "heatmap"
)
```

![Heat map.](spatialist_files/figure-html/heatmap-1.png)

#### Pixel coordinates

``` r

kevin <- spatialise(
  path = input_file,
  return.type = "xy"
)
head(kevin)
#>       x   y
#> 1   571 -80
#> 24  573 -87
#> 30  579 -87
#> 423 561 -94
#> 429 567 -94
#> 435 573 -94
```

#### Scatter plot

``` r

spatialise(
  path = input_file,
  return.type = "point",
  downsample = 100
) + theme_void()
```

![Scatter plot.](spatialist_files/figure-html/point-1.png)

#### Jittered scatter plot

``` r

spatialise(
  path = input_file,
  return.type = "jitter",
  downsample = 100,
  jitter = 5
) + theme_void()
```

![Jittered scatter plot.](spatialist_files/figure-html/jitter-1.png)

#### Xenium-like

``` r

spatialise(
  path = input_file,
  return.type = "spatial",
  downsample = 75,
  jitter = 5,
  extras = list(
    cluster = list(k.nn = 50, k.cluster = 10)
  )
) + theme_void() + guides(colour = "none")
```

![Xenium-like plot.](spatialist_files/figure-html/spatial-1.png)

#### Visium-like

``` r

spatialise(
  path = input_file,
  return.type = "visium",
  downsample = 100,
  point.size = 0.25,
  extras = list(
    cluster = list(k.nn = 50, k.cluster = 10)
  )
) + theme_void() + guides(colour = "none")
```

![Visium-like plot.](spatialist_files/figure-html/visium-1.png)

## Additional information

The GitHub repository contains the development version of the package,
where new functionality is added over time. The authors appreciate
well-considered suggestions for improvements or new features, or even
better, pull requests.

If you use *[spatialist](https://github.com/kevinrue/spatialist)* for
your analysis, please cite it as shown below:

``` r

citation("spatialist")
#> To cite package 'spatialist' in publications use:
#> 
#>   Rue-Albrecht K (2024). _spatialist: Spatialise Your Images_. R
#>   package version 0.1.0, <https://kevinrue.github.io/spatialist>.
#> 
#> A BibTeX entry for LaTeX users is
#> 
#>   @Manual{,
#>     title = {spatialist: Spatialise Your Images},
#>     author = {Kevin Rue-Albrecht},
#>     year = {2024},
#>     note = {R package version 0.1.0},
#>     url = {https://kevinrue.github.io/spatialist},
#>   }
```

## Session Info

``` r

sessionInfo()
#> R Under development (unstable) (2026-01-25 r89330)
#> Platform: x86_64-pc-linux-gnu
#> Running under: Ubuntu 24.04.3 LTS
#> 
#> Matrix products: default
#> BLAS:   /usr/lib/x86_64-linux-gnu/openblas-pthread/libblas.so.3 
#> LAPACK: /usr/lib/x86_64-linux-gnu/openblas-pthread/libopenblasp-r0.3.26.so;  LAPACK version 3.12.0
#> 
#> locale:
#>  [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
#>  [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
#>  [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
#>  [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                 
#>  [9] LC_ADDRESS=C               LC_TELEPHONE=C            
#> [11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       
#> 
#> time zone: UTC
#> tzcode source: system (glibc)
#> 
#> attached base packages:
#> [1] stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] ggplot2_4.0.1    spatialist_0.1.0 BiocStyle_2.39.0
#> 
#> loaded via a namespace (and not attached):
#>   [1] rlang_1.1.7                 magrittr_2.0.4             
#>   [3] shinydashboard_0.7.3        clue_0.3-66                
#>   [5] GetoptLong_1.1.0            otel_0.2.0                 
#>   [7] matrixStats_1.5.0           compiler_4.6.0             
#>   [9] mgcv_1.9-4                  png_0.1-8                  
#>  [11] systemfonts_1.3.1           vctrs_0.7.1                
#>  [13] pkgconfig_2.0.3             shape_1.4.6.1              
#>  [15] crayon_1.5.3                fastmap_1.2.0              
#>  [17] magick_2.9.0                XVector_0.51.0             
#>  [19] labeling_0.4.3              fontawesome_0.5.3          
#>  [21] utf8_1.2.6                  promises_1.5.0             
#>  [23] rmarkdown_2.30              shinyAce_0.4.4             
#>  [25] ragg_1.5.0                  xfun_0.56                  
#>  [27] cachem_1.1.0                jsonlite_2.0.0             
#>  [29] listviewer_4.0.0            later_1.4.5                
#>  [31] DelayedArray_0.37.0         parallel_4.6.0             
#>  [33] cluster_2.1.8.1             R6_2.6.1                   
#>  [35] bslib_0.10.0                RColorBrewer_1.1-3         
#>  [37] GenomicRanges_1.63.1        jquerylib_0.1.4            
#>  [39] Rcpp_1.1.1                  Seqinfo_1.1.0              
#>  [41] bookdown_0.46               SummarizedExperiment_1.41.0
#>  [43] iterators_1.0.14            knitr_1.51                 
#>  [45] IRanges_2.45.0              httpuv_1.6.16              
#>  [47] Matrix_1.7-4                splines_4.6.0              
#>  [49] igraph_2.2.1                tidyselect_1.2.1           
#>  [51] abind_1.4-8                 yaml_2.3.12                
#>  [53] doParallel_1.0.17           codetools_0.2-20           
#>  [55] miniUI_0.1.2                lattice_0.22-7             
#>  [57] tibble_3.3.1                withr_3.0.2                
#>  [59] Biobase_2.71.0              shiny_1.12.1               
#>  [61] S7_0.2.1                    evaluate_1.0.5             
#>  [63] desc_1.4.3                  circlize_0.4.17            
#>  [65] pillar_1.11.1               BiocManager_1.30.27        
#>  [67] MatrixGenerics_1.23.0       DT_0.34.0                  
#>  [69] foreach_1.5.2               stats4_4.6.0               
#>  [71] shinyjs_2.1.1               generics_0.1.4             
#>  [73] dbscan_1.2.4                iSEE_2.23.1                
#>  [75] S4Vectors_0.49.0            scales_1.4.0               
#>  [77] xtable_1.8-4                glue_1.8.0                 
#>  [79] tools_4.6.0                 colourpicker_1.3.0         
#>  [81] fs_1.6.6                    grid_4.6.0                 
#>  [83] colorspace_2.1-2            SingleCellExperiment_1.33.0
#>  [85] nlme_3.1-168                vipor_0.4.7                
#>  [87] cli_3.6.5                   textshaping_1.0.4          
#>  [89] viridisLite_0.4.2           S4Arrays_1.11.1            
#>  [91] ComplexHeatmap_2.27.0       dplyr_1.1.4                
#>  [93] gtable_0.3.6                rintrojs_0.3.4             
#>  [95] sass_0.4.10                 digest_0.6.39              
#>  [97] BiocGenerics_0.57.0         SparseArray_1.11.10        
#>  [99] ggrepel_0.9.6               rjson_0.2.23               
#> [101] htmlwidgets_1.6.4           farver_2.1.2               
#> [103] htmltools_0.5.9             pkgdown_2.2.0              
#> [105] lifecycle_1.0.5             shinyWidgets_0.9.0         
#> [107] GlobalOptions_0.1.3         mime_0.13
```

## References
