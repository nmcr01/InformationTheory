
Workflow Basics and ggplot2 in R
========================================================
author: Robin Choudhury
date: 2018-07-04
autosize: true
transition: fade
font-family: 'Helvetica'
<style>
.small-code pre code {
  font-size: 1em;
}
</style>

Workflow Basics in R
========================================================
![](console.png)

For this Section we will be using RStudio


Coding Basics 1
========================================================
R can work like a calculator...

```r
1 / 200 * 30
```

```
[1] 0.15
```


```r
pi *3
```

```
[1] 9.424778
```
Base R knows `pi` as the constant `3.14...`.


Coding Basics 2
========================================================
R can also handle text...

```r
print("Hello, World!")
```

```
[1] "Hello, World!"
```

And can mix text and calculations...

```r
paste("The value of pi is", pi)
```

```
[1] "The value of pi is 3.14159265358979"
```



Coding Basics 3
========================================================
You can also create new objects with `<-`

```r
a <- 1 / 200 * 30; a
```

```
[1] 0.15
```
Then use those objects in subsequent calculations

```r
a*3
```

```
[1] 0.45
```


Coding Basics 4
========================================================
Object names must start with a letter, and needs to contain letters, numbers, **_**, and **.**

You can make assignments with either **<-** or **=**, but most people prefer **<-**. Using **<-** originated when APL computers had a single <- key on them (see http://blog.revolutionanalytics.com/2008/12/use-equals-or-arrow-for-assignment.html for more info). 

R is case sensitive, so **A** will not tell you the value of **a**

ggplot2 and the Aesthetic of Graphics
========================================================
ggplot2 is part of a a suite of packages in R known colloquially as the 'Tidyverse'. ggplot2 was developed to build graphs by mapping aesthetics, allowing users to flexibly create beautiful publication-quality figures.


```r
library(tidyverse)
library(datasets)
```


The Dataset 
========================================================
![](iris.jpg)

I will be using the iris dataset:

- Common example dataset
- Fairly compact (150 obs. of 5 variables)
- Flower measurement of 3 iris species

```r
data(iris)
```


ggplot2 Basics: Making the First Call
========================================================
class: small-code
As mentioned earlier, ggplot2 works by layering on different aesthetics from a dataset. ggplot2 first needs to know what dataset you plan to use, and what will be plotted.


```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width))
```

![plot of chunk unnamed-chunk-9](ggplot-figure/unnamed-chunk-9-1.png)
...pretty boring. Why?

ggplot2 Basics: Adding Aesthetics
========================================================
class: small-code
Now we want to use a scatterplot method to mark out these two variables. 

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width))+
  geom_point()
```

![plot of chunk unnamed-chunk-10](ggplot-figure/unnamed-chunk-10-1.png)

ggplot2 Basics: Adding Smoothing Functions
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width))+
  geom_point() + geom_smooth()
```

![plot of chunk unnamed-chunk-11](ggplot-figure/unnamed-chunk-11-1.png)

ggplot2 Basics: Color Points By Species
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width))+
  geom_point(aes(color=Species)) + geom_smooth()
```

![plot of chunk unnamed-chunk-12](ggplot-figure/unnamed-chunk-12-1.png)

ggplot2 Basics: Size by Petal Length
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width))+
  geom_point(aes(color=Species, size=Petal.Length)) + geom_smooth()
```

![plot of chunk unnamed-chunk-13](ggplot-figure/unnamed-chunk-13-1.png)

ggplot2 Basics: Color Lines and Points By Species
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width,color=Species))+
  geom_point(aes(size=Petal.Length)) + geom_smooth()
```

![plot of chunk unnamed-chunk-14](ggplot-figure/unnamed-chunk-14-1.png)

ggplot2 Basics: Use Linear Smoothing
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width,color=Species))+
  geom_point(aes(size=Petal.Length)) + geom_smooth(method="lm")
```

![plot of chunk unnamed-chunk-15](ggplot-figure/unnamed-chunk-15-1.png)

ggplot2 Basics: Different Line Types
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width,color=Species))+
  geom_point(aes(size=Petal.Length)) + geom_smooth(aes( linetype=Species), method="lm")
```

![plot of chunk unnamed-chunk-16](ggplot-figure/unnamed-chunk-16-1.png)

ggplot2 Basics: Rug Really Ties the Room Together
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width,color=Species))+
  geom_point(aes(size=Petal.Length)) + geom_smooth(aes( linetype=Species), method="lm") +
  geom_rug()
```

![plot of chunk unnamed-chunk-17](ggplot-figure/unnamed-chunk-17-1.png)

ggplot2 Basics: Density
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width,color=Species))+
  geom_point(aes(size=Petal.Length)) + 
  geom_density2d()
```

![plot of chunk unnamed-chunk-18](ggplot-figure/unnamed-chunk-18-1.png)

ggplot2 Basics: Hex
========================================================
class: small-code

```r
ggplot(data=iris, aes(x = Sepal.Length,y = Sepal.Width))+
  geom_hex()
```

![plot of chunk unnamed-chunk-19](ggplot-figure/unnamed-chunk-19-1.png)

ggplot2 Basics: Histograms
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram()
```

![plot of chunk unnamed-chunk-20](ggplot-figure/unnamed-chunk-20-1.png)

ggplot2 Basics: Histograms with Dodge
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram(position = "dodge")
```

![plot of chunk unnamed-chunk-21](ggplot-figure/unnamed-chunk-21-1.png)

ggplot2 Basics: Fill vs. Color
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram(color="black")
```

![plot of chunk unnamed-chunk-22](ggplot-figure/unnamed-chunk-22-1.png)

ggplot2 Basics: Inside vs. Outside of Aes
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram(aes(color="black"))
```

![plot of chunk unnamed-chunk-23](ggplot-figure/unnamed-chunk-23-1.png)

ggplot2 Basics: Alpha
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram(aes(color="black"), alpha=0.5)
```

![plot of chunk unnamed-chunk-24](ggplot-figure/unnamed-chunk-24-1.png)

ggplot2 Basics: Theme
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram(color="black")+
  theme_bw()
```

![plot of chunk unnamed-chunk-25](ggplot-figure/unnamed-chunk-25-1.png)

ggplot2 Basics: Theme
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram(color="black", alpha=0.5)+
  theme_bw() + 
  theme(legend.position="bottom")
```

![plot of chunk unnamed-chunk-26](ggplot-figure/unnamed-chunk-26-1.png)

ggplot2 Basics: Theme
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram(color="black", alpha=0.5)+
  theme_bw() + 
  theme(legend.position="bottom",
        axis.title=element_text(size=20, face="bold"))
```

![plot of chunk unnamed-chunk-27](ggplot-figure/unnamed-chunk-27-1.png)

ggplot2 Basics: Axis Labels
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
geom_histogram(color="black", alpha=0.5)+
  theme_bw() + ylab("Count")+xlab("Sepal Length")+
  theme(legend.position="bottom",
        axis.title=element_text(size=20, face="bold"))
```

![plot of chunk unnamed-chunk-28](ggplot-figure/unnamed-chunk-28-1.png)

ggplot2 Basics: stat_ vs geom_
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length,fill=Species))+
stat_bin()
```

![plot of chunk unnamed-chunk-29](ggplot-figure/unnamed-chunk-29-1.png)


ggplot2 Basics: Multiple Datasets
========================================================
class: small-code

```r
ggplot()+
  geom_point(data=iris, aes(Sepal.Length, Sepal.Width))+
  geom_smooth(data=iris, aes(Sepal.Length, Sepal.Width ))
```

![plot of chunk unnamed-chunk-30](ggplot-figure/unnamed-chunk-30-1.png)

ggplot2 Basics: Summarizing Data with Boxplots
========================================================
class: small-code

```r
ggplot(data=iris, aes(Species, Sepal.Width))+
  geom_jitter(alpha=0.2)+ geom_boxplot()
```

![plot of chunk unnamed-chunk-31](ggplot-figure/unnamed-chunk-31-1.png)
ORDER MATTERS!

ggplot2 Basics: Faceting Data
========================================================
class: small-code

```r
ggplot(data=iris, aes(Sepal.Length, Sepal.Width))+
  geom_jitter(alpha=0.2)+ geom_smooth()+
  facet_grid(Species~.)
```

![plot of chunk unnamed-chunk-32](ggplot-figure/unnamed-chunk-32-1.png)

ggplot2 Basics: Maps
========================================================
class: small-code

```r
nz <- map_data("nz")
ggplot(nz, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black")+
  coord_cartesian()
```

![plot of chunk unnamed-chunk-33](ggplot-figure/unnamed-chunk-33-1.png)

ggplot2 Basics: Maps
========================================================
class: small-code

```r
data("world.cities") 
nz.city <- world.cities %>% filter(country.etc=="New Zealand")
ggplot(data=nz, aes(long, lat)) +
  geom_polygon(aes(group = group),fill = "white", colour = "black") +
  geom_point(data=nz.city, aes(long, lat, size = pop)) +
  coord_cartesian()
```

![plot of chunk unnamed-chunk-34](ggplot-figure/unnamed-chunk-34-1.png)
