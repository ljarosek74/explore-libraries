CopyOf00\_filesystem-practice\_jenny.R
================
ljarosek
Wed Jan 31 14:05:36 2018

``` r
## First attempt: Just get it to work ----

list.files("C:/Users/ljarosek/Desktop/day1_s1_explore-libraries")
```

    ## [1] "01_explore-libraries_comfy.R"    "01_explore-libraries_jenny.R"   
    ## [3] "01_explore-libraries_spartan.R"  "day1_s1_explore-libraries.Rproj"

``` r
list.files("C:/Users/ljarosek/Desktop/day1_s1_explore-libraries", pattern = "\\.R$")
```

    ## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
    ## [3] "01_explore-libraries_spartan.R"

``` r
list.files(
  "C:/Users/ljarosek/Desktop/day1_s1_explore-libraries",
  pattern = "\\.R$",
  full.names = TRUE
)
```

    ## [1] "C:/Users/ljarosek/Desktop/day1_s1_explore-libraries/01_explore-libraries_comfy.R"  
    ## [2] "C:/Users/ljarosek/Desktop/day1_s1_explore-libraries/01_explore-libraries_jenny.R"  
    ## [3] "C:/Users/ljarosek/Desktop/day1_s1_explore-libraries/01_explore-libraries_spartan.R"

``` r
from_files <- list.files(
  "C:/Users/ljarosek/Desktop/day1_s1_explore-libraries",
  pattern = "\\.R$",
  full.names = TRUE
)

(to_files <- basename(from_files))
```

    ## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
    ## [3] "01_explore-libraries_spartan.R"

``` r
file.copy(from_files, to_files)
```

    ## [1] TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "01_explore-libraries_comfy.R"               
    ## [2] "01_explore-libraries_jenny.R"               
    ## [3] "01_explore-libraries_spartan.R"             
    ## [4] "CopyOf00_filesystem-practice_jenny.html"    
    ## [5] "CopyOf00_filesystem-practice_jenny.R"       
    ## [6] "CopyOf00_filesystem-practice_jenny.spin.R"  
    ## [7] "CopyOf00_filesystem-practice_jenny.spin.Rmd"
    ## [8] "explore-libraries.Rproj"                    
    ## [9] "README.md"

``` r
## Clean it out, so we can refine ----
file.remove(to_files)
```

    ## [1] TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "CopyOf00_filesystem-practice_jenny.html"    
    ## [2] "CopyOf00_filesystem-practice_jenny.R"       
    ## [3] "CopyOf00_filesystem-practice_jenny.spin.R"  
    ## [4] "CopyOf00_filesystem-practice_jenny.spin.Rmd"
    ## [5] "explore-libraries.Rproj"                    
    ## [6] "README.md"

``` r
## Copy again, tighter code ----
from_dir <- file.path("C:/Users/ljarosek", "Desktop", "day1_s1_explore-libraries")
from_files <- list.files(from_dir, pattern = "\\.R$", full.names = TRUE)
to_files <- basename(from_files)
file.copy(from_files, to_files)
```

    ## [1] TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "01_explore-libraries_comfy.R"               
    ## [2] "01_explore-libraries_jenny.R"               
    ## [3] "01_explore-libraries_spartan.R"             
    ## [4] "CopyOf00_filesystem-practice_jenny.html"    
    ## [5] "CopyOf00_filesystem-practice_jenny.R"       
    ## [6] "CopyOf00_filesystem-practice_jenny.spin.R"  
    ## [7] "CopyOf00_filesystem-practice_jenny.spin.Rmd"
    ## [8] "explore-libraries.Rproj"                    
    ## [9] "README.md"

``` r
## Clean it out, so we can use fs ----
file.remove(to_files)
```

    ## [1] TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "CopyOf00_filesystem-practice_jenny.html"    
    ## [2] "CopyOf00_filesystem-practice_jenny.R"       
    ## [3] "CopyOf00_filesystem-practice_jenny.spin.R"  
    ## [4] "CopyOf00_filesystem-practice_jenny.spin.Rmd"
    ## [5] "explore-libraries.Rproj"                    
    ## [6] "README.md"

``` r
## Copy again, using fs ----
library(fs)
```

    ## Warning: package 'fs' was built under R version 3.3.3

``` r
#(from_dir <- path_home("Desktop", "day1_s1_explore-libraries"))
(from_dir <- fs::path_real('../day1_s1_explore-libraries'))
```

    ## C:/Users/ljarosek/Desktop/day1_s1_explore-libraries

``` r
(from_files <- dir_ls(from_dir, glob = "*.R"))
```

    ## C:/Users/ljarosek/Desktop/day1_s1_explore-libraries/01_explore-libraries_comfy.R
    ## C:/Users/ljarosek/Desktop/day1_s1_explore-libraries/01_explore-libraries_jenny.R
    ## C:/Users/ljarosek/Desktop/day1_s1_explore-libraries/01_explore-libraries_spartan.R

``` r
(to_files <- path_file(from_files))
```

    ## 01_explore-libraries_comfy.R   01_explore-libraries_jenny.R   
    ## 01_explore-libraries_spartan.R

``` r
(out <- file_copy(from_files, to_files))
```

    ## 01_explore-libraries_comfy.R   01_explore-libraries_jenny.R   
    ## 01_explore-libraries_spartan.R

``` r
dir_ls()
```

    ## 01_explore-libraries_comfy.R
    ## 01_explore-libraries_jenny.R
    ## 01_explore-libraries_spartan.R
    ## CopyOf00_filesystem-practice_jenny.html
    ## CopyOf00_filesystem-practice_jenny.R
    ## CopyOf00_filesystem-practice_jenny.spin.R
    ## CopyOf00_filesystem-practice_jenny.spin.Rmd
    ## explore-libraries.Rproj
    ## README.md

``` r
dir_info()
```

    ##                                          path type    size permissions
    ## 1                01_explore-libraries_comfy.R file   1.12K        rw- 
    ## 2                01_explore-libraries_jenny.R file   1.54K        rw- 
    ## 3              01_explore-libraries_spartan.R file     850        rw- 
    ## 4     CopyOf00_filesystem-practice_jenny.html file  731.2K        rw- 
    ## 5        CopyOf00_filesystem-practice_jenny.R file      2K        rw- 
    ## 6   CopyOf00_filesystem-practice_jenny.spin.R file      2K        rw- 
    ## 7 CopyOf00_filesystem-practice_jenny.spin.Rmd file   2.11K        rw- 
    ## 8                     explore-libraries.Rproj file     218        rw- 
    ## 9                                   README.md file     138        rw- 
    ##     modification_time user group  device_id hard_links special_device_id
    ## 1 2018-01-31 09:57:02 <NA>  <NA> 1177936306          1                 0
    ## 2 2018-01-31 09:57:02 <NA>  <NA> 1177936306          1                 0
    ## 3 2018-01-31 09:57:02 <NA>  <NA> 1177936306          1                 0
    ## 4 2018-01-31 13:57:41 <NA>  <NA> 1177936306          1                 0
    ## 5 2018-01-31 14:05:33 <NA>  <NA> 1177936306          1                 0
    ## 6 2018-01-31 14:05:36 <NA>  <NA> 1177936306          1                 0
    ## 7 2018-01-31 14:05:36 <NA>  <NA> 1177936306          1                 0
    ## 8 2018-01-31 13:32:20 <NA>  <NA> 1177936306          1                 0
    ## 9 2018-01-31 13:46:09 <NA>  <NA> 1177936306          1                 0
    ##          inode block_size blocks flags generation         access_time
    ## 1 1.407375e+15       4096      8     0          0 2018-01-31 14:05:36
    ## 2 1.125900e+15       4096      8     0          0 2018-01-31 14:05:36
    ## 3 1.125900e+15       4096      8     0          0 2018-01-31 14:05:36
    ## 4 8.725724e+15       4096   1464     0          0 2018-01-31 13:57:41
    ## 5 6.473924e+15       4096      8     0          0 2018-01-31 13:50:58
    ## 6 1.125900e+15       4096      8     0          0 2018-01-31 14:05:36
    ## 7 5.629500e+14       4096      8     0          0 2018-01-31 14:05:36
    ## 8 5.629500e+14       4096      0     0          0 2018-01-31 13:32:20
    ## 9 8.444249e+14       4096      0     0          0 2018-01-31 13:46:09
    ##           change_time          birth_time
    ## 1 2018-01-31 09:59:00 2018-01-31 14:05:36
    ## 2 2018-01-31 10:02:41 2018-01-31 14:05:36
    ## 3 2018-01-31 09:57:02 2018-01-31 14:05:36
    ## 4 2018-01-31 13:57:41 2018-01-31 13:57:41
    ## 5 2018-01-31 14:05:33 2018-01-31 13:50:58
    ## 6 2018-01-31 14:05:36 2018-01-31 14:05:36
    ## 7 2018-01-31 14:05:36 2018-01-31 14:05:36
    ## 8 2018-01-31 13:32:20 2018-01-31 13:32:20
    ## 9 2018-01-31 13:46:09 2018-01-31 13:32:20

``` r
## Sidebar: Why does Jenny name files this way? ----
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 3.3.3

    ## -- Attaching packages ---------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 2.2.1     v purrr   0.2.4
    ## v tibble  1.4.2     v dplyr   0.7.4
    ## v tidyr   0.8.0     v stringr 1.2.0
    ## v readr   1.1.1     v forcats 0.2.0

    ## Warning: package 'ggplot2' was built under R version 3.3.3

    ## Warning: package 'tibble' was built under R version 3.3.3

    ## Warning: package 'tidyr' was built under R version 3.3.3

    ## Warning: package 'readr' was built under R version 3.3.3

    ## Warning: package 'purrr' was built under R version 3.3.3

    ## Warning: package 'dplyr' was built under R version 3.3.3

    ## Warning: package 'stringr' was built under R version 3.3.3

    ## Warning: package 'forcats' was built under R version 3.3.3

    ## -- Conflicts ------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
ft <- tibble(files = dir_ls(glob = "*.R"))
ft
```

    ## # A tibble: 5 x 1
    ##   files                                    
    ##   <fs::path>                               
    ## 1 01_explore-libraries_comfy.R             
    ## 2 01_explore-libraries_jenny.R             
    ## 3 01_explore-libraries_spartan.R           
    ## 4 CopyOf00_filesystem-practice_jenny.R     
    ## 5 CopyOf00_filesystem-practice_jenny.spin.R

``` r
ft %>%
  filter(str_detect(files, "explore"))
```

    ## Warning: package 'bindrcpp' was built under R version 3.3.3

    ## # A tibble: 3 x 1
    ##   files                         
    ##   <fs::path>                    
    ## 1 01_explore-libraries_comfy.R  
    ## 2 01_explore-libraries_jenny.R  
    ## 3 01_explore-libraries_spartan.R

``` r
ft %>%
  mutate(files = path_ext_remove(files)) %>%
  separate(files, into = c("i", "topic", "flavor"), sep = "_")
```

    ## # A tibble: 5 x 3
    ##   i        topic               flavor    
    ##   <chr>    <chr>               <chr>     
    ## 1 01       explore-libraries   comfy     
    ## 2 01       explore-libraries   jenny     
    ## 3 01       explore-libraries   spartan   
    ## 4 CopyOf00 filesystem-practice jenny     
    ## 5 CopyOf00 filesystem-practice jenny.spin

``` r
#dirs <- dir_ls(path_home("Desktop"), type = "directory")
dirs <- dir_ls(fs::path_real('../day1_s1_explore-libraries'))

(dt <- tibble(dirs = path_file(dirs)))
```

    ## # A tibble: 4 x 1
    ##   dirs                           
    ##   <fs::path>                     
    ## 1 01_explore-libraries_comfy.R   
    ## 2 01_explore-libraries_jenny.R   
    ## 3 01_explore-libraries_spartan.R 
    ## 4 day1_s1_explore-libraries.Rproj

``` r
dt %>%
  separate(dirs, into = c("day", "session", "topic"), sep = "_")
```

    ## # A tibble: 4 x 3
    ##   day   session           topic                  
    ##   <chr> <chr>             <chr>                  
    ## 1 01    explore-libraries comfy.R                
    ## 2 01    explore-libraries jenny.R                
    ## 3 01    explore-libraries spartan.R              
    ## 4 day1  s1                explore-libraries.Rproj

``` r
## Principled use of delimiters --> meta-data can be recovered from filename

## Clean it out, so we reset for workshop ----
file_delete(to_files)
dir_ls()
```

    ## CopyOf00_filesystem-practice_jenny.html
    ## CopyOf00_filesystem-practice_jenny.R
    ## CopyOf00_filesystem-practice_jenny.spin.R
    ## CopyOf00_filesystem-practice_jenny.spin.Rmd
    ## explore-libraries.Rproj
    ## README.md
