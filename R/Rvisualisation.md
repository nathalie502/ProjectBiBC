---
title: "R Notebook"
output: html_notebook
---

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you execute code within the notebook, the results appear beneath the code. 

Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Ctrl+Shift+Enter*. 

```{r}
plot(cars)
```

Add a new chunk by clicking the *Insert Chunk* button on the toolbar or by pressing *Ctrl+Alt+I*.

When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the *Preview* button or press *Ctrl+Shift+K* to preview the HTML file).

The preview shows you a rendered HTML copy of the contents of the editor. Consequently, unlike *Knit*, *Preview* does not run any R code chunks. Instead, the output of the chunk when it was last run in the editor is displayed.


# Data extraction, transformation and loading

## Packages loaded

#Data visualisation
```{r}
if (!require("ggplot2")) {
  install.packages("ggplot2", dependencies = TRUE)
  library(ggplot2)
  citation("ggplot2")
}
```

## Data loading
```{r}
insurance = read.csv("Data/insurance.csv")
head(insurance)
```

# Visualization
```{r}
library(ggplot2)
library(gridExtra)

bmi_plot = qplot(bmi, charges, data = insurance, xlab = "BMI", ylab = "Charges") + geom_vline(xintercept = 18.5, color = "red") + geom_vline(xintercept = 24.9, color = "red")
bmi_plot
```

```{r}
age_plot = qplot(age, charges, data = insurance, xlab = "Age", ylab = "Charges", col = sex)
sex_plot = qplot(sex, charges, data = insurance, xlab = "Age", ylab = "Charges")

plot1 = grid.arrange(bmi_plot, age_plot, sex_plot, ncol=1 )
plot1
```



```{r}
sex_boxplot = ggplot(insurance, aes(x=sex, y=charges)) + geom_boxplot()
region_boxplot = ggplot(insurance, aes(x=region, y=charges)) + geom_boxplot() + theme(axis.text.x = element_text(angle = 90, hjust = 1))
children_boxplot = ggplot(insurance, aes(x=as.factor(children), y=charges)) + geom_boxplot() + labs(x="# of children")
smoker_boxplot = ggplot(insurance, aes(x=smoker, y=charges)) + geom_boxplot()

grid.arrange(children_boxplot, sex_boxplot, smoker_boxplot, region_boxplot, ncol=2 )
```



