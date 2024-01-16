# Introduction to ggplot2

ggplot2 is a plotting package in R. Graphics are built layer by layer by adding new elements. This approach allows for extensive flexibility and customization of plots.

Load the library:
```{r, echo=TRUE}
library(ggplot2)
```

Load the data:
To create the dataset used in this tutorial please see the following tutorial: https://github.com/SparkleMalone/DataBasics

### Building blocks of layers with the grammar of graphics:
- Data: The element is the dataset itself
- Aesthetics: The data is used to map onto the aesthetics attributes such as x-axis, y-axis, color, fill, size, labels, alpha, shape, line width, line type
- Geometrics: How the data being displayed using point, line, histogram, bar, boxplot
- Facets: Display the subset of the data using columns and rows
- Statistics: Binning, smoothing, descriptive, intermediate
- Coordinates: the space between data and display using Cartesian, fixed, polar, limits
- Themes: Non-data link

### Data Layer:
We first need to define the source of the information to be visualized. The function ggplot() is used to generate the plots.

```{r, echo=TRUE}
ggplot(data = Yale.Myers.sub) + 
 labs(title = "Climate of Yale Myers Forest")

```
### Aesthetic Layer:
mapping ... display and map dataset into certain aesthetics.

```{r, echo=TRUE}
ggplot(data = Yale.Myers.sub, aes(x = date , y = tmean)) +
  labs(title = "Climate of Yale Myers Forest")
 ```
### Geometric layer:
The geometric layer controls the essential elements, see how the data being displayed using point, line, histogram, bar, boxplot.

```{r, echo=TRUE}
ggplot(data = Yale.Myers.sub, aes(x = date , y = tmean))+
   geom_point() +
  labs(title = "Miles per Gallon vs Horsepower",
       x = "Date",
       y = "Mean Air Temperature (Degrees Celcius)")
```

Geometric layer: Adding size, color, and shape.

```{r, echo=TRUE}
# Adding size
ggplot(data = Yale.Myers.sub, aes(x = date , y = tmean, size=year))+
  geom_point() +
  labs(title = 'Climate of Yale Myers Forest',
       x = "Date",
       y = "Mean Air Temperature (Degrees Celcius)")
       
# Adding shape and color
ggplot(data = Yale.Myers.sub, aes(x = date , y = tmean, col=month))+
  geom_point() +
  labs(title = 'Climate of Yale Myers Forest',
       x = "Date",
       y = "Mean Air Temperature (Degrees Celcius)")
 
# Histogram plot
ggplot(data =  Yale.Myers.sub, aes(x = tmean)) +
  geom_histogram(binwidth = 5) +
  labs(title = 'Climate of Yale Myers Forest',
       x = "Mean Air Temperature (Degrees Celcius)",
       y = "Count" )
```

### Facet Layer:
The facet layer is used to split the data into subsets of the entire dataset. It allows the subsets to be visualized on the same plot. Here we separate plots according to month.

```{r, echo=TRUE}

# Subset dataset to indlude only months 9-11
Yale.Myers.fall <- Yale.Myers.sub %>% filter( month > '08' & month < '12')

p <- ggplot(data = Yale.Myers.fall, aes(x = date , y = tmean)) + geom_point()

p + facet_grid(month ~ .) +
  labs(title = 'Climate of Yale Myers Forest',
       x = "Date",
       y = "Mean Air Temperature (Degrees Celcius)")

```
### Statistics layer
We can transform our data using binning, smoothing, descriptive, intermediate. We will explore how february temperatures have changed from 1990 - 2018
```{r, echo=TRUE}

#Subset the data:
Yale.Myers.feb <- Yale.Myers.sub %>% filter( month =='02')

ggplot(data = Yale.Myers.feb, aes(x = date , y = tmean)) + geom_point() +
  stat_smooth(method = lm, col = "red") +
  labs(title = 'Climate of Yale Myers Forest')

```
### Coordinates layer:

Data coordinates are mapped together to the mentioned plane of the graphic and we adjust the axis and change the spacing of the displayed data with control plot dimensions.
```{r, echo=TRUE}
ggplot(data = Yale.Myers.fall, aes(x = tmin , y = tmean)) + geom_point() +
  stat_smooth(method = lm, col = "red") +
  labs(title = 'Climate of Yale Myers Forest') +
  scale_y_continuous(limits = c(-10, 40), expand = c(0, 0)) +
  scale_x_continuous(limits = c(-10, 40), expand = c(0, 0)) +
  coord_equal() +
  labs(title = 'Climate of Yale Myers Forest')
  
	```
Coord_cartesian() to proper zoom in:
```{r, echo=TRUE}
# Add coord_cartesian() to proper zoom in
ggplot(data = Yale.Myers.fall, aes(x = tmin , y = tmean)) + geom_point() +
  stat_smooth(method = lm, col = "red") +
  labs(title = 'Climate of Yale Myers Forest')  +
						coord_cartesian(xlim = c(-10, 10))
```				
### Theme Layer:
Layer controls the finer points of display, like the font size and background color properties.

Example: Theme layer – element_rect() function:
```{r, echo=TRUE}

ggplot(data = Yale.Myers.fall, aes(x = tmin , y = tmean)) + geom_point() +
  stat_smooth(method = lm, col = "red") +
  facet_grid(. ~ month) +
  theme(plot.background = element_rect(fill = "blue", colour = "gray")) 
```