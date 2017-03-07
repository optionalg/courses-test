---
title       : Testing PlainMultipleChoiceExercise
description : Testing PlainMultipleChoiceExercise

--- type:PlainMultipleChoiceExercise xp:50 key:916f4a9641
## Plain Multiple Choice Exercise

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

*** =instructions
- Ronald McDonald
- Ronald Reagan
- Donald Knuth
- Ross Ihaka

*** =sct
```{r}
test_mc(2)
```

--- type:NormalExercise xp:100
## Ggplot Exercise

For Chester

*** =instructions
- None provided

*** =pre_exercise_code
```{r}
library(fivethirtyeight)
library(dplyr)
library(ggplot2)
data(bechdel)
year_bins <- c("1970-'74", "1975-'79", "1980-'84", "1985-'89",
  "1990-'94", "1995-'99", "2000-'04", "2005-'09",
  "2010-'13")
bechdel <- bechdel %>%
  mutate(five_year = cut(year,
    breaks = seq(1969, 2014, 5),
    labels = year_bins)) %>%
  mutate(clean_test = factor(clean_test,
    levels = c("nowomen", "notalk", "men", "dubious", "ok")))
```

*** =sample_code
```{r}
library(fivethirtyeight)
library(ggplot2)

```

*** =solution
```{r}
library(fivethirtyeight)
library(ggplot2)
ggplot(data = bechdel,
  mapping = aes(x = five_year, fill = binary)) +
  geom_bar(position = "fill", color = "white")
```

*** =sct
```{r}
```
