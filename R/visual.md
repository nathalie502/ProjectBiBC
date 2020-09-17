R Notebook for visualisations
================

-   [Including Plots](#including-plots)
-   [Data extraction, transformation and loading](#data-extraction-transformation-and-loading)
    -   [Packages loaded](#packages-loaded)
    -   [Data loading](#data-loading)
-   [Visualization](#visualization)

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

Including Plots
---------------

You can also embed plots, for example:

![](visual_files/figure-markdown_github/pressure-1.png)

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.

Data extraction, transformation and loading
===========================================

Packages loaded
---------------

Data loading
------------

``` r
insurance = read.csv("c:/users/denat/ProjectBiBC/Data/insurance.csv")
head(insurance)
```

    ##   age    sex    bmi children smoker    region   charges
    ## 1  19 female 27.900        0    yes southwest 16884.924
    ## 2  18   male 33.770        1     no southeast  1725.552
    ## 3  28   male 33.000        3     no southeast  4449.462
    ## 4  33   male 22.705        0     no northwest 21984.471
    ## 5  32   male 28.880        0     no northwest  3866.855
    ## 6  31 female 25.740        0     no southeast  3756.622

Visualization
=============

``` r
library(ggplot2)
library(gridExtra)

bmi_plot = qplot(bmi, charges, data = insurance, xlab = "BMI", ylab = "Charges") + geom_vline(xintercept = 18.5, color = "red") + geom_vline(xintercept = 24.9, color = "red")
```

![](visual_files/figure-markdown_github/bmi_plot-1.png)

``` r
age_plot = qplot(age, charges, data = insurance, xlab = "Age", ylab = "Charges", col = sex)
sex_plot = qplot(sex, charges, data = insurance, xlab = "Age", ylab = "Charges")

plot1 = grid.arrange(bmi_plot, age_plot, sex_plot, ncol=1 )
```

![](visual_files/figure-markdown_github/unnamed-chunk-2-1.png)

``` r
sex_boxplot = ggplot(insurance, aes(x=sex, y=charges)) + geom_boxplot()
region_boxplot = ggplot(insurance, aes(x=region, y=charges)) + geom_boxplot() + theme(axis.text.x = element_text(angle = 90, hjust = 1))
children_boxplot = ggplot(insurance, aes(x=as.factor(children), y=charges)) + geom_boxplot() + labs(x="# of children")
smoker_boxplot = ggplot(insurance, aes(x=smoker, y=charges)) + geom_boxplot()

grid.arrange(children_boxplot, sex_boxplot, smoker_boxplot, region_boxplot, ncol=2 )
```

![](visual_files/figure-markdown_github/unnamed-chunk-3-1.png)
