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

### Replace NAs
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

### Models
distributions:

95% CI from bootstrapped sample:
```R
ac.samp <- rnorm(n,ac.mu,ac.se)
quantile(ac.samp,.025) 
quantile(ac.samp,.975)  
```

linear mixed effect model:

