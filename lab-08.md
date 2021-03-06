Lab 08 - Conveying the right message through visualisation
================
Lindley Slipetz
3/26/2021

### Load packages and data

``` r
library(tidyverse) 
library(wesanderson)
```

### Exercise 1

We’re going to make a tibble of dates, counts, and mask/no mask.
Honestly, what took me so long on this lab was just figuring out what in
the world that graph was trying to convey.

``` r
covid <- tribble(
  ~date, ~count, ~mask,
  "7/13/2020", 23, "yes",
  "7/14/2020", 20, "yes", 
  "7/15/2020", 20, "yes",
  "7/16/2020", 20, "yes",
  "7/17/2020", 20, "yes", 
  "7/18/2020", 20, "yes",
  "7/19/2020", 20, "yes",
  "7/20/2020", 20, "yes", 
  "7/21/2020", 21, "yes",
  "7/22/2020", 21, "yes",
  "7/23/2020", 20, "yes",
  "7/24/2020", 20, "yes",
  "7/25/2020", 20, "yes",
  "7/26/2020", 19, "yes", 
  "7/27/2020", 18, "yes",
  "7/28/2020", 16, "yes",
  "7/29/2020", 16, "yes", 
  "7/30/2020", 16, "yes",
  "7/31/2020", 16, "yes",
  "8/1/2020", 16, "yes", 
  "8/2/2020", 16, "yes",
  "8/3/2021", 16, "yes",
  "7/13/2020", 9, "no",
  "7/14/2020", 9, "no", 
  "7/15/2020", 10, "no",
  "7/16/2020", 10, "no",
  "7/17/2020", 9, "no", 
  "7/18/2020", 9, "no",
  "7/19/2020", 9, "no",
  "7/20/2020", 9, "no", 
  "7/21/2020", 9, "no",
  "7/22/2020", 9, "no",
  "7/23/2020", 9, "no",
  "7/24/2020", 9, "no",
  "7/25/2020", 10, "no",
  "7/26/2020", 10, "no", 
  "7/27/2020", 9, "no",
  "7/28/2020", 9, "no",
  "7/29/2020", 9, "no", 
  "7/30/2020", 10, "no",
  "7/31/2020", 9, "no",
  "8/1/2020", 9, "no", 
  "8/2/2020", 9, "no",
  "8/3/2021", 9, "no",
   
)
```

### Exercise 2

``` r
covid %>%
ggplot(aes(x = date, y = factor(count), color = mask, group = mask)) + 
  geom_line() +
  geom_point() +
  theme(axis.text.x = element_text(angle = 90)) +
  scale_y_discrete(name ="Rolling Average Daily Cases per 100k", 
                    labels = c("4" = 4,"8" = 8,
  "12" = 12,"16" = 16,"20" = 20, "24" = 24)) +
  labs(x = "Date", title = "Kansas Covid-19 7-Day Rolling Average of Daily Cases per 100k") +
  scale_color_manual(values=wes_palette(n=2, name="BottleRocket2"))
```

![](lab-08_files/figure-gfm/graph-1.png)<!-- -->

### Exercise 3

It shows that the no mask cases are actually much lower, which was not
clear on the other graph due to the weird y-axes. We also see the nearly
steady number of cases with no mask and the decrease of cases for mask.

### Exercise 4

What the data tells us is over time, wearing a mask decreases the number
of cases of Covid per 100k. Not wearing a mask results in a steady
number of cases.

One might claim that, because the number of cases is less for not
wearing a mask, it’s better to not wear a mask. I am suspicious of that
claim. My guess would be less people don’t wear masks, so there would be
less cases for no mask simply because there’s less people in that group.
To test this perhaps we could look at the percentage of cases within the
two groups to see if it is more likely to get Covid with or without a
mask.
