# Common-R
list of common R commands

### Set up
Clear workspace:
```R
rm(list=ls())
```

Set working directory
```R
setwd("/Users/<name>/Documents/...")
```

### Data preparation
Recode value as NA:
```R
df$var[df$var==-999.00] <- NA
```
or
```R
mydata$v1[mydata$v1==99] <- NA
```
Recode NA as another value:
```R
d[is.na(d)] <- 0
```
Merge:
```R
new_df <- merge(df1, df2, by.x="df1key", by.y="df2key", all.x=TRUE, all.y=FALSE)
```

### Exploratory plots
### Pairs
Simple pairs:
```R
pairs(iris[1:4],
      main = "Anderson's Iris Data",
      pch = 21,
      bg = c("red", "green2", "steelblue4")[unclass(iris$Species)])
 ```
 Fancy pairs:
 from: http://bxhorn.com/2013/correlation-plots/
 ```R
 # Load packages
library(ggplot2, quietly = TRUE)
library(GGally, quietly = TRUE)
library(grid, quietly = TRUE)
 
# Load theme for ggplot2
theme_set(theme_bw())
 
# Generate plot
plot.layout <- ggpairs(iris, title = "Anderson's Iris Data", axisLabels="show", color = "Species")
plot.text <- ggally_text(paste0("Observations\nPer Variable:\n", dim(iris)[1]), aes(color="black"))
plot.cor1 <- ggally_cor(iris, mapping = aes(x = "Sepal.Length", y = "Sepal.Width", color = "black"), corSize = 4.5)
plot.cor2 <- ggally_cor(iris, mapping = aes(x = "Sepal.Length", y = "Petal.Length", color = "black"), corSize = 4.5)
plot.cor3 <- ggally_cor(iris, mapping = aes(x = "Sepal.Length", y = "Petal.Width", color = "black"), corSize = 4.5)
plot.cor4 <- ggally_cor(iris, mapping = aes(x = "Sepal.Width", y = "Petal.Length", color = "black"), corSize = 4.5)
plot.cor5 <- ggally_cor(iris, mapping = aes(x = "Sepal.Width", y = "Petal.Width", color = "black"), corSize = 4.5)
plot.cor6 <- ggally_cor(iris, mapping = aes(x = "Petal.Length", y = "Petal.Width", color = "black"), corSize = 4.5)
plot.layout <- putPlot(plot.layout, plot.text, 5, 5)
plot.layout <- putPlot(plot.layout, plot.cor1, 1, 2)
plot.layout <- putPlot(plot.layout, plot.cor2, 1, 3)
plot.layout <- putPlot(plot.layout, plot.cor3, 1, 4)
plot.layout <- putPlot(plot.layout, plot.cor4, 2, 3)
plot.layout <- putPlot(plot.layout, plot.cor5, 2, 4)
putPlot(plot.layout, plot.cor6, 3, 4)
 ```

### Plotting
density plot (with subscripts and superscripts in label):
```R
plot(density(ac.samp),main=expression(italic(Acacia)),xlab=expression('fixation rate (kg N ha'^-1*' yr'^-1*') per stand basal area'))
```

scatter:

scatter with large text:

histogram:

3x2 panel of graphs:

barchart:

barchart (ggplot):
```R
library(ggplot2)
library(ggthemes)
ggplot(s, aes(x=xcol, y=ycol, fill=factor(grpcol))) +
  geom_bar(stat="identity", position="dodge") +
  scale_fill_discrete(name="grp name") +
  xlab("x name")+ylab("y name") + ggtitle("Title") +
  theme_tufte() +
  #geom_rangeframe() +
  theme(axis.text=element_text(size=14), axis.title=element_text(size=14,face="bold"), 
        axis.line = element_line(color='black'), plot.title=element_text(size=20,face="bold",hjust=0.5),
        legend.text=element_text(size=14), legend.title=element_text(size=14, face="bold"))
```

whisker plot:

plot commands (adapted from: http://bxhorn.com/r-graphics-high-level-commands/)  
```barplot()```	Vertical or horizontal bar graph.  
```boxes()```	Boxplots at specified locations.  
```boxplot()```	Simple or side-by-side box plots.  
```contour()```	Line chart given x, y, and z co-ordinates (e.g. terrain lines). (The Trellis equivalent is contourplot()).  
```dotchart()```	Plots a dot chart from a vector.  
```hist()```	A histogram.  
```image()```	Heat map plot given x, y, and z co-ordinates (e.g. terrain area). The Trellis equivalent is levelplot()  
```matplot()```	Plots columns of one matrix against columns of another matrix.  
```persp()```	Perspective plot given a heights matrix on a spaced grid (e.g. terrain). Trellis equivalent is wireframe().  
```pie()```	A pie chart.  
```qqnorm()```	the quantile-quantile comparison is a given sample vs. the normal distribution  
```qqplot()```	Produces a graphical display to test the distribution of data based on quantile-quantile comparisons.  
```scatter()```	A scatter plot.  
```stars()```	Star plots of a matrix of multivariate data.  
```ts.plot()```	Plots one or more time series. By default, five line types and four collars are cycled through.  
```xyplot()```	Trellis scatter plots.  

modifying plots (adapted from: http://bxhorn.com/r-graphics-high-level-commands/)  
```abline()```	Add lines to the current plot; horizontal, vertical, or slope-intercept form  
```arrows()```	Draw arrows between pairs of points.  
```axis()```	Add a custom axis to the plot  
```box()```	Surround the current plot with a box.  
```identify()```	Read the position of the graphics pointer when the (first) mouse button is pressed. Returns and index with x/y coordinates.  
```lines()```	Add lines to the plot.  
```locator()```	Returns co-ordinates specified interactively on a plot so points/lines can be added  
```mtext()```	Add text in the margins.  
```par()```	Set graphics parameters; controls the actions of the graphic device.  
```points()```	Add points to the plot  
```polygon()```	Add polygon(s) to the plot.  
```rect()```	Add a rectangle to the plot.  
```segments()```	Draw line segments between pairs of points.  
```symbols()```	Add symbols to the plot.  
```text()```	Add text to the plot  
```title()```	Add labels to the plot. Use with expression() for math symbols.  

### Models
distributions:

95% CI from bootstrapped sample:
```R
ac.samp <- rnorm(n,ac.mu,ac.se)
quantile(ac.samp,.025) 
quantile(ac.samp,.975)  
```

linear mixed effect model:

### Mapping
one country map:
```R
# Map of Japan
map_data("world") %>%
  filter(region == 'Japan') %>%
  ggplot(aes(x = long, y = lat, group = group)) +
    geom_polygon()
```
