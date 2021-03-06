---
title: "CASE STUDY 2"
author: "Austin Ith"
date: "January 18, 2020"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---





## Background

I found this case study challenging, yet fun to complete. I learned a lot about the functionality and capabilities of ggplot. I found the first image shown below to be fairly straight and completed it quickly, taking things one step at the time. 

The second image, however, gave me a little more trouble. I was able to get the basic's set up, but it took a good deal of time to figure out how to add in the second dataset. Once the second dataset was added, I had issues fixing the Population scale to accommodate both data sets but learned that you have to add the size aesthetic to both geom_points. 

Overall, I really enjoyed working on this project. See completed graphic's below.

## Images


```r
gapminder <- gapminder %>% 
  filter(country != "Kuwait") 

gapminder %>% 
  ggplot(aes(x = lifeExp, y = gdpPercap)) +
  geom_point(aes(color = continent, size = pop / 100000)) +
  facet_grid(~year) +
  theme_bw() + 
  labs(x = "Life Expectancy", 
       y = "GDP per capita",
       color = "Continent",
       size = "Population (100K)") +
  scale_y_continuous(trans = "sqrt")
```

![](Case-Study-2_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
ggsave("Plot1.png", plot = last_plot(), width = 15, units = "in")
```




```r
gapminder_mean <- gapminder %>% 
  group_by(continent, year) %>% 
  summarise(mean = weighted.mean(gdpPercap),
            pop1 = sum(pop)/100000)

ggplot(data = gapminder, aes(x= year, y=gdpPercap, color = continent)) +
geom_point(data = gapminder, aes(size = pop / 100000)) +
geom_line(data = gapminder, aes(group=country)) +
geom_point(data = gapminder_mean, aes(x= year, y = mean, size = pop1), color = "black") +
geom_line(data = gapminder_mean, aes(x=year, y = mean), color = "black") +
facet_grid(~ continent) +
theme_bw() +
labs(x = "Year", 
      y = "GDP per capita",
      color = "Continent",
      size = "Population (100K)")
```

![](Case-Study-2_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
ggsave("Plot2.png", plot = last_plot(), width = 15, units = "in")
```

