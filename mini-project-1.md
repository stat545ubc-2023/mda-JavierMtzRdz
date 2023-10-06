Mini Data-Analysis Deliverable 1
================

# Welcome to your (maybe) first-ever data analysis project!

And hopefully the first of many. Let’s get started:

1.  Install the [`datateachr`](https://github.com/UBC-MDS/datateachr)
    package by typing the following into your **R terminal**:

<!-- -->

    install.packages("devtools")
    devtools::install_github("UBC-MDS/datateachr")

2.  Load the packages below.

``` r
library(datateachr)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(ggridges)
library(scales)
```

    ## 
    ## Attaching package: 'scales'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     discard
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     col_factor

2.1 Save ploting theme

``` r
mi_tema <- function (...) {
  ggplot2::theme_minimal() + 
    ggplot2::theme(text = ggplot2::element_text(family = "Lato"), 
                   axis.line = ggplot2::element_line(linewidth = 0.3), 
                   plot.title = ggplot2::element_text(hjust = 0.5,
                                                      size = 14,
                                                      face = "bold", 
                                                      color = "grey20"), 
                   plot.title.position = "plot", 
                   plot.subtitle = ggplot2::element_text(hjust = 0.5,
                                                         size = 12,
                                                         color = "gray50"), 
                   plot.caption = ggplot2::element_text(color = "gray50",
                                                        size = 10, 
                                                        hjust = 0),
                   panel.grid = ggplot2::element_line(linetype = 2, 
                                                      linewidth = 0.3,
                                                      color = "gray90"), 
                   panel.grid.minor = ggplot2::element_blank(), 
                   legend.key.width = unit(0.7, "cm"), 
                   legend.margin = margin(0, 0, 0, 0), 
                   legend.spacing = unit(0, "cm"),
                   strip.background = ggplot2::element_rect(fill = "gray95", 
                                                            linetype = "blank"), 
                   panel.border = ggplot2::element_rect(color = "gray95", 
                                                        fill = NA),
                   rect = ggplot2::element_rect(fill = "transparent")) + 
    ggplot2::theme(...)
}
```

3.  Make a repository in the <https://github.com/stat545ubc-2023>
    Organization. You can do this by following the steps found on canvas
    in the entry called [MDA: Create a
    repository](https://canvas.ubc.ca/courses/126199/pages/mda-create-a-repository).
    One completed, your repository should automatically be listed as
    part of the stat545ubc-2023 Organization.

# Instructions

## For Both Milestones

- Each milestone has explicit tasks. Tasks that are more challenging
  will often be allocated more points.

- Each milestone will be also graded for reproducibility, cleanliness,
  and coherence of the overall Github submission.

- While the two milestones will be submitted as independent
  deliverables, the analysis itself is a continuum - think of it as two
  chapters to a story. Each chapter, or in this case, portion of your
  analysis, should be easily followed through by someone unfamiliar with
  the content.
  [Here](https://swcarpentry.github.io/r-novice-inflammation/06-best-practices-R/)
  is a good resource for what constitutes “good code”. Learning good
  coding practices early in your career will save you hassle later on!

- The milestones will be equally weighted.

## For Milestone 1

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-1.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work below --->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to the mini-analysis GitHub repository you made
earlier, and tag a release on GitHub. Then, submit a link to your tagged
release on canvas.

**Points**: This milestone is worth 36 points: 30 for your analysis, and
6 for overall reproducibility, cleanliness, and coherence of the Github
submission.

# Learning Objectives

By the end of this milestone, you should:

- Become familiar with your dataset of choosing
- Select 4 questions that you would like to answer with your data
- Generate a reproducible and clear report using R Markdown
- Become familiar with manipulating and summarizing your data in tibbles
  using `dplyr`, with a research question in mind.

# Task 1: Choose your favorite dataset

The `datateachr` package by Hayley Boyce and Jordan Bourak currently
composed of 7 semi-tidy datasets for educational purposes. Here is a
brief description of each dataset:

- *apt_buildings*: Acquired courtesy of The City of Toronto’s Open Data
  Portal. It currently has 3455 rows and 37 columns.

- *building_permits*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 20680 rows and 14 columns.

- *cancer_sample*: Acquired courtesy of UCI Machine Learning Repository.
  It currently has 569 rows and 32 columns.

- *flow_sample*: Acquired courtesy of The Government of Canada’s
  Historical Hydrometric Database. It currently has 218 rows and 7
  columns.

- *parking_meters*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 10032 rows and 22 columns.

- *steam_games*: Acquired courtesy of Kaggle. It currently has 40833
  rows and 21 columns.

- *vancouver_trees*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 146611 rows and 20 columns.

**Things to keep in mind**

- We hope that this project will serve as practice for carrying our your
  own *independent* data analysis. Remember to comment your code, be
  explicit about what you are doing, and write notes in this markdown
  document when you feel that context is required. As you advance in the
  project, prompts and hints to do this will be diminished - it’ll be up
  to you!

- Before choosing a dataset, you should always keep in mind **your
  goal**, or in other ways, *what you wish to achieve with this data*.
  This mini data-analysis project focuses on *data wrangling*,
  *tidying*, and *visualization*. In short, it’s a way for you to get
  your feet wet with exploring data on your own.

And that is exactly the first thing that you will do!

1.1 **(1 point)** Out of the 7 datasets available in the `datateachr`
package, choose **4** that appeal to you based on their description.
Write your choices below:

**Note**: We encourage you to use the ones in the `datateachr` package,
but if you have a dataset that you’d really like to use, you can include
it here. But, please check with a member of the teaching team to see
whether the dataset is of appropriate complexity. Also, include a
**brief** description of the dataset here to help the teaching team
understand your data.

<!-------------------------- Start your work below ---------------------------->

1: **vancouver_trees** 2: **steam_games** 3: **building_permits** 4:
**apt_buildings**

<!----------------------------------------------------------------------------->

1.2 **(6 points)** One way to narrowing down your selection is to
*explore* the datasets. Use your knowledge of dplyr to find out at least
*3* attributes about each of these datasets (an attribute is something
such as number of rows, variables, class type…). The goal here is to
have an idea of *what the data looks like*.

*Hint:* This is one of those times when you should think about the
cleanliness of your analysis. I added a single code chunk for you below,
but do you want to use more than one? Would you like to write more
comments outside of the code chunk?

<!-------------------------- Start your work below ---------------------------->

## 1. First exploration of ‘vancouver_trees’ ————–

``` r
# Dataset structure to get an initial glance of information
glimpse(vancouver_trees)
```

    ## Rows: 146,611
    ## Columns: 20
    ## $ tree_id            <dbl> 149556, 149563, 149579, 149590, 149604, 149616, 149…
    ## $ civic_number       <dbl> 494, 450, 4994, 858, 5032, 585, 4909, 4925, 4969, 7…
    ## $ std_street         <chr> "W 58TH AV", "W 58TH AV", "WINDSOR ST", "E 39TH AV"…
    ## $ genus_name         <chr> "ULMUS", "ZELKOVA", "STYRAX", "FRAXINUS", "ACER", "…
    ## $ species_name       <chr> "AMERICANA", "SERRATA", "JAPONICA", "AMERICANA", "C…
    ## $ cultivar_name      <chr> "BRANDON", NA, NA, "AUTUMN APPLAUSE", NA, "CHANTICL…
    ## $ common_name        <chr> "BRANDON ELM", "JAPANESE ZELKOVA", "JAPANESE SNOWBE…
    ## $ assigned           <chr> "N", "N", "N", "Y", "N", "N", "N", "N", "N", "N", "…
    ## $ root_barrier       <chr> "N", "N", "N", "N", "N", "N", "N", "N", "N", "N", "…
    ## $ plant_area         <chr> "N", "N", "4", "4", "4", "B", "6", "6", "3", "3", "…
    ## $ on_street_block    <dbl> 400, 400, 4900, 800, 5000, 500, 4900, 4900, 4900, 7…
    ## $ on_street          <chr> "W 58TH AV", "W 58TH AV", "WINDSOR ST", "E 39TH AV"…
    ## $ neighbourhood_name <chr> "MARPOLE", "MARPOLE", "KENSINGTON-CEDAR COTTAGE", "…
    ## $ street_side_name   <chr> "EVEN", "EVEN", "EVEN", "EVEN", "EVEN", "ODD", "ODD…
    ## $ height_range_id    <dbl> 2, 4, 3, 4, 2, 2, 3, 3, 2, 2, 2, 5, 3, 2, 2, 2, 2, …
    ## $ diameter           <dbl> 10.00, 10.00, 4.00, 18.00, 9.00, 5.00, 15.00, 14.00…
    ## $ curb               <chr> "N", "N", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "…
    ## $ date_planted       <date> 1999-01-13, 1996-05-31, 1993-11-22, 1996-04-29, 19…
    ## $ longitude          <dbl> -123.1161, -123.1147, -123.0846, -123.0870, -123.08…
    ## $ latitude           <dbl> 49.21776, 49.21776, 49.23938, 49.23469, 49.23894, 4…

``` r
# Number and proportion of variables by data type
vancouver_trees %>% 
  summarise(across(everything(), class)) %>% 
  pivot_longer(everything(),
               values_to = "data_type") %>% 
  count(data_type) %>% 
  mutate(prop = percent(n/sum(n), accuracy = 0.1))
```

    ## # A tibble: 3 × 3
    ##   data_type     n prop 
    ##   <chr>     <int> <chr>
    ## 1 Date          1 5.0% 
    ## 2 character    12 60.0%
    ## 3 numeric       7 35.0%

``` r
# Statistics of numeric variables
vancouver_trees %>% 
summarise(across(where(is.numeric), .fns = 
                     list(min = min,
                          median = median,
                          mean = mean,
                          stdev = sd,
                          q25 = (\(., ...) quantile(., 0.25, ...)),
                          q75 = (\(., ...) quantile(., 0.75, ...)),
                          max = max),
                 na.rm = T,
                 .names = "{.col}__{.fn}")) %>% 
  pivot_longer(everything(), 
               names_sep = "__", 
               names_to = c("variable", ".value"))
```

    ## Warning: There was 1 warning in `summarise()`.
    ## ℹ In argument: `across(...)`.
    ## Caused by warning:
    ## ! The `...` argument of `across()` is deprecated as of dplyr 1.1.0.
    ## Supply arguments directly to `.fns` through an anonymous function instead.
    ## 
    ##   # Previously
    ##   across(a:b, mean, na.rm = TRUE)
    ## 
    ##   # Now
    ##   across(a:b, \(x) mean(x, na.rm = TRUE))

    ## # A tibble: 7 × 8
    ##   variable           min   median      mean      stdev     q25      q75      max
    ##   <chr>            <dbl>    <dbl>     <dbl>      <dbl>   <dbl>    <dbl>    <dbl>
    ## 1 tree_id           12   134903   131892.   75457.     65464.  194450.  266203  
    ## 2 civic_number       0     2604     2937.    2058.      1306     4005    17888  
    ## 3 on_street_block    0     2600     2909.    2067.      1300     4000     9900  
    ## 4 height_range_id    0        2        2.63     1.54       1        4       10  
    ## 5 diameter           0        9       11.5      9.21       3.5     16.5    435  
    ## 6 longitude       -123.    -123.    -123.       0.0495  -123.    -123.    -123. 
    ## 7 latitude          49.2     49.2     49.2      0.0211    49.2     49.3     49.3

## 2. First exploration of ‘steam_games’ ————–

``` r
# Dataset structure to get an initial glance of information
glimpse(steam_games)
```

    ## Rows: 40,833
    ## Columns: 21
    ## $ id                       <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14…
    ## $ url                      <chr> "https://store.steampowered.com/app/379720/DO…
    ## $ types                    <chr> "app", "app", "app", "app", "app", "bundle", …
    ## $ name                     <chr> "DOOM", "PLAYERUNKNOWN'S BATTLEGROUNDS", "BAT…
    ## $ desc_snippet             <chr> "Now includes all three premium DLC packs (Un…
    ## $ recent_reviews           <chr> "Very Positive,(554),- 89% of the 554 user re…
    ## $ all_reviews              <chr> "Very Positive,(42,550),- 92% of the 42,550 u…
    ## $ release_date             <chr> "May 12, 2016", "Dec 21, 2017", "Apr 24, 2018…
    ## $ developer                <chr> "id Software", "PUBG Corporation", "Harebrain…
    ## $ publisher                <chr> "Bethesda Softworks,Bethesda Softworks", "PUB…
    ## $ popular_tags             <chr> "FPS,Gore,Action,Demons,Shooter,First-Person,…
    ## $ game_details             <chr> "Single-player,Multi-player,Co-op,Steam Achie…
    ## $ languages                <chr> "English,French,Italian,German,Spanish - Spai…
    ## $ achievements             <dbl> 54, 37, 128, NA, NA, NA, 51, 55, 34, 43, 72, …
    ## $ genre                    <chr> "Action", "Action,Adventure,Massively Multipl…
    ## $ game_description         <chr> "About This Game Developed by id software, th…
    ## $ mature_content           <chr> NA, "Mature Content Description  The develope…
    ## $ minimum_requirements     <chr> "Minimum:,OS:,Windows 7/8.1/10 (64-bit versio…
    ## $ recommended_requirements <chr> "Recommended:,OS:,Windows 7/8.1/10 (64-bit ve…
    ## $ original_price           <dbl> 19.99, 29.99, 39.99, 44.99, 0.00, NA, 59.99, …
    ## $ discount_price           <dbl> 14.99, NA, NA, NA, NA, 35.18, 70.42, 17.58, N…

``` r
# Number and proportion of variables by data type
steam_games %>% 
  summarise(across(everything(), class)) %>% 
  pivot_longer(everything(),
               values_to = "data_type") %>% 
  count(data_type) %>% 
  mutate(prop = percent(n/sum(n), accuracy = 0.1))
```

    ## # A tibble: 2 × 3
    ##   data_type     n prop 
    ##   <chr>     <int> <chr>
    ## 1 character    17 81.0%
    ## 2 numeric       4 19.0%

``` r
# Statistics of numeric variables
steam_games %>% 
summarise(across(where(is.numeric), .fns = 
                     list(min = min,
                          median = median,
                          mean = mean,
                          stdev = sd,
                          q25 = (\(., ...) quantile(., 0.25, ...)),
                          q75 = (\(., ...) quantile(., 0.75, ...)),
                          max = max),
                 na.rm = T,
                 .names = "{.col}__{.fn}")) %>% 
  pivot_longer(everything(), 
               names_sep = "__", 
               names_to = c("variable", ".value"))
```

    ## # A tibble: 4 × 8
    ##   variable         min   median    mean   stdev      q25      q75     max
    ##   <chr>          <dbl>    <dbl>   <dbl>   <dbl>    <dbl>    <dbl>   <dbl>
    ## 1 id                 1 20417    20417   11788.  10209    30625     40833 
    ## 2 achievements       1    21       77.2   449.     12       38      9821 
    ## 3 original_price     0     4.99    53.1  5194.      1.99     9.99 730640 
    ## 4 discount_price     0    20.0     46.8    93.8     8.78    43.9     963.

## 3. First exploration of ‘building_permits’ ————–

``` r
# Dataset structure to get an initial glance of information
glimpse(building_permits)
```

    ## Rows: 20,680
    ## Columns: 14
    ## $ permit_number               <chr> "BP-2016-02248", "BU468090", "DB-2016-0445…
    ## $ issue_date                  <date> 2017-02-01, 2017-02-01, 2017-02-01, 2017-…
    ## $ project_value               <dbl> 0, 0, 35000, 15000, 181178, 0, 15000, 0, 6…
    ## $ type_of_work                <chr> "Salvage and Abatement", "New Building", "…
    ## $ address                     <chr> "4378 W 9TH AVENUE, Vancouver, BC V6R 2C7"…
    ## $ project_description         <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
    ## $ building_contractor         <chr> NA, NA, NA, "Mercury Contracting Ltd", "08…
    ## $ building_contractor_address <chr> NA, NA, NA, "88 W PENDER ST  \r\nUnit 2069…
    ## $ applicant                   <chr> "Raffaele & Associates DBA: Raffaele and A…
    ## $ applicant_address           <chr> "2642 East Hastings\r\nVancouver, BC  V5K …
    ## $ property_use                <chr> "Dwelling Uses", "Dwelling Uses", "Dwellin…
    ## $ specific_use_category       <chr> "One-Family Dwelling", "Multiple Dwelling"…
    ## $ year                        <dbl> 2017, 2017, 2017, 2017, 2017, 2017, 2017, …
    ## $ bi_id                       <dbl> 524, 535, 539, 541, 543, 546, 547, 548, 54…

``` r
# Number and proportion of variables by data type
building_permits %>% 
  summarise(across(everything(), class)) %>% 
  pivot_longer(everything(),
               values_to = "data_type") %>% 
  count(data_type) %>% 
  mutate(prop = percent(n/sum(n), accuracy = 0.1))
```

    ## # A tibble: 3 × 3
    ##   data_type     n prop 
    ##   <chr>     <int> <chr>
    ## 1 Date          1 7.1% 
    ## 2 character    10 71.4%
    ## 3 numeric       3 21.4%

``` r
# Statistics of numeric variables
building_permits %>% 
summarise(across(where(is.numeric), .fns = 
                     list(min = min,
                          median = median,
                          mean = mean,
                          stdev = sd,
                          q25 = (\(., ...) quantile(., 0.25, ...)),
                          q75 = (\(., ...) quantile(., 0.75, ...)),
                          max = max),
                 na.rm = T,
                 .names = "{.col}__{.fn}")) %>% 
  pivot_longer(everything(), 
               names_sep = "__", 
               names_to = c("variable", ".value"))
```

    ## # A tibble: 3 × 8
    ##   variable        min median    mean       stdev    q25     q75       max
    ##   <chr>         <dbl>  <dbl>   <dbl>       <dbl>  <dbl>   <dbl>     <dbl>
    ## 1 project_value     0 48000  609166. 8101389.    10739  217791. 807185500
    ## 2 year           2017  2018    2018.       0.947  2017    2019       2020
    ## 3 bi_id             1 10340.  10340.    5970.     5171.  15510.     20680

## 4. First exploration of ‘apt_buildings’ ————–

``` r
# Dataset structure to get an initial glance of information
glimpse(apt_buildings)
```

    ## Rows: 3,455
    ## Columns: 37
    ## $ id                               <dbl> 10359, 10360, 10361, 10362, 10363, 10…
    ## $ air_conditioning                 <chr> "NONE", "NONE", "NONE", "NONE", "NONE…
    ## $ amenities                        <chr> "Outdoor rec facilities", "Outdoor po…
    ## $ balconies                        <chr> "YES", "YES", "YES", "YES", "NO", "NO…
    ## $ barrier_free_accessibilty_entr   <chr> "YES", "NO", "NO", "YES", "NO", "NO",…
    ## $ bike_parking                     <chr> "0 indoor parking spots and 10 outdoo…
    ## $ exterior_fire_escape             <chr> "NO", "NO", "NO", "YES", "NO", NA, "N…
    ## $ fire_alarm                       <chr> "YES", "YES", "YES", "YES", "YES", "Y…
    ## $ garbage_chutes                   <chr> "YES", "YES", "NO", "NO", "NO", "NO",…
    ## $ heating_type                     <chr> "HOT WATER", "HOT WATER", "HOT WATER"…
    ## $ intercom                         <chr> "YES", "YES", "YES", "YES", "YES", "Y…
    ## $ laundry_room                     <chr> "YES", "YES", "YES", "YES", "YES", "Y…
    ## $ locker_or_storage_room           <chr> "NO", "YES", "YES", "YES", "NO", "YES…
    ## $ no_of_elevators                  <dbl> 3, 3, 0, 1, 0, 0, 0, 2, 4, 2, 0, 2, 2…
    ## $ parking_type                     <chr> "Underground Garage , Garage accessib…
    ## $ pets_allowed                     <chr> "YES", "YES", "YES", "YES", "YES", "Y…
    ## $ prop_management_company_name     <chr> NA, "SCHICKEDANZ BROS. PROPERTIES", N…
    ## $ property_type                    <chr> "PRIVATE", "PRIVATE", "PRIVATE", "PRI…
    ## $ rsn                              <dbl> 4154812, 4154815, 4155295, 4155309, 4…
    ## $ separate_gas_meters              <chr> "NO", "NO", "NO", "NO", "NO", "NO", "…
    ## $ separate_hydro_meters            <chr> "YES", "YES", "YES", "YES", "YES", "Y…
    ## $ separate_water_meters            <chr> "NO", "NO", "NO", "NO", "NO", "NO", "…
    ## $ site_address                     <chr> "65  FOREST MANOR RD", "70  CLIPPER R…
    ## $ sprinkler_system                 <chr> "YES", "YES", "NO", "YES", "NO", "NO"…
    ## $ visitor_parking                  <chr> "PAID", "FREE", "UNAVAILABLE", "UNAVA…
    ## $ ward                             <chr> "17", "17", "03", "03", "02", "02", "…
    ## $ window_type                      <chr> "DOUBLE PANE", "DOUBLE PANE", "DOUBLE…
    ## $ year_built                       <dbl> 1967, 1970, 1927, 1959, 1943, 1952, 1…
    ## $ year_registered                  <dbl> 2017, 2017, 2017, 2017, 2017, NA, 201…
    ## $ no_of_storeys                    <dbl> 17, 14, 4, 5, 4, 4, 4, 7, 32, 4, 4, 7…
    ## $ emergency_power                  <chr> "NO", "YES", "NO", "NO", "NO", "NO", …
    ## $ `non-smoking_building`           <chr> "YES", "NO", "YES", "YES", "YES", "NO…
    ## $ no_of_units                      <dbl> 218, 206, 34, 42, 25, 34, 14, 105, 57…
    ## $ no_of_accessible_parking_spaces  <dbl> 8, 10, 20, 42, 12, 0, 5, 1, 1, 6, 12,…
    ## $ facilities_available             <chr> "Recycling bins", "Green Bin / Organi…
    ## $ cooling_room                     <chr> "NO", "NO", "NO", "NO", "NO", "NO", "…
    ## $ no_barrier_free_accessible_units <dbl> 2, 0, 0, 42, 0, NA, 14, 0, 0, 1, 25, …

``` r
# Number and proportion of variables by data type
apt_buildings %>% 
  summarise(across(everything(), class)) %>% 
  pivot_longer(everything(),
               values_to = "data_type") %>% 
  count(data_type) %>% 
  mutate(prop = percent(n/sum(n), accuracy = 0.1))
```

    ## # A tibble: 2 × 3
    ##   data_type     n prop 
    ##   <chr>     <int> <chr>
    ## 1 character    28 75.7%
    ## 2 numeric       9 24.3%

``` r
# Statistics of numeric variables
apt_buildings %>% 
summarise(across(where(is.numeric), .fns = 
                     list(min = min,
                          median = median,
                          mean = mean,
                          stdev = sd,
                          q25 = (\(., ...) quantile(., 0.25, ...)),
                          q75 = (\(., ...) quantile(., 0.75, ...)),
                          max = max),
                 na.rm = T,
                 .names = "{.col}__{.fn}")) %>% 
  pivot_longer(everything(), 
               names_sep = "__", 
               names_to = c("variable", ".value"))
```

    ## # A tibble: 9 × 8
    ##   variable                        min median   mean   stdev    q25    q75    max
    ##   <chr>                         <dbl>  <dbl>  <dbl>   <dbl>  <dbl>  <dbl>  <dbl>
    ## 1 id                           1.04e4 1.21e4 1.21e4 9.98e+2 1.12e4 1.29e4 1.38e4
    ## 2 no_of_elevators              0      1   e0 1.21e0 1.31e+0 0      2   e0 3.2 e1
    ## 3 rsn                          4.15e6 4.15e6 4.17e6 5.20e+4 4.15e6 4.16e6 4.72e6
    ## 4 year_built                   1.81e3 1.96e3 1.96e3 1.91e+1 1.95e3 1.97e3 2.02e3
    ## 5 year_registered              2.02e3 2.02e3 2.02e3 4.21e-1 2.02e3 2.02e3 2.02e3
    ## 6 no_of_storeys                0      5   e0 7.74e0 6.24e+0 3   e0 1   e1 5.1 e1
    ## 7 no_of_units                  0      5.2 e1 9.11e1 1.17e+2 2.5 e1 1.24e2 4.11e3
    ## 8 no_of_accessible_parking_sp… 0      1   e0 6.56e0 1.66e+1 0      5   e0 3.4 e2
    ## 9 no_barrier_free_accessible_… 0      0      9.41e0 3.96e+1 0      1   e0 4.74e2

<!----------------------------------------------------------------------------->

1.3 **(1 point)** Now that you’ve explored the 4 datasets that you were
initially most interested in, let’s narrow it down to 1. What lead you
to choose this one? Briefly explain your choice below.

<!-------------------------- Start your work below ---------------------------->

For this project, I’ve selected the **vancouver_trees** dataset. Upon
examining its variables and overall structure, I became curious about
the variation in grove structure across different neighborhoods. I
started pondering questions like: What’s the tree count per
neighborhood? How does the species composition differ in each area? This
led me to delve deeper into this topic.
<!----------------------------------------------------------------------------->

1.4 **(2 points)** Time for a final decision! Going back to the
beginning, it’s important to have an *end goal* in mind. For example, if
I had chosen the `titanic` dataset for my project, I might’ve wanted to
explore the relationship between survival and other variables. Try to
think of 1 research question that you would want to answer with your
dataset. Note it down below.

<!-------------------------- Start your work below ---------------------------->

My research question for this project is: What are the primary
characteristics of the forest ecosystem in each neighborhood?
<!----------------------------------------------------------------------------->

# Important note

Read Tasks 2 and 3 *fully* before starting to complete either of them.
Probably also a good point to grab a coffee to get ready for the fun
part!

This project is semi-guided, but meant to be *independent*. For this
reason, you will complete tasks 2 and 3 below (under the **START HERE**
mark) as if you were writing your own exploratory data analysis report,
and this guidance never existed! Feel free to add a brief introduction
section to your project, format the document with markdown syntax as you
deem appropriate, and structure the analysis as you deem appropriate. If
you feel lost, you can find a sample data analysis
[here](https://www.kaggle.com/headsortails/tidy-titarnic) to have a
better idea. However, bear in mind that it is **just an example** and
you will not be required to have that level of complexity in your
project.

# Task 2: Exploring your dataset

If we rewind and go back to the learning objectives, you’ll see that by
the end of this deliverable, you should have formulated *4* research
questions about your data that you may want to answer during your
project. However, it may be handy to do some more exploration on your
dataset of choice before creating these questions - by looking at the
data, you may get more ideas. **Before you start this task, read all
instructions carefully until you reach START HERE under Task 3**.

2.1 **(12 points)** Complete *4 out of the following 8 exercises* to
dive deeper into your data. All datasets are different and therefore,
not all of these tasks may make sense for your data - which is why you
should only answer *4*.

Make sure that you’re using dplyr and ggplot2 rather than base R for
this task. Outside of this project, you may find that you prefer using
base R functions for certain tasks, and that’s just fine! But part of
this project is for you to practice the tools we learned in class, which
is dplyr and ggplot2.

1.  Plot the distribution of a numeric variable.
2.  Create a new variable based on other variables in your data (only if
    it makes sense)
3.  Investigate how many missing values there are per variable. Can you
    find a way to plot this?
4.  Explore the relationship between 2 variables in a plot.
5.  Filter observations in your data according to your own criteria.
    Think of what you’d like to explore - again, if this was the
    `titanic` dataset, I may want to narrow my search down to passengers
    born in a particular year…
6.  Use a boxplot to look at the frequency of different observations
    within a single variable. You can do this for more than one variable
    if you wish!
7.  Make a new tibble with a subset of your data, with variables and
    observations that you are interested in exploring.
8.  Use a density plot to explore any of your variables (that are
    suitable for this type of plot).

2.2 **(4 points)** For each of the 4 exercises that you complete,
provide a *brief explanation* of why you chose that exercise in relation
to your data (in other words, why does it make sense to do that?), and
sufficient comments for a reader to understand your reasoning and code.

<!-------------------------- Start your work below ---------------------------->

# Exploring Street Trees in Vancouver’s Neighborhoods

Vancouver is known for its deep-rooted connection with nature, but this
relationship’s specific details and extent need to be more widely
understood. That’s why this project sets out to delve into Vancouver’s
trees data sourced from the City’s Open Data Portal. To accomplish this,
the analysis is broken down into four sections, each dedicated to
exploring an aspect of the trees in Vancouver.

### Missing Values

Upon inspecting the initial rows, it’s evident that there are some
missing values. However, the full extent of this missing data is yet
unknown. To gain a better understanding of this dataset, the first step
is to **visualize the missing values by variable**. This information can
be represented using a barplot, where each variable is depicted as a
separate bar.

``` r
vancouver_trees %>% 
  summarise_all(function(x){sum(ifelse(is.na(x), 1, 0))}) %>% # Counting NA's
  pivot_longer(everything(), # Pivoting columnes to make them rows
               names_to = "variable",
               values_to = "missing_values") %>% 
  ggplot(aes(x = reorder(variable, # Starting barplot
                         missing_values),
             y = missing_values)) +
  coord_flip() +
  geom_col(fill = "#006D77") + 
  scale_y_continuous(labels = comma,
                     expand = expansion(mult = c(0, 0.2))) +
  labs(title = "Missing Values by Variable",
       x = "Variable",
       y = "Number of missing values",
       caption = "Source: The City of Vancouver's Open Data Portal.") +
  mi_tema() 
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

### Tree Density Comparison

When examining the tree population across Vancouver’s neighborhoods, a
straightforward approach might be to display the raw count in each area.
However, this method can be misleading due to the different sizes of
neighborhoods. Therefore, this section focuses on the density of trees
per city block in each neighborhoods. Below, you will find the code that
generates a **density plot** for this purpose (see Exercise 8).

``` r
vancouver_trees %>% 
  count(neighbourhood_name,
        on_street, on_street_block) %>%  # Counting trees by block
  ggplot(aes(x = n, # Ploting density
             y = reorder(str_to_title(neighbourhood_name),
                         -n))) +
  geom_density_ridges(quantile_lines = T, 
                      fill = "#006D77",
                      alpha = 0.5,
                      scale = 1.2,
                      quantile_fun = mean) + 
  labs(title = "Density distribution of trees by Neighborhoods",
       x = "Number of trees by block",
       y = element_blank(),
       caption = "Source: The City of Vancouver's Open Data Portal.") +
  scale_y_discrete(expand = expand_scale(mult = c(0.02, 0.1))) +
  xlim(0, 50) +
  mi_tema() 
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

### Life Span of Trees

Another crucial aspect of trees is their age. Although the dataset
doesn’t directly provide this information, it can be estimated based on
the planting date. Therefore, the following code chunk introduces a new
variable that indicates the age of each tree.

``` r
vancouver_trees <- vancouver_trees %>% 
  mutate(age = as.numeric((today() - date_planted)/365)) # Days since the tree was planted divided by the number of days 
```

### Diameter vs. Age

There is often a **relation between a tree’s diameter and its age**. To
investigate this relationship, the following scatterplot compares the
diameter and age of trees. This plot is particularly effective for this
purpose as it enables us to quickly identify patterns.

``` r
vancouver_trees %>%
  mutate(species_recode = ifelse(n() > 5000,
                                 str_to_title(species_name),
                                 "Others"), # Recoding species with less amount
         .by = species_name) %>%  
  ggplot(aes(x = age, # Creating scatterplot
             y = diameter)) +
  geom_point(aes(color = species_recode),
             size = 0.5,
             alpha = 0.1) +
  scale_y_log10(expand = expand_scale(mult = c(0.02, 0.1))) +
  labs(title = "Relationship between tree's diameter and its age",
       x = "Age",
       y = "Diameter (inches)",
       color = "Main species",
       caption = "Source: The City of Vancouver's Open Data Portal.") +
  guides(color = guide_legend(override.aes = list(size = 2,
                                                  alpha = 0.8))) +
  mi_tema() 
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

<!----------------------------------------------------------------------------->

# Task 3: Choose research questions

**(4 points)** So far, you have chosen a dataset and gotten familiar
with it through exploring the data. You have also brainstormed one
research question that interested you (Task 1.4). Now it’s time to pick
4 research questions that you would like to explore in Milestone 2!
Write the 4 questions and any additional comments below.

<!--- *****START HERE***** --->

Derived from the main research question (Task 1.4), the selected
research questions are as follows:

1.  What is the most common species of tree in each neighborhood?

2.  What is the range of tree heights and how are diameters distributed
    across neighborhoods?

3.  How many trees have root barriers installed, and what is the
    distribution between neighborhoods?

4.  How many trees were planted in each decade, and how does this vary
    across neighborhoods?

<!----------------------------->

# Overall reproducibility/Cleanliness/Coherence Checklist

## Coherence (0.5 points)

The document should read sensibly from top to bottom, with no major
continuity errors. An example of a major continuity error is having a
data set listed for Task 3 that is not part of one of the data sets
listed in Task 1.

## Error-free code (3 points)

For full marks, all code in the document should run without error. 1
point deduction if most code runs without error, and 2 points deduction
if more than 50% of the code throws an error.

## Main README (1 point)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

- In a sentence or two, explains what this repository is, so that
  future-you or someone else stumbling on your repository can be
  oriented to the repository.
- In a sentence or two (or more??), briefly explains how to engage with
  the repository. You can assume the person reading knows the material
  from STAT 545A. Basically, if a visitor to your repository wants to
  explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## Output (1 point)

All output is readable, recent and relevant:

- All Rmd files have been `knit`ted to their output md files.
- All knitted md files are viewable without errors on Github. Examples
  of errors: Missing plots, “Sorry about that, but we can’t show files
  that are this big right now” messages, error messages from broken R
  code
- All of these output files are up-to-date – that is, they haven’t
  fallen behind after the source (Rmd) files have been updated.
- There should be no relic output files. For example, if you were
  knitting an Rmd to html, but then changed the output to be only a
  markdown file, then the html file is a relic and should be deleted.

(0.5 point deduction if any of the above criteria are not met. 1 point
deduction if most or all of the above criteria are not met.)

Our recommendation: right before submission, delete all output files,
and re-knit each milestone’s Rmd file, so that everything is up to date
and relevant. Then, after your final commit and push to Github, CHECK on
Github to make sure that everything looks the way you intended!

## Tagged release (0.5 points)

You’ve tagged a release for Milestone 1.

### Attribution

Thanks to Icíar Fernández Boyano for mostly putting this together, and
Vincenzo Coia for launching.
