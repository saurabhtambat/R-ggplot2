GGPLOT2
================
Rohit chaware 2208, Saurabh Tambat 2239 & Nitesh sathe 2233
13/12/2022

------------------------------------------------------------------------

## INTRODUCTION

1.  ggplot2 is an R package which is designed especially for data
    visualization and providing best exploratory data analysis.

2.  Provides beautiful, hassle-free plots that take care of minute
    details like drawing legends and representing them

3.  Designed for data visualization and providing exploratory data
    analysis.

4.  **ggplot2** graphics are built layer by layer by adding new
    elements. Adding layers in this fashion allows for extensive
    flexibility and customization of plots.

5.  This package works under deep grammar called as “Grammar of
    graphics” which is made up of a set of independent components that
    can be created in many ways.

------------------------------------------------------------------------

## Prerequisites

-   ggplot2 is included in the **tidyverse** package.
-   To reproduce the code throughout this tutorial you will need to load
    the ggplot2 package. Note that ggplot2 also comes with a number of
    built-in data sets.

## Grammer of Graphics

Just as the grammar of language helps us construct meaningful sentences
out of words, the Grammar of Graphics helps us to construct graphical
figures out of different visual elements. This grammar gives us a way to
talk about parts of a plot: all the circles, lines, arrows, and words
that are combined into a diagram for visualizing data.

Now let us focus on different types of plots which can be created with
reference to the grammar

-   the data being plotted

-   the geometric objects like circles, lines, etc.that appear on the
    plot

-   a set of mappings from variables in the data to the aesthetics
    (appearance) of the geometric objects

-   a statistical transformation used to calculate the data values used
    in the plot

-   a position adjustment for locating each geometric object on the plot

-   a scale e.g., range of values for each aesthetic mapping used

-   a coordinate system used to organize the geometric objects

-   the facets or groups of data shown in different plots

All together, this grammar enables us to discuss what plots look like
using a standard set of vocabulary.

------------------------------------------------------------------------

## Learning Objectives

-   Creating a ggplot

-   Aesthetic Mapping

-   Faceting

-   Geometric Objects

-   Statistical Transformation

-   Position Adjustment

-   Coordinate System

-   Graphical parameters

-   Plotting with ggplot2

------------------------------------------------------------------------

## Creating a ggplot

-   **Template to build a graph**

            ggplot (data = data) + 

            geom_funtion (mapping = aes( mapping ), stat = stat , position = position ) +

            coordinate_funtion +

            facet_funtion +

            scale_funtion +

            theme_funtion

### Example

**Que**. Do cars with big engines use more fuel than cars with small
engines? What does the relationship between engine size and fuel
efficiency look like? Is it positive? Negative? Linear? Nonlinear?

-   variables in mpg are:

1.  displ, a car’s engine size, in liters.

2.  hwy, a car’s fuel efficiency on the highway, in miles per gallon
    (mpg)

``` r
library(ggplot2)
data("mpg")
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy))
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

------------------------------------------------------------------------

## Aesthetic Mappings

-   The aesthetic mappings take properties of the data and use them to
    influence visual characteristics, such as position, color, size,
    shape, or transparency.

-   You can add a third variable, like class, to a two-dimensional
    scatterplot by mapping it to an aesthetic.

-   Aesthetic is a visual property of the objects in your plot.

-   Aesthetics include things like the size, the shape, or the color of
    your points.

For example, we can add a mapping from the class of the cars to a color
characteristic:

``` r
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy, color =class))
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_point(color = "blue")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

------------------------------------------------------------------------

## Facets

-   The facet approach partitions a plot into a matrix of panels. Each
    panel shows a different subset of the data.

-   Facets divide a plot into subplots based on the values of one or
    more discrete variables.

-   This also describes how to split a graph using ggplot2 package.

-   There are two main functions for faceting :

    facet_grid() facet_wrap()

``` r
ggplot(data = mpg) +
geom_point(mapping = aes(x = displ, y = hwy)) +
facet_grid(drv ~ cyl)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

-   you can use the argument **margins** to add additional facets which
    contain all the data for each of the possible values of the faceting
    variables

``` r
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy)) +
 facet_grid(drv ~ cyl, margins=TRUE)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

-   By default, all the panels have the same scales (scales=“fixed”).
    They can be made independent, by setting scales to free, free_x, or
    free_y.

``` r
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy)) +
 facet_grid(drv ~ cyl, scales='free')
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

-   The argument labeller can be used to control the labels of the
    panels

``` r
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy)) +
 facet_grid(drv ~ cyl, labeller=label_both)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy)) +
 facet_wrap(~ class, nrow = 2)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

------------------------------------------------------------------------

## Geometric Objects

-   A geom is the geometrical object that a plot uses to represent data.

-   ggplot2 can be used to build almost any kind of plot you may want.

-   ggplot2 supports a number of different types of geoms, including:

• geom_point for drawing individual points (e.g., a scatter plot)

``` r
ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_point()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

• geom_line for drawing lines (e.g., for a line charts)

• geom_smooth for drawing smoothed lines (e.g., for simple trends or
approximations)

``` r
ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

• geom_bar for drawing bars (e.g., for bar charts)

``` r
ggplot(data = mpg, aes(x = class)) +
  geom_bar()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

• geom_histogram for drawing binned values (e.g. a histogram)

``` r
ggplot(data = mpg, aes(x = hwy)) +
  geom_histogram()
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

• geom_polygon for drawing arbitrary shapes

``` r
ggplot(mpg, aes(x = hwy, y = displ))+
  geom_polygon()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

• geom_map for drawing polygons in the shape of a map! (You can access
the data to use for these maps by using the map_data() function).

-   **To display multiple geoms in the same plot, add multiple geom
    functions to ggplot()**

``` r
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy)) +
 geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
# color aesthetic passed to each geom layer
ggplot(mpg, aes(x = displ, y = hwy, color = class)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

``` r
# color aesthetic specified for only the geom_point layer
ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_point(aes(color = class)) +
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
ggplot(data = mpg) +
 geom_smooth(mapping = aes(x = displ, y = hwy,linetype=drv))
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

------------------------------------------------------------------------

## Statistical Transformations

-   The algorithm used to calculate new values for a graph

-   **stat** is shortform for statistical transformation.

Consider the diamonds dataset in ggplot2 which contains information
about \~54,000 diamonds, including the price, carat, color, clarity, and
cut of each diamond.

``` r
ggplot(data = diamonds) +
 geom_bar(mapping = aes(x = cut))
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

1.  **stat_count()**: geom_bar shows the default value for stat is
    “count,” which means that geom_bar() uses **stat_count()**.

You can generally use geoms and stats interchangeably. For example, you
can re-create the previous plot using **stat_count()** instead of
geom_bar():

``` r
ggplot(data = diamonds) +
 stat_count(mapping = aes(x = cut))
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

2.  **stat_summary()**, which summarizes the y values for each unique x
    value, to draw attention to the summary that you’re computing:

``` r
ggplot(data = diamonds) +
 stat_summary(mapping = aes(x = cut, y = depth),
 fun.ymin = min,
 fun.ymax = max,
 fun.y = median)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

------------------------------------------------------------------------

## Position Adjustments

-   The stacking is performed automatically by the position adjustment
    specified by the position argument.

-   If you don’t want a stacked barchart, you can use one of three other
    options: “identity”, “dodge” or “fill”:

1.  **position = “fill”** works like stacking, but makes each set of
    stacked bars the same height. This makes it easier to compare
    proportions across groups:

``` r
ggplot(data = diamonds) +
 geom_bar(mapping = aes(x = cut, fill = clarity),
 position = "fill")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

2.  **position = “dodge”** places overlapping objects directly beside
    one another. This makes it easier to compare individual values:

``` r
ggplot(data = diamonds) +
 geom_bar(mapping = aes(x = cut, fill = clarity),
 position = "dodge")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

-   Below you can see that the values of hwy and displ are rounded so
    the points appear on a grid and many points overlap each other. This
    problem is known as overplotting.

``` r
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy))
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-24-1.png)<!-- --> so to
overcome such we use

3.  **position = “jitter”**: You can avoid this gridding by setting the
    position adjustment to “jitter.” **position = “jitter”** adds a
    small amount of random noise to each point.

``` r
ggplot(data = mpg) +
 geom_point(mapping = aes(x = displ, y = hwy),
 position = "jitter")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

------------------------------------------------------------------------

## Coordinate System

-   Coordinate systems are probably the most complicated part of
    ggplot2.
-   There are a number of other coordinate systems that are helpful:

1.  **coord_flip()** :

switches the x-axes and y-axes

``` r
ggplot(data = mpg, mapping = aes(x = class, y = hwy)) +
 geom_boxplot()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = class, y = hwy)) +
 geom_boxplot() +
 coord_flip()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-26-2.png)<!-- -->

2.  **coord_quickmap()** :

-   Sets the aspect ratio correctly for maps.

-   coord_map() projects a portion of the earth, which is approximately
    spherical, onto a flat 2D plane

``` r
nz=map_data("nz")
ggplot(nz, aes(long, lat, group = group)) +
geom_polygon(fill = "white", color = "black")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

``` r
ggplot(nz, aes(long, lat, group = group)) +
 geom_polygon(fill = "white", color = "black") +
 coord_quickmap()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-27-2.png)<!-- -->

3.  **coord_polar()** : Uses polar coordinates and Polar coordinates
    show connection between a bar chart and a **Coxcomb** chart

``` r
library(ggplot2)
bar = ggplot(data = diamonds) +
 geom_bar(mapping = aes(x = cut, fill = cut),
 show.legend = TRUE,
 width = 1) +
 labs(x = NULL, y = NULL)
bar
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

``` r
bar + coord_flip()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

``` r
bar + coord_polar()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-29-2.png)<!-- -->

------------------------------------------------------------------------

## Geometrical Parameters

### Themes

-   The function **theme()** is used to control non-data parts of the
    graph including

1.  **theme_bw()**

White background with grid lines.

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme_bw()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

2.  **theme_gray()**

Grey background (default theme)

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme_gray(base_size = 15)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

3.  **theme_void()**

Empty theme

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme_void()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

4)**theme_dark()**

Dark background designed to make colours pop out

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme_dark()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

5.  **theme_linedraw()**

black lines around the plot

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme_linedraw()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-34-1.png)<!-- -->

6.  **theme_light()**

light gray lines and axis (more attention towards the data)

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme_light()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

7.  **theme_minimal()**

no background annotations

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme_minimal()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->

8.  **theme_classic()**

theme with axis lines and no grid lines

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme_classic()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-37-1.png)<!-- -->

-   The R code below illustrates how to modify the appearance of the
    plot panel background and grid lines.

**Change the colors of plot panel background to lightblue**

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot() +
  theme (panel.background = element_rect(fill = "lightblue",size = 0.5, linetype = "solid"))
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->

------------------------------------------------------------------------

## Legends

1.  **theme(legend.position = ” “)**

Place legend at “bottom”, “top”, “left”, or “right”

``` r
data(iris)
ggplot(iris,aes(Sepal.Length,Petal.Length,colour=Species)) +
 geom_point() +
 theme(legend.position="bottom")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

2.  **guides(fill = “none”)**

Set legend type for each aesthetic: colorbar, legend, or none (no
legend)

3.  **scale_fill_discrete(name = “Title”, labels = c(“A”, “B”, “C”, “D”,
    “E”))**

Set legend title and labels with a scale function.

------------------------------------------------------------------------

## Labels

-   t + labs( x = “New x axis label”, y = “New y axis label”, title
    =“Add a title above the plot”, subtitle = “Add a subtitle below
    title”, caption = “Add a caption below plot”)

``` r
ggplot(iris,aes(Sepal.Length,Petal.Length,colour=Species)) +
 geom_point() +
labs(title ="IRISPLOT", subtitle = "Scatterplot",caption = "Relationship between Sepal.Length and Petal.Length")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-40-1.png)<!-- -->

-   t + (annotate(geom = “text”, x = 8, y = 9, label = “A”))

manual values for geom’s aesthetics.

``` r
ggplot(iris,aes(Sepal.Length,Petal.Length,colour=Species)) +
 geom_point() +
 annotate(geom = "text",x=6,y=5,label="Hello")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-41-1.png)<!-- -->

------------------------------------------------------------------------

## Create a scatter plot and change point shapes using the argument shape

``` r
library(ggplot2)
# Basic scatter plot
ggplot(mpg, aes(x=displ, y=hwy)) +
  geom_point()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-42-1.png)<!-- -->

``` r
# Change the point shape
ggplot(mpg, aes(x=displ, y=hwy)) +
  geom_point(shape=18)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-42-2.png)<!-- -->

``` r
# change shape, color, fill, size
ggplot(mpg, aes(x=displ, y=hwy)) +
  geom_point(shape=23, fill="blue", color="darkred", size=3)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-42-3.png)<!-- -->

------------------------------------------------------------------------

![](C:\Users\tamba\Downloads\slide_2.jpg)

------------------------------------------------------------------------

## Boxplot

Now we will describes how to create a box plot using R software and
ggplot2 package.The function **geom_boxplot()** is used. A simplified
format is:

    geom_boxplot(outlier.colour="black", outlier.shape=16,
             outlier.size=2, notch=FALSE)

• outlier.colour, outlier.shape, outlier.size : The color, the shape and
the size for outlying points.

• notch : logical value. If TRUE, make a notched box plot. The notch
displays a confidence interval around the median

``` r
# Basic box plot
p=ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot()
p
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-43-1.png)<!-- -->

### Rotate the box plot

``` r
p + coord_flip()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

### Notched box plot

``` r
# Notched box plot
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot(notch=TRUE)
```

    ## Notch went outside hinges
    ## ℹ Do you want `notch = FALSE`?
    ## Notch went outside hinges
    ## ℹ Do you want `notch = FALSE`?

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-45-1.png)<!-- -->

### Change outlier, color, shape and size

``` r
ggplot(mpg, aes(x=class, y=hwy)) + 
  geom_boxplot(outlier.colour="red", outlier.shape=8,
                outlier.size=4)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

------------------------------------------------------------------------

## Histogram

``` r
# Basic histogram
ggplot(data=mpg, aes(x=cty)) + 
  geom_histogram()
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-47-1.png)<!-- -->

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-48-1.png)<!-- -->

``` r
ggplot(data=mpg, aes(x=cty)) +
geom_histogram(col="black",fill="blue",alpha = 0.5,binwidth =3)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-49-1.png)<!-- -->

``` r
ggplot(data=mpg, aes(x=cty)) +
geom_histogram(col="black",fill="red",binwidth =3,linetype="dashed")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-50-1.png)<!-- -->

------------------------------------------------------------------------

## Stripchart

Stripcharts are also known as one dimensional scatter plots. These plots
are suitable compared to box plots when sample sizes are small.

The function geom_jitter() is used.

``` r
# Basic stripchart
ggplot(ToothGrowth, aes(x=dose, y=len)) + 
  geom_jitter()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-51-1.png)<!-- -->

``` r
# Change the position
# 0.2 : degree of jitter in x direction
p=ggplot(ToothGrowth, aes(x=dose, y=len)) + 
  geom_jitter(position=position_jitter(0.2))
p
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-51-2.png)<!-- -->

``` r
# Rotate the stripchart
p + coord_flip()
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-51-3.png)<!-- -->

``` r
# Change point size
ggplot(ToothGrowth, aes(x=dose, y=len)) + 
  geom_jitter(position=position_jitter(0.2), cex=1.2)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-52-1.png)<!-- -->

``` r
# Change shape
ggplot(ToothGrowth, aes(x=dose, y=len)) + 
  geom_jitter(position=position_jitter(0.2), shape=17)
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-52-2.png)<!-- -->

``` r
# stripchart with mean points
p + stat_summary(fun.y=mean, geom="point", shape=18,
                 size=3, color="red")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-53-1.png)<!-- -->

``` r
# stripchart with median points
p + stat_summary(fun.y=median, geom="point", shape=18,
                 size=3, color="red")
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-53-2.png)<!-- -->

------------------------------------------------------------------------

## Piechart

``` r
df = as.data.frame(table(mpg$drv))
colnames(df) = c("class", "freq")
pie = ggplot(df, aes(x = "", y=freq, fill = factor(class))) +
 geom_bar(width = 1,stat = "identity")+
coord_polar("y",start=0)
pie
```

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-54-1.png)<!-- -->

**Change the pie chart fill colors**

-   It is possible to change manually the pie chart fill colors using
    the functions

• scale_fill_manual() : to use custom colors

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-55-1.png)<!-- -->

♥ scale_fill_grey() : to use grey color palettes

![](ggplot2pre2_files/figure-gfm/unnamed-chunk-56-1.png)<!-- -->

------------------------------------------------------------------------

![](C:\Users\tamba\Downloads\1000_F_291522205_XkrmS421FjSGTMRdTrqFZPxDY19VxpmL.jpg)
