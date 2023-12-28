# Introduction to ggplot2

ggplot2 is a plotting package. The function ggplot()  is used to generate the plots, and so references to using the function will be referred to as ggplot() and the package as a whole as ggplot2. Graphics are built layer by layer by adding new elements. This approach allows for extensive flexibility and customization of plots.

Load the library:
```{r, echo=TRUE}
library(ggplot2)
```

### Building blocks of layers with the grammar of graphics:
- Data: The element is the data set itself
- Aesthetics: The data is to map onto the Aesthetics attributes such as x-axis, y-axis, color, fill, size, labels, alpha, shape, line width, line type
- Geometrics: How our data being displayed using point, line, histogram, bar, boxplot
- Facets: It displays the subset of the data using Columns and rows
- Statistics: Binning, smoothing, descriptive, intermediate
- Coordinates: the space between data and display using Cartesian, fixed, polar, limits
- Themes: Non-data link

### Data Layer:
We first need to define the source of the information to be visualized.

```{r, echo=TRUE}
ggplot(data = mtcars) +  labs(title = "MTCars Data Plot")
```
### Aesthetic Layer:
mapping ... display and map dataset into certain aesthetics.

```{r, echo=TRUE}
ggplot(data = mtcars, aes(x = hp, y = mpg, col = disp))+
 labs(title = "MTCars Data Plot")
 ```
### Geometric layer:
ggplot2 in R geometric layer control the essential elements, see how our data being displayed using point, line, histogram, bar, boxplot.

```{r, echo=TRUE}
ggplot(data = mtcars, aes(x = hp, y = mpg, col = disp)) +
  geom_point() +
  labs(title = "Miles per Gallon vs Horsepower",
       x = "Horsepower",
       y = "Miles per Gallon")
```

Geometric layer: Adding Size, color, and shape and then plotting the Histogram plot

```{r, echo=TRUE}
# Adding size
ggplot(data = mtcars, aes(x = hp, y = mpg, size = disp)) +
  geom_point() +
  labs(title = "Miles per Gallon vs Horsepower",
       x = "Horsepower",
       y = "Miles per Gallon")
 
# Adding shape and color
ggplot(data = mtcars, aes(x = hp, y = mpg, col = factor(cyl),
       shape = factor(am))) +geom_point() +
  labs(title = "Miles per Gallon vs Horsepower",
       x = "Horsepower",
       y = "Miles per Gallon")
 
# Histogram plot
ggplot(data = mtcars, aes(x = hp)) +
  geom_histogram(binwidth = 5) +
  labs(title = "Histogram of Horsepower",
       x = "Horsepower",
       y = "Count")
```

### Facet Layer:
ggplot2 in R facet layer is used to split the data up into subsets of the entire dataset and it allows the subsets to be visualized on the same plot. Here we separate rows according to transmission type and Separate columns according to cylinders.

```{r, echo=TRUE}
# Facet Layer
# Separate rows according to transmission type
p <- ggplot(data = mtcars, aes(x = hp, y = mpg, shape = factor(cyl))) + geom_point()
 
p + facet_grid(am ~ .) +
  labs(title = "Miles per Gallon vs Horsepower",
       x = "Horsepower",
       y = "Miles per Gallon")
 
# Separate columns according to cylinders
p <- ggplot(data = mtcars, aes(x = hp, y = mpg, shape = factor(cyl))) + geom_point()
 
p + facet_grid(. ~ cyl) +
  labs(title = "Miles per Gallon vs Horsepower",
       x = "Horsepower",
       y = "Miles per Gallon")
```

# Statistics layer
ggplot2 in R this layer, we transform our data using binning, smoothing, descriptive, intermediate
```{r, echo=TRUE}
ggplot(data = mtcars, aes(x = hp, y = mpg)) +
  geom_point() +
  stat_smooth(method = lm, col = "red") +
  labs(title = "Miles per Gallon vs Horsepower")
```
Coordinates layer:
ggplot2 in R these layers, data coordinates are mapped together to the mentioned plane of the graphic and we adjust the axis and changes the spacing of displayed data with Control plot dimensions.

```{r, echo=TRUE}
ggplot(data = mtcars, aes(x = wt, y = mpg)) +
geom_point() +
stat_smooth(method = lm, col = "red") +
scale_y_continuous("Miles per Gallon", limits = c(2, 35), expand = c(0, 0)) +
scale_x_continuous("Weight", limits = c(0, 25), expand = c(0, 0)) +
coord_equal() +
labs(title = "Miles per Gallon vs Weight",
	x = "Weight",
	y = "Miles per Gallon")
	```
Coord_cartesian() to proper zoom in:
```{r, echo=TRUE}
# Add coord_cartesian() to proper zoom in
ggplot(data = mtcars, aes(x = wt, y = hp, col = am)) +
						geom_point() + geom_smooth() +
						coord_cartesian(xlim = c(3, 6))
```				
						
# Theme Layer:
ggplot2 in R layer controls the finer points of display like the font size and background color properties.

Example 1: Theme layer – element_rect() function
```{r, echo=TRUE}
ggplot(data = mtcars, aes(x = hp, y = mpg)) +
geom_point() +
facet_grid(. ~ cyl) +
theme(plot.background = element_rect(fill = "blue", colour = "gray")) +
labs(title = "Miles per Gallon vs Horsepower")
```


