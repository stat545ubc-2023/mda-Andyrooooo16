*To complete this milestone, you can either edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to the rest of your mini data analysis project!

In Milestone 1, you explored your data. and came up with research
questions. This time, we will finish up our mini data analysis and
obtain results for your data by:

-   Making summary tables and graphs
-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

We will also explore more in depth the concept of *tidy data.*

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 50 points: 45 for your analysis, and
5 for overall reproducibility, cleanliness, and coherence of the Github
submission.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

-   Understand what *tidy* data is, and how to create it using `tidyr`.
-   Generate a reproducible and clear report using R Markdown.
-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD

======= &gt;&gt;&gt;&gt;&gt;&gt;&gt;
9c5f7b898f7c2e6a4115ab037fef9b08c03b4a97

    library(datateachr) # <- might contain the data you picked!
    library(dplyr)
    library(ggplot2)
    library(tidyverse)

    library(here)

    ## here() starts at C:/Users/andre/Documents/mda-Andyrooooo16

    library(datateachr) 
    library(dplyr)
    library(ggplot2)
    library(tidyverse)
    library(broom)

# Task 1: Process and summarize your data

From milestone 1, you should have an idea of the basic structure of your
dataset (e.g. number of rows and columns, class types, etc.). Here, we
will start investigating your data more in-depth using various data
manipulation functions.

### 1.1 (1 point)

First, write out the 4 research questions you defined in milestone 1
were. This will guide your work through milestone 2:

<!-------------------------- Start your work below ---------------------------->

**1. What is the relationship between the age of the tree and plant
area?** *(This question used to be “What is the relationship between
density of trees in a neighbourhood and the age of the trees planted?”,
however, upon further consideration, I did not believe there would be
tangible correlation between density of tree clusters and age. Instead I
wish to explore growth trends of trees based on species by first
determining average diameter based on age.)*

**2. What is the distribution of different species of “Spectacle” trees
throughout Vancouver? (“Spectacle” trees is an subjective term that will
be defined as species of that people visit as an attraction)**

**3. Which neighbourhood in Vancouver contain the most amounts of
“Spectacle trees”?** *(This question used to be”Which streets in
Vancouver have the most amount of trees with the largest plant area? Is
there a relationship between plant area and how old a tree is?“,
however, upon further evaluation I believe this question to be
distracted in scope. I wanted to narrow down the question in pursuit of
finding the best places in Vancouver to view”Spectacle trees” in fall
and spring respectively.*

**4. What is the relationship between tree diameter and age of tree?**
*(This question used to be ” What is the relationship between species
diversity and longitude/latitude? Is there a specific species that
dominates a certain area of vancouver or is the distribution fairly
equal?“, however, upon further review this quesiton can be answered
through my earlier inquiries so I wanted to gain more insight into
growth patterns instead*
<!----------------------------------------------------------------------------->

Here, we will investigate your data using various data manipulation and
graphing functions.

### 1.2 (8 points)

Now, for each of your four research questions, choose one task from
options 1-4 (summarizing), and one other task from 4-8 (graphing). You
should have 2 tasks done for each research question (8 total). Make sure
it makes sense to do them! (e.g. don’t use a numerical variables for a
task that needs a categorical variable.). Comment on why each task helps
(or doesn’t!) answer the corresponding research question.

Ensure that the output of each operation is printed!

Also make sure that you’re using dplyr and ggplot2 rather than base R.
Outside of this project, you may find that you prefer using base R
functions for certain tasks, and that’s just fine! But part of this
project is for you to practice the tools we learned in class, which is
dplyr and ggplot2.

**Summarizing:**

1.  Compute the *range*, *mean*, and *two other summary statistics* of
    **one numerical variable** across the groups of **one categorical
    variable** from your data.
2.  Compute the number of observations for at least one of your
    categorical variables. Do not use the function `table()`!
3.  Create a categorical variable with 3 or more groups from an existing
    numerical variable. You can use this new variable in the other
    tasks! *An example: age in years into “child, teen, adult, senior”.*
4.  Compute the proportion and counts in each category of one
    categorical variable across the groups of another categorical
    variable from your data. Do not use the function `table()`!

**Graphing:**

1.  Create a graph of your choosing, make one of the axes logarithmic,
    and format the axes labels so that they are “pretty” or easier to
    read.
2.  Make a graph where it makes sense to customize the alpha
    transparency.

Using variables and/or tables you made in one of the “Summarizing”
tasks:

1.  Create a graph that has at least two geom layers.
2.  Create 3 histograms, with each histogram having different sized
    bins. Pick the “best” one and explain why it is the best.

Make sure it’s clear what research question you are doing each operation
for!

<!------------------------- Start your work below ----------------------------->

    # I am redefining my custom data set here because I had issues linking my first MDA file data set to this one. I hope this is okay :( 

    vancouver_trees$Year_Column <- format(vancouver_trees$date_planted, "%Y") 

    vancouver_trees_age <- vancouver_trees %>%
      mutate(Year_Column = as.numeric(format(date_planted, "%Y")),
             tree_age = 2023 - Year_Column) 

    print(vancouver_trees_age)

    ## # A tibble: 146,611 × 22
    ##    tree_id civic_number std_street    genus_name species_name cultivar_name  
    ##      <dbl>        <dbl> <chr>         <chr>      <chr>        <chr>          
    ##  1  149556          494 W 58TH AV     ULMUS      AMERICANA    BRANDON        
    ##  2  149563          450 W 58TH AV     ZELKOVA    SERRATA      <NA>           
    ##  3  149579         4994 WINDSOR ST    STYRAX     JAPONICA     <NA>           
    ##  4  149590          858 E 39TH AV     FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ##  5  149604         5032 WINDSOR ST    ACER       CAMPESTRE    <NA>           
    ##  6  149616          585 W 61ST AV     PYRUS      CALLERYANA   CHANTICLEER    
    ##  7  149617         4909 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ##  8  149618         4925 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ##  9  149619         4969 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ## 10  149625          720 E 39TH AV     FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ## # ℹ 146,601 more rows
    ## # ℹ 16 more variables: common_name <chr>, assigned <chr>, root_barrier <chr>,
    ## #   plant_area <chr>, on_street_block <dbl>, on_street <chr>,
    ## #   neighbourhood_name <chr>, street_side_name <chr>, height_range_id <dbl>,
    ## #   diameter <dbl>, curb <chr>, date_planted <date>, longitude <dbl>,
    ## #   latitude <dbl>, Year_Column <dbl>, tree_age <dbl>

### What is the relationship between the age of the tree and the tree diameter?

**Compute the *range*, *mean*, and *two other summary statistics* of one
numerical variable across the groups of one categorical variable from
your data.**

    tree_age_stats <- vancouver_trees_age %>%
      filter(!is.na(tree_age)) %>%
      summarize(
        range_tree_age = max(tree_age) - min(tree_age),
        average_tree_age = mean(tree_age), 
        median_tree_age = median(tree_age), 
        sd_tree_age = sd(tree_age)
      )

    # Print the summary statistics
    print(tree_age_stats)

    ## # A tibble: 1 × 4
    ##   range_tree_age average_tree_age median_tree_age sd_tree_age
    ##            <dbl>            <dbl>           <dbl>       <dbl>
    ## 1             30             19.1              19        7.44

**8. Create a graph that has at least two geom layers.**

    filtered_data <- na.omit(vancouver_trees_age[, c("plant_area", "tree_age", "diameter")])

    ggplot(data = filtered_data, aes(x = plant_area, y = tree_age)) +
      geom_point(aes(size = diameter), alpha = 0.5, color = "darkgreen") +  
      labs(
        title = "Relationship between Plant Area, Tree Age, and Diameter",
        x = "Plant Area",
        y = "Tree Age"
      ) +
      theme_minimal() +
      theme(axis.text.x = element_text(angle = 90, vjust = 0.5))  

![](MDA-2-Andrew_files/figure-markdown_strict/unnamed-chunk-5-1.png)

### What is the distribution of different species of “Spectacle” trees throughout Vancouver? (“Spectacle” trees is an subjective term that will be defined as species of that people visit as an attraction)

**2.Compute the number of observations for at least one of your
categorical variables. Do not use the function `table()`!**

    species_count <- vancouver_trees_age %>%
      group_by(species_name) %>%
      summarise(Count = n())

    print(species_count)

    ## # A tibble: 283 × 2
    ##    species_name   Count
    ##    <chr>          <int>
    ##  1 ABIES            139
    ##  2 ACERIFOLIA   X  1724
    ##  3 ACUMINATA          7
    ##  4 ACUTISSIMA       526
    ##  5 AILANTHIFOLIA      5
    ##  6 ALBA              26
    ##  7 ALBA-SINENSIS      3
    ##  8 ALNIFOLIA        274
    ##  9 ALPINUM            1
    ## 10 ALTISSIMA          4
    ## # ℹ 273 more rows

**7. Make a graph where it makes sense to customize the alpha
transparency.**

    filtered_data <- vancouver_trees_age %>%
      filter(genus_name %in% c("PRUNUS", "CORNUS", "ACER", "ABIES")) %>%
      na.omit()

    ggplot(filtered_data, aes(x = longitude, y = latitude, fill = genus_name)) +
      geom_point(alpha = 1.0, shape = 21) +
      stat_density_2d(geom = "tile", contour = TRUE, alpha = 0.2) +
      scale_fill_manual(values = c("PRUNUS" = "pink", "CORNUS" = "hotpink", "ACER" = "orange", "ABIES" = "yellow")) +
      labs(
        title = "Distribution of Cherry Blossoms and Maple Trees in Vancouver",
        x = "Longitude",
        y = "Latitude"
      ) +
      theme_minimal()

![](MDA-2-Andrew_files/figure-markdown_strict/unnamed-chunk-7-1.png)

*Supplementary calculation to find Maple genus. We find that “ACER” and
“ABIES” are out two genus’ of interest.*

    search_string <- 'maple'

    matching_rows <- grep(search_string, vancouver_trees_age$common_name, ignore.case = TRUE)

    unique_values <- unique(vancouver_trees_age$common_name[matching_rows])

    associated_values_list <- list()

    for (val in unique_values) {
      associated_values_list[[val]] <- unique(vancouver_trees_age$genus_name[matching_rows[vancouver_trees_age$common_name[matching_rows] == val]])
    }

    result_trees <- data.frame(common_name = names(associated_values_list), genus_name = unlist(associated_values_list))

    print(result_trees)

    ##                                                   common_name genus_name
    ## HEDGE MAPLE                                       HEDGE MAPLE       ACER
    ## COLUMNAR NORWAY MAPLE                   COLUMNAR NORWAY MAPLE       ACER
    ## RED MAPLE                                           RED MAPLE       ACER
    ## MAPLE SPECIES                                   MAPLE SPECIES       ACER
    ## NORWAY MAPLE                                     NORWAY MAPLE       ACER
    ## FREEMAN'S S.S. MAPLE                     FREEMAN'S S.S. MAPLE       ACER
    ## KARPICK RED MAPLE                           KARPICK RED MAPLE       ACER
    ## SILVER VARIEGATED NORWAY MAPLE SILVER VARIEGATED NORWAY MAPLE       ACER
    ## NORWEGIAN SUNSET MAPLE                 NORWEGIAN SUNSET MAPLE       ACER
    ## PAPERBARK MAPLE                               PAPERBARK MAPLE       ACER
    ## GLOBEHEAD NORWAY MAPLE                 GLOBEHEAD NORWAY MAPLE       ACER
    ## GREEN MOUNTAIN NORWAY MAPLE       GREEN MOUNTAIN NORWAY MAPLE       ACER
    ## JAPANESE MAPLE                                 JAPANESE MAPLE       ACER
    ## BOWHALL RED MAPLE                           BOWHALL RED MAPLE       ACER
    ## BIGLEAF MAPLE                                   BIGLEAF MAPLE       ACER
    ## DEBORAH NORWAY MAPLE                     DEBORAH NORWAY MAPLE       ACER
    ## AUTUMN FLAME RED MAPLE                 AUTUMN FLAME RED MAPLE       ACER
    ## HARVEST ORANGE JPN MAPLE             HARVEST ORANGE JPN MAPLE      ABIES
    ## PACIFIC SUNSET MAPLE                     PACIFIC SUNSET MAPLE       ACER
    ## AUTUMN BLAZE RED MAPLE                 AUTUMN BLAZE RED MAPLE       ACER
    ## RED CAUCASIAN MAPLE                       RED CAUCASIAN MAPLE       ACER
    ## SCHWEDLER NORWAY MAPLE                 SCHWEDLER NORWAY MAPLE       ACER
    ## ARMSTRONG RED MAPLE                       ARMSTRONG RED MAPLE       ACER
    ## OCTOBER GLORY RED MAPLE               OCTOBER GLORY RED MAPLE       ACER
    ## OSAKAZUKI JAPANESE MAPLE             OSAKAZUKI JAPANESE MAPLE       ACER
    ## DOUGLAS MAPLE                                   DOUGLAS MAPLE       ACER
    ## SUPERFORM NORWAY MAPLE                 SUPERFORM NORWAY MAPLE       ACER
    ## QUEEN ELIZABETH MAPLE                   QUEEN ELIZABETH MAPLE       ACER
    ## GREEN COLUMN BLACK MAPLE             GREEN COLUMN BLACK MAPLE       ACER
    ## CAUCASIAN MAPLE                               CAUCASIAN MAPLE       ACER
    ## EMERALD QUEEN NORWAY MAPLE         EMERALD QUEEN NORWAY MAPLE       ACER
    ## FAIRVIEW NORWAY MAPLE                   FAIRVIEW NORWAY MAPLE       ACER
    ## CRIMSON KING NORWAY MAPLE           CRIMSON KING NORWAY MAPLE       ACER
    ## PURPLE LEAF SYCAMORE MAPLE         PURPLE LEAF SYCAMORE MAPLE       ACER
    ## PRINCETON GOLD MAPLE                     PRINCETON GOLD MAPLE       ACER
    ## BRANDYWINE RED MAPLE                     BRANDYWINE RED MAPLE       ACER
    ## SILVER MAPLE                                     SILVER MAPLE       ACER
    ## SYCAMORE MAPLE                                 SYCAMORE MAPLE       ACER
    ## VARIEGATED SYCAMORE MAPLE           VARIEGATED SYCAMORE MAPLE       ACER
    ## RED SUNSET RED MAPLE                     RED SUNSET RED MAPLE       ACER
    ## TATARIAN MAPLE                                 TATARIAN MAPLE       ACER
    ## SNAKEBARK MAPLE                               SNAKEBARK MAPLE       ACER
    ## AMUR MAPLE                                         AMUR MAPLE       ACER
    ## RED JAPANESE MAPLE                         RED JAPANESE MAPLE       ACER
    ## PURPLE NORWAY MAPLE                       PURPLE NORWAY MAPLE       ACER
    ## CRIMSON SENTRY NORWAY MAPLE       CRIMSON SENTRY NORWAY MAPLE       ACER
    ## ROYAL RED NORWAY MAPLE                 ROYAL RED NORWAY MAPLE       ACER
    ## FULLMOON MAPLE                                 FULLMOON MAPLE       ACER
    ## NORTHWOOD RED MAPLE                       NORTHWOOD RED MAPLE       ACER
    ## MORGAN RED MAPLE                             MORGAN RED MAPLE       ACER
    ## VINE MAPLE                                         VINE MAPLE       ACER
    ## SUGAR MAPLE                                       SUGAR MAPLE       ACER
    ## THREADLEAF JAPANESE MAPLE           THREADLEAF JAPANESE MAPLE       ACER
    ## BURGANDY LACE JAPANESE  MAPLE   BURGANDY LACE JAPANESE  MAPLE       ACER
    ## SHOJO JAPANESE MAPLE                     SHOJO JAPANESE MAPLE       ACER
    ## EVELYN HEDGE MAPLE                         EVELYN HEDGE MAPLE       ACER
    ## CONQUEST MAPLE                                 CONQUEST MAPLE       ACER
    ## RED SHINE MAPLE                               RED SHINE MAPLE       ACER
    ## KOTO NO IKO JAPANESE MAPLE         KOTO NO IKO JAPANESE MAPLE       ACER
    ## BLOODGOOD JAPANESE MAPLE             BLOODGOOD JAPANESE MAPLE       ACER
    ## PANACEK MAPLE                                   PANACEK MAPLE       ACER
    ## KOREAN MAPLE                                     KOREAN MAPLE       ACER
    ## POINTED LEAF MAPLE                         POINTED LEAF MAPLE       ACER
    ## GOLDEN CAUCASIAN MAPLE                 GOLDEN CAUCASIAN MAPLE       ACER
    ## TAIJA JAPANESE MAPLE                     TAIJA JAPANESE MAPLE       ACER
    ## QUEEN ELIZABETH NORWAY MAPLE     QUEEN ELIZABETH NORWAY MAPLE       ACER
    ## FAASSEN'S BLACK NORWAY MAPLE     FAASSEN'S BLACK NORWAY MAPLE       ACER
    ## ELWOOD NORWAY MAPLE                       ELWOOD NORWAY MAPLE       ACER
    ## GREENLACE NORWAY MAPLE                 GREENLACE NORWAY MAPLE       ACER
    ## PERE DAVIDS MAPLE                           PERE DAVIDS MAPLE       ACER
    ## CRIMSON SUNSET MAPLE                     CRIMSON SUNSET MAPLE       ACER
    ## CUTLEAF SILVER MAPLE                     CUTLEAF SILVER MAPLE       ACER
    ## BLACK MAPLE                                       BLACK MAPLE       ACER
    ## HOT WINGS MAPLE                               HOT WINGS MAPLE       ACER
    ## SILVER QUEEN MAPLE                         SILVER QUEEN MAPLE       ACER
    ## IVY-LEAVED MAPLE                             IVY-LEAVED MAPLE       ACER
    ## ALMIRA NORWAY MAPLE                       ALMIRA NORWAY MAPLE       ACER
    ## SCARLET MAPLE FRANK JR                 SCARLET MAPLE FRANK JR       ACER
    ## COLUMNAR RED MAPLE                         COLUMNAR RED MAPLE       ACER
    ## WIER CUTLEAF SILVER MAPLE           WIER CUTLEAF SILVER MAPLE       ACER
    ## STRIPED-BARK MAPLE                         STRIPED-BARK MAPLE       ACER
    ## CRIMSON QUEEN JAPANESE MAPLE     CRIMSON QUEEN JAPANESE MAPLE       ACER
    ## CELEBRATION RED MAPLE                   CELEBRATION RED MAPLE       ACER
    ## GREENLACE JAPANESE MAPLE             GREENLACE JAPANESE MAPLE       ACER
    ## HENRY MAPLE                                       HENRY MAPLE       ACER
    ## SOUTHERN SUGAR MAPLE                     SOUTHERN SUGAR MAPLE       ACER
    ## EASTERN MOUNTAIN MAPLE                 EASTERN MOUNTAIN MAPLE       ACER
    ## PARKWAY MAPLE                                   PARKWAY MAPLE       ACER
    ## RUGGED RIDGE MIYABE MAPLE           RUGGED RIDGE MIYABE MAPLE       ACER
    ## CUTLEAF NORWAY MAPLE                     CUTLEAF NORWAY MAPLE       ACER
    ## HARVEST ORANGE MAPLE                     HARVEST ORANGE MAPLE       ACER
    ## CLEVELAND NORWAY MAPLE                 CLEVELAND NORWAY MAPLE       ACER
    ## SHANTUNG MAPLE                                 SHANTUNG MAPLE       ACER
    ## JADE GREEN NORWAY MAPLE               JADE GREEN NORWAY MAPLE       ACER
    ## EASY STREET NORWAY MAPLE             EASY STREET NORWAY MAPLE       ACER

### Which neighbourhood in Vancouver contain the most amounts of “Spectacle trees”?

**2.Compute the number of observations for at least one of your
categorical variables. Do not use the function `table()`!**

    spectacle_trees <- c("PRUNUS", "CORNUS", "ACER", "ABIES")

    tree_counts_by_genus_and_neighbourhood <- vancouver_trees_age %>%
      filter(genus_name %in% spectacle_trees) %>%  
      group_by(neighbourhood_name, genus_name) %>%      
      summarize(tree_count = n()) %>%          
      ungroup()

    ## `summarise()` has grouped output by 'neighbourhood_name'. You can override
    ## using the `.groups` argument.

    print(tree_counts_by_genus_and_neighbourhood)

    ## # A tibble: 88 × 3
    ##    neighbourhood_name genus_name tree_count
    ##    <chr>              <chr>           <int>
    ##  1 ARBUTUS-RIDGE      ABIES              18
    ##  2 ARBUTUS-RIDGE      ACER              867
    ##  3 ARBUTUS-RIDGE      CORNUS             58
    ##  4 ARBUTUS-RIDGE      PRUNUS           1514
    ##  5 DOWNTOWN           ABIES               1
    ##  6 DOWNTOWN           ACER             2043
    ##  7 DOWNTOWN           CORNUS             15
    ##  8 DOWNTOWN           PRUNUS            171
    ##  9 DUNBAR-SOUTHLANDS  ABIES              10
    ## 10 DUNBAR-SOUTHLANDS  ACER             2464
    ## # ℹ 78 more rows

**8. Create a graph that has at least two geom layers.**

    #First I need to create a new function that tallies the amount of trees in each neighborhood

    neighborhood_counts <- vancouver_trees_age %>%
      count(neighbourhood_name, name = "Total_Trees")

    print(neighborhood_counts)

    ## # A tibble: 22 × 2
    ##    neighbourhood_name       Total_Trees
    ##    <chr>                          <int>
    ##  1 ARBUTUS-RIDGE                   5169
    ##  2 DOWNTOWN                        5159
    ##  3 DUNBAR-SOUTHLANDS               9415
    ##  4 FAIRVIEW                        4002
    ##  5 GRANDVIEW-WOODLAND              6703
    ##  6 HASTINGS-SUNRISE               10547
    ##  7 KENSINGTON-CEDAR COTTAGE       11042
    ##  8 KERRISDALE                      6936
    ##  9 KILLARNEY                       6148
    ## 10 KITSILANO                       8115
    ## # ℹ 12 more rows

    plot <- ggplot(data = neighborhood_counts, aes(x = reorder(neighbourhood_name, -Total_Trees), y = Total_Trees)) +
      geom_bar(stat = "identity", fill = "darkgreen") +
      labs(
        title = "Number of Spectacle Trees in each Vancouver Neighborhood",
        x = "Neighbourhood",
        y = "Total Trees"
      ) +
      theme_minimal() +
      theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
      coord_flip() +
      scale_y_log10()  

    average_age <- filtered_data %>%
      group_by(neighbourhood_name) %>%
      summarise(Average_Age = mean(tree_age, na.rm = TRUE))

    plot + geom_line(data = average_age, aes(x = reorder(neighbourhood_name, -Average_Age), y = Average_Age, group = 1), color = "red") +
      labs(y = "Total Trees / Average Age (x10)")

![](MDA-2-Andrew_files/figure-markdown_strict/unnamed-chunk-11-1.png)

### What is the relationship between tree diameter and age of tree?

**3.Create a categorical variable with 3 or more groups from an existing
numerical variable. You can use this new variable in the other tasks! An
example: age in years into “child, teen, adult, senior”.**

    vancouver_trees_age <- vancouver_trees_age %>%
      mutate(Diameter_string = case_when(
        diameter <= 10 ~ "xsmall_width",
        diameter <= 20 ~ "small_width",
        diameter <= 30 ~ "medium_width",
        TRUE ~ "large_width"
      ))

    print(head(vancouver_trees_age$Diameter_string, 10))

    ##  [1] "xsmall_width" "xsmall_width" "xsmall_width" "small_width"  "xsmall_width"
    ##  [6] "xsmall_width" "small_width"  "small_width"  "small_width"  "xsmall_width"

**7. Make a graph where it makes sense to customize the alpha
transparency.**

    filtered_data <- na.omit(vancouver_trees_age[, c("tree_age", "diameter", "Diameter_string")])

    ggplot(data = filtered_data, aes(x = tree_age, y = diameter, color = Diameter_string)) +
      geom_point(aes(alpha = 0), size = 3) +
      labs(
        title = "Relationship between Tree Diameter and Age",
        x = "Tree Age",
        y = "Tree Diameter"
      ) +
      scale_color_manual(values = c("xsmall_width" = "red", "small_width" = "blue", "medium_width" = "green", "large_width" = "purple")) +
      scale_alpha(range = c(0.1, 1.0))

![](MDA-2-Andrew_files/figure-markdown_strict/unnamed-chunk-13-1.png)

<!----------------------------------------------------------------------------->

### 1.3 (2 points)

Based on the operations that you’ve completed, how much closer are you
to answering your research questions? Think about what aspects of your
research questions remain unclear. Can your research questions be
refined, now that you’ve investigated your data a bit more? Which
research questions are yielding interesting results?

<!------------------------- Write your answer here ---------------------------->

**1. What is the relationship between the age of the tree and plant
area?**

With the graph associated with this question, I am much closer to answer
the research question. I think to clarify the data further, I may need
to insert a trend line to see if there is a actual correlation or
relationship between age of a tree and plant area. I do not believe I
needed a second geom layer showing diameter of trees to answer this
specific question, but it gives greater context regarding my question 4
below.

**2. What is the distribution of different species of “Spectacle” trees
throughout Vancouver? (“Spectacle” trees is an subjective term that will
be defined as species of that people visit as an attraction)**

Firstly, it was helpful to define the specific genus of trees that are
defined as “spectacle trees”. Being able to graph them based on
longitude and latitude with color coding resulted in a very visual
representation of spectacle trees. It seems that there are a lot more
occurence of Maple than Cherry trees which matches my own knowledge
regarding the distribution of these trees. I believe this research
question was answered to the fullest extend and exceeded my own
expectations in terms of results.

**3. Which neighbourhood in Vancouver contain the most amounts of
“Spectacle trees”?**

With the previously defined “spectacle trees” filter, it was a lot
easier for me to graph the total amount of spectacle trees per
neighbourhood. Although my initial inquiry is answered and I have found
Dunbar-Southlands to contain the most amount of spectacle trees overall,
I may try to insert a stacked bar chart in the future to visualize the
distribution of genus amonst the existing tally of spectacle trees.

**4. What is the relationship between tree diameter and age of tree?**

This relationship was a lot easier to find as the two numerical metrics
were already predefined in my reformatted dataset. A curious finding for
me was that on average, trees over 32 years of age had smaller diameters
than those who are in the range of 19-29 years old. Presuming that tree
trunks get thicker each year since another ring grows, this finding was
quite surprising for me.

<!----------------------------------------------------------------------------->

# Task 2: Tidy your data

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

-   Each row is an **observation**
-   Each column is a **variable**
-   Each cell is a **value**

### 2.1 (2 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have &gt;8 variables,
just pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->

**To answer this question, I will be analyzing whether my
vancouver\_trees\_age dataset is clean or not. I will be showing data
below from the first 8 columns since my data set has 24 columns.For the
most part, the data is tidy as it satisfies the aforementioned three
statements defining tidy data. Each column highlights a specific
variable and does not additionally expand any column values. However,
during the data cleaning process, I made a stylistic choice to not omit
outliers that had missing values within a row. Specifically,
“cultivar\_name” column within the first 8 columns includes some NA
values. I chose not to remove these rows because “cultivar\_name” and
the other columns with missing data were not columns I was using in my
analysis. Since the rest of the observations were complete from the rows
containing the missing values, I decided that I could still include them
in the dataset.**

    #Demonstration of first 8 columns

    first_8_columns <- vancouver_trees_age[, 1:8]
    print(first_8_columns)

    ## # A tibble: 146,611 × 8
    ##    tree_id civic_number std_street    genus_name species_name cultivar_name  
    ##      <dbl>        <dbl> <chr>         <chr>      <chr>        <chr>          
    ##  1  149556          494 W 58TH AV     ULMUS      AMERICANA    BRANDON        
    ##  2  149563          450 W 58TH AV     ZELKOVA    SERRATA      <NA>           
    ##  3  149579         4994 WINDSOR ST    STYRAX     JAPONICA     <NA>           
    ##  4  149590          858 E 39TH AV     FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ##  5  149604         5032 WINDSOR ST    ACER       CAMPESTRE    <NA>           
    ##  6  149616          585 W 61ST AV     PYRUS      CALLERYANA   CHANTICLEER    
    ##  7  149617         4909 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ##  8  149618         4925 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ##  9  149619         4969 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ## 10  149625          720 E 39TH AV     FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ## # ℹ 146,601 more rows
    ## # ℹ 2 more variables: common_name <chr>, assigned <chr>

<!----------------------------------------------------------------------------->

### 2.2 (4 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

    #Since I previously categorized my data as tidy in Task 2.1, I will first untidy the data by expanding the column "assigned". The table under Task 2.1 shows the original "before" view. The output table from this function is the "after" view. 

    wide_data <- pivot_wider(
      data = vancouver_trees_age,
      names_from = assigned,
      values_from = assigned
    )

    print(wide_data)

    ## # A tibble: 146,611 × 24
    ##    tree_id civic_number std_street    genus_name species_name cultivar_name  
    ##      <dbl>        <dbl> <chr>         <chr>      <chr>        <chr>          
    ##  1  149556          494 W 58TH AV     ULMUS      AMERICANA    BRANDON        
    ##  2  149563          450 W 58TH AV     ZELKOVA    SERRATA      <NA>           
    ##  3  149579         4994 WINDSOR ST    STYRAX     JAPONICA     <NA>           
    ##  4  149590          858 E 39TH AV     FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ##  5  149604         5032 WINDSOR ST    ACER       CAMPESTRE    <NA>           
    ##  6  149616          585 W 61ST AV     PYRUS      CALLERYANA   CHANTICLEER    
    ##  7  149617         4909 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ##  8  149618         4925 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ##  9  149619         4969 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ## 10  149625          720 E 39TH AV     FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ## # ℹ 146,601 more rows
    ## # ℹ 18 more variables: common_name <chr>, root_barrier <chr>, plant_area <chr>,
    ## #   on_street_block <dbl>, on_street <chr>, neighbourhood_name <chr>,
    ## #   street_side_name <chr>, height_range_id <dbl>, diameter <dbl>, curb <chr>,
    ## #   date_planted <date>, longitude <dbl>, latitude <dbl>, Year_Column <dbl>,
    ## #   tree_age <dbl>, Diameter_string <chr>, N <chr>, Y <chr>

    # The following formula makes my table tidy again. The output looks slightly different from the "before" table from Task 2.1, but that is because the "tree_id" sorting is different. The values from each row of this restpred table remain the same as the "before" table from Task 2.1. 

    wide_data <- wide_data %>%
      mutate(assigned = coalesce(N, Y)) %>%
      select(-N, -Y)

    print(wide_data)

    ## # A tibble: 146,611 × 23
    ##    tree_id civic_number std_street    genus_name species_name cultivar_name  
    ##      <dbl>        <dbl> <chr>         <chr>      <chr>        <chr>          
    ##  1  149556          494 W 58TH AV     ULMUS      AMERICANA    BRANDON        
    ##  2  149563          450 W 58TH AV     ZELKOVA    SERRATA      <NA>           
    ##  3  149579         4994 WINDSOR ST    STYRAX     JAPONICA     <NA>           
    ##  4  149590          858 E 39TH AV     FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ##  5  149604         5032 WINDSOR ST    ACER       CAMPESTRE    <NA>           
    ##  6  149616          585 W 61ST AV     PYRUS      CALLERYANA   CHANTICLEER    
    ##  7  149617         4909 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ##  8  149618         4925 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ##  9  149619         4969 SHERBROOKE ST ACER       PLATANOIDES  COLUMNARE      
    ## 10  149625          720 E 39TH AV     FRAXINUS   AMERICANA    AUTUMN APPLAUSE
    ## # ℹ 146,601 more rows
    ## # ℹ 17 more variables: common_name <chr>, root_barrier <chr>, plant_area <chr>,
    ## #   on_street_block <dbl>, on_street <chr>, neighbourhood_name <chr>,
    ## #   street_side_name <chr>, height_range_id <dbl>, diameter <dbl>, curb <chr>,
    ## #   date_planted <date>, longitude <dbl>, latitude <dbl>, Year_Column <dbl>,
    ## #   tree_age <dbl>, Diameter_string <chr>, assigned <chr>

<!----------------------------------------------------------------------------->

### 2.3 (4 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the remaining tasks:

<!-------------------------- Start your work below ---------------------------->

1.  **Which neighbourhood in Vancouver contain the most amounts of
    “Spectacle trees”?**

2.  **What is the relationship between tree diameter and age of tree?**

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

**For question 1:** I want to further explore the genus of spectacle
trees in each neighbourhood. This can be done by aggregating a count of
the trees of each genus in each neighbourhood, allowing me to
superimpose the data on top of each other in a stacked bar chart.

**For question 2:**Now that I can create a scatter plot for these two
variables, I would like to add a linear model to see if I can
extrapolate any trends for specific species types .

<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

(If it makes more sense, then you can make/pick two versions of your
data, one for each research question.)

<!--------------------------- Start your work below --------------------------->

    # I am going to create a new version of my vancouver_trees_age dataset for Task 3

    vancouver_trees_age2 <- vancouver_trees_age %>%
      select(
        genus_name, species_name, cultivar_name, common_name, assigned,
        plant_area, neighbourhood_name, diameter, date_planted,
        longitude, latitude, Year_Column, tree_age, Diameter_string)

    print(vancouver_trees_age2)

    ## # A tibble: 146,611 × 14
    ##    genus_name species_name cultivar_name   common_name       assigned plant_area
    ##    <chr>      <chr>        <chr>           <chr>             <chr>    <chr>     
    ##  1 ULMUS      AMERICANA    BRANDON         BRANDON ELM       N        N         
    ##  2 ZELKOVA    SERRATA      <NA>            JAPANESE ZELKOVA  N        N         
    ##  3 STYRAX     JAPONICA     <NA>            JAPANESE SNOWBELL N        4         
    ##  4 FRAXINUS   AMERICANA    AUTUMN APPLAUSE AUTUMN APPLAUSE … Y        4         
    ##  5 ACER       CAMPESTRE    <NA>            HEDGE MAPLE       N        4         
    ##  6 PYRUS      CALLERYANA   CHANTICLEER     CHANTICLEER PEAR  N        B         
    ##  7 ACER       PLATANOIDES  COLUMNARE       COLUMNAR NORWAY … N        6         
    ##  8 ACER       PLATANOIDES  COLUMNARE       COLUMNAR NORWAY … N        6         
    ##  9 ACER       PLATANOIDES  COLUMNARE       COLUMNAR NORWAY … N        3         
    ## 10 FRAXINUS   AMERICANA    AUTUMN APPLAUSE AUTUMN APPLAUSE … N        3         
    ## # ℹ 146,601 more rows
    ## # ℹ 8 more variables: neighbourhood_name <chr>, diameter <dbl>,
    ## #   date_planted <date>, longitude <dbl>, latitude <dbl>, Year_Column <dbl>,
    ## #   tree_age <dbl>, Diameter_string <chr>

<!----------------------------------------------------------------------------->

# Task 3: Modelling

## 3.0 (no points)

Pick a research question from 1.2, and pick a variable of interest
(we’ll call it “Y”) that’s relevant to the research question. Indicate
these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: **What is the relationship between tree diameter
and age of tree?**

**Variable of interest**: *diameter*

<!----------------------------------------------------------------------------->

## 3.1 (3 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

-   **Note**: It’s OK if you don’t know how these models/tests work.
    Here are some examples of things you can do here, but the sky’s the
    limit.

    -   You could fit a model that makes predictions on Y using another
        variable, by using the `lm()` function.
    -   You could test whether the mean of Y equals 0 using `t.test()`,
        or maybe the mean across two groups are different using
        `t.test()`, or maybe the mean across multiple groups are
        different using `anova()` (you may have to pivot your data for
        the latter two).
    -   You could use `lm()` to test for significance of regression
        coefficients.

<!-------------------------- Start your work below ---------------------------->

    filtered_data <- vancouver_trees_age2[vancouver_trees_age2$common_name == "JAPANESE SNOWBELL", ]

    scatter_plot <- ggplot(data = filtered_data, aes(x = tree_age, y = diameter)) +
      geom_point() +
      labs(
        title = "Scatter Plot of Tree Age vs. Diameter for Japanese Snowbell",
        x = "Tree Age",
        y = "Diameter"
      ) +
      geom_smooth(method = "lm", se = FALSE, color = "blue") +  
      scale_x_log10() +  
      scale_y_log10()    

    print(scatter_plot)

    ## Warning: Transformation introduced infinite values in continuous y-axis
    ## Transformation introduced infinite values in continuous y-axis

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 228 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 228 rows containing missing values (`geom_point()`).

![](MDA-2-Andrew_files/figure-markdown_strict/unnamed-chunk-18-1.png)

<!----------------------------------------------------------------------------->

## 3.2 (3 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

-   Be sure to indicate in writing what you chose to produce.
-   Your code should either output a tibble (in which case you should
    indicate the column that contains the thing you’re looking for), or
    the thing you’re looking for itself.
-   Obtain your results using the `broom` package if possible. If your
    model is not compatible with the broom function you’re needing, then
    you can obtain your results by some other means, but first indicate
    which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

**I am looking to find multiple regression coefficients such as the
estimated coefficients for the linear regression model, the standard
error, the statistic and the p.value. I am hoping by gathering these 4
metrics that I will get a better understanding of the relationship
between tree age and tree diameter.**

    filtered_data <- vancouver_trees_age2[vancouver_trees_age2$common_name == "JAPANESE SNOWBELL", ]

    lm_model <- lm(diameter ~ tree_age, data = filtered_data)

    coefficients_df <- tidy(lm_model)

    print(coefficients_df)

    ## # A tibble: 2 × 5
    ##   term        estimate std.error statistic p.value
    ##   <chr>          <dbl>     <dbl>     <dbl>   <dbl>
    ## 1 (Intercept)   2.46      1.05        2.35  0.0188
    ## 2 tree_age      0.0932    0.0492      1.89  0.0587

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 4.1 (3 points)

Take a summary table that you made from Task 1, and write it as a csv
file in your `output` folder. Use the `here::here()` function.

-   **Robustness criteria**: You should be able to move your Mini
    Project repository / project folder to some other location on your
    computer, or move this very Rmd file to another location within your
    project repository / folder, and your code should still work.
-   **Reproducibility criteria**: You should be able to delete the csv
    file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

**First I will create a new “output” folder for my work.**

    output_folder <- "output"

    if (!dir.exists(output_folder)) {
      dir.create(output_folder)
    } else {
      cat(paste("The folder", output_folder, "already exists.\n"))
    }

    ## The folder output already exists.

    setwd(output_folder)

**I have selected to use the following research question and summary
table for this assignment:**

*What is the distribution of different species of “Spectacle” trees
throughout Vancouver? (“Spectacle” trees is an subjective term that will
be defined as species of that people visit as an attraction)*

*2. Compute the number of observations for at least one of your
categorical variables. Do not use the function `table()`!*

    # I have tested robustness and reproducibility manually by dragging and dropping my files to different locations and by deleting and rerunning my code.
    species_count <- vancouver_trees_age %>%
      group_by(species_name) %>%
      summarise(Count = n())

    output_file <- here::here("output", "species_summary.csv")

    write.csv(species_count, output_file, row.names = FALSE)

    cat("CSV file saved:", output_file, "\n")

    ## CSV file saved: C:/Users/andre/Documents/mda-Andyrooooo16/output/species_summary.csv

<!----------------------------------------------------------------------------->

## 4.2 (3 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

-   The same robustness and reproducibility criteria as in 4.1 apply
    here.

<!-------------------------- Start your work below ---------------------------->

**For reference, here is the code again for my model in Task 3:**

    # I have tested robustness and reproducibility manually by dragging and dropping my files to different locations and by deleting and rerunning my code.

    filtered_data <- vancouver_trees_age[vancouver_trees_age$common_name == "JAPANESE SNOWBELL", ]

    scatter_plot <- ggplot(data = filtered_data, aes(x = tree_age, y = diameter)) +
      geom_point() +
      labs(
        title = "Scatter Plot of Tree Age vs. Diameter for Japanese Snowbell",
        x = "Tree Age",
        y = "Diameter"
      ) +
      geom_smooth(method = "lm", se = FALSE, color = "blue") +  
      scale_x_log10() +  
      scale_y_log10()    

    print(scatter_plot)

    ## Warning: Transformation introduced infinite values in continuous y-axis
    ## Transformation introduced infinite values in continuous y-axis

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 228 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 228 rows containing missing values (`geom_point()`).

![](MDA-2-Andrew_files/figure-markdown_strict/unnamed-chunk-22-1.png)

    model_regression <- here::here("output", "your_model.rds")
    saveRDS(scatter_plot, file = model_regression)

    loaded_model <- readRDS(model_regression)

<!----------------------------------------------------------------------------->

# Overall Reproducibility/Cleanliness/Coherence Checklist

Here are the criteria we’re looking for.

## Coherence (0.5 points)

The document should read sensibly from top to bottom, with no major
continuity errors.

The README file should still satisfy the criteria from the last
milestone, i.e. it has been updated to match the changes to the
repository made in this milestone.

## File and folder structure (1 points)

You should have at least three folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (1 point)

All output is recent and relevant:

-   All Rmd files have been `knit`ted to their output md files.
-   All knitted md files are viewable without errors on Github. Examples
    of errors: Missing plots, “Sorry about that, but we can’t show files
    that are this big right now” messages, error messages from broken R
    code
-   All of these output files are up-to-date – that is, they haven’t
    fallen behind after the source (Rmd) files have been updated.
-   There should be no relic output files. For example, if you were
    knitting an Rmd to html, but then changed the output to be only a
    markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

## Tagged release (0.5 point)

You’ve tagged a release for Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
