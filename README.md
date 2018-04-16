# Common-R
list of common R commands

## Clear workspace

## Replace NAs

## Exploratory plots
### Pairs
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

## Plotting
scatter:
histogram:
3x2 panel of graphs:
barchart:
whisker plot:

## Models
distributions:
linear mixed effect model:
