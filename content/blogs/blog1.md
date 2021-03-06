---
categories:
- ""
- ""
date: "2017-10-31T21:28:43-05:00"
description: "Exploring GDP and Life Expectancy"
draft: false
image: pic10.jpg
keywords: ""
slug: blog1
title: Gapminder
---

Here is a look at the first 20 rows of data in the gapminder dataset, which shows life expectancy, population, and GDP per capita for 142 countries from 1952 to 2007.

```{r}
glimpse(gapminder)
head(gapminder, 20)
```
I have created the `country_data` and `continent_data` for the country and continent from which I am from with the code below
```{r}
country_data <- gapminder %>% 
            filter(country == "United States")
continent_data <- gapminder %>% 
            filter(continent == "Americas")
```
First, I created a plot of life expectancy over time for the United States.
```{r, lifeExp_one_country}
plot1 <- ggplot(data = country_data, mapping = aes(x = year, y = lifeExp)) + 
geom_point() +
geom_smooth(se = FALSE) + 
NULL 
plot1
```
Next, I added a title.
```{r, lifeExp_one_country_with_label}
plot1 <- ggplot(data = country_data, mapping = aes(x = year, y = lifeExp)) + 
geom_point() + 
geom_smooth(se = FALSE) + 
labs(title = "United States Life Expectancy", x = "Year", y = "Years of Age") + 
NULL
plot1
```
Thirdly, I produced a plot for all countries in the Americas.

```{r lifeExp_one_continent}
ggplot(data =  continent_data, mapping = aes(x =  year, y = lifeExp, colour = country)) + 
geom_point() + 
geom_smooth(se = FALSE) + 
NULL
```
Finally, using the original gapminder data, I produced a life expectancy over time graph, grouped by continent. 
```{r lifeExp_facet_by_continent}
ggplot(data = gapminder , mapping = aes(x = year, y = lifeExp, colour = country)) + 
eom_point() +  
geom_smooth(se = FALSE) + 
facet_wrap(~continent) + 
theme(legend.position="none") + 
NULL
```
In general, life expectancy has improved worldwide in the 55 years covered in the data, with a few particular exceptions. Especially in Africa, but also in Asia and the Americas, a few countries experienced severe decreases in their life expectancy that could likely be contributed to a small handful of factors. Many parts of Africa, for example, experienced wars of many varieties during the late 20th century, whether they be revolutions, civil wars, coups, or insurgencies. The same could be said for a similar dip in one country in Asia in the 1970s. Without knowing for sure, I would say that country is Vietnam as it was torn apart by the Vietnam War. There is also a much more gradual curve to one country in the Americas that does not fit the sharp decline seen during warfare. This is a much more difficult label to pin down as gradual social deterioration could apply to many countries in the Western hemisphere, including Venezuela, El Salvador, Honduras, Panama, Colombia, or Nicaragua just to name a few. 