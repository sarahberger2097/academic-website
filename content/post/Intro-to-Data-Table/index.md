---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Introduction to data.table in R"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-12-05T11:49:47-05:00
lastmod: 2020-12-05T11:49:47-05:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
One of the most exciting packages in the R universe is data.table. This package allows you to create data.table objects as an alternative to data.frame. The benefit of using data.table is the speed and efficiency when working with large datasets, and a concise syntax that can be really easy to use once you get used to it. 

### Load data.table package and dataset

Lets first start with installing and loading the package. For this demonstration we will use the iris dataset that is preinstalled in R. 

```{r setup}
install.packages("data.table")
library(data.table)

data = setDT(copy(iris)) 
#note we have to create a copy because iris is built-in to R and thus not modifiable
```

In this case we didn't import our data from a csv file, but if you have a large dataset that you need to import, the `fread()` function from data.table allows for extremely quick importing of data from either a csv file or a URL. 

Also, here we converted an existing data frame to a data table object using `setDT()`. We could also use `as.data.frame()` for an existing object, or create our own data table by inputting data using `data.table()`

### Data Table Syntax

The main syntax that data table uses is the `DT[i, j, by]`

{{< figure src="ijby.png" >}}

This syntax allows for data to be manipulated extremely easily and in only one line of code! It may seem pretty foreign, so lets go through some explanations and examples. 

#### Filter rows

Let's say we only want the 15th row of our dataset. Or only data for flowers of the versicolor species. Or only data for the versicolor species with a sepal width less than 3. This is all easy to do in the "i" part of a data table.
```{r filter}
#15th row

row_15 <- data[15]
row_15
```
{{< figure src="row_15.png" >}}

```{r filter2}
# versicolor species
versicolor <- data[Species == "versicolor"]
head(versicolor)
```
{{< figure src="verisocolor.png" >}}
```{r filter3}
#versicolor species with a sepal width less than 3
versicolor_sepal3 <- data[Species == "versicolor" & Sepal.Width < 3]
head(versicolor_sepal3)

```
{{< figure src="verisocolor_sepal3.png" >}}

##### Other special operators include %in% and %between%

```{r rows2}

setosa_virginica <- data[Species %in% c("setosa", "virginica")]

pl_1.2_1.6 <- data[Petal.Length %between% c(1.2, 1.6)]

```


#### Working with columns

Let say you want all rows, but only the Species and sepal width columns. Note that you will leave the i section empty by just adding a comma before the j section.

```{r column}

species_sepalw <- data[, c("Species", "Sepal.Width")]

#an alternate way of writing a list in data.table is by using .() 
species_sepalw <- data[, .(Species, Sepal.Width)]
head(species_sepalw)
```
{{< figure src="species_sepalw.png" >}}

It is also easy to do computations on columns in data.table. Let's find the median sepal width

```{r column2}

median_sw <- data[, median(Sepal.Width)]
median_sw 

```
{{< figure src="median_sw.png" >}}

#### The := Operator: Creating New Columns

Using the ":=" operator in the j section allows you to create new columns using existing ones. When doing this, you don't have to assign the result to a new object, because the column will be directly added to the current data table. For example, let's compute sepal area (length x width)

```{r column3}

data[, Sepal.Area := Sepal.Length * Sepal.Width]
head(data)

```
{{< figure src="sepal.area.png" >}}

Notice how the new column name is on the left of the operator, and the operation is on the right.


#### Group by variables

We can use the last section to group variables using "by". For example, we can get the mean Sepal length by species.

```{r by}

mean_by_species <- data[, .(mean.sepal.length = mean(Sepal.Length)), by = Species]
mean_by_species

```
{{< figure src="mean_by_species.png" >}}

You can also create a new column by using the := operator, that is grouped by a variable (or multiple variables).

```{r by2}

data[, mean.sepal.width := mean(Sepal.Width), by = Species]

```
{{< figure src="mean.sepal.width.png" >}}

### The .N special symbol 

Using the .N symbol means the number of rows present. This can function similarly to nrows(). For example, here we can get the number of rows where the sepal width is less than 3 and sepal length is less than 5.

```{r .N}

less_3_5 <- data[Sepal.Width < 3 & Sepal.Length < 5, .N]
less_3_5

```
{{< figure src="less_3_5.png" >}}

.N becomes really useful when you want to also use "by". For example let's get the number of observations per species.

```{r .N2}

obs <- data[, .N, by = Species]
obs

```
{{< figure src="obs.png" >}}

There are lots of other features of data.table that make it useful to use for data manipulation, but here I have gone over the basics and the operations that I use most often. If you are looking for more resources on using data.table you can:

1. Visit the [CRAN](https://cran.r-project.org/web/packages/data.table/data.table.pdf)
2. Complete a datacamp tutorial. Here is one called [Data Manipulation with data.table in R](https://learn.datacamp.com/courses/data-manipulation-with-datatable-in-r)
3. Check out the CRAN Vignette called [Introduction to data.table](https://cran.r-project.org/web/packages/data.table/vignettes/datatable-intro.html)

Happy analyzing! 

