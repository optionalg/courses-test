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

--- type:NormalExercise xp:100 key:6224dcc129
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
test_library_function("fivethirtyeight")
test_library_function("ggplot2")
test_or({
  # match original solution
  ggplot_fun <- ex() %>% check_function("ggplot")
  ggplot_fun %>% check_arg("data") %>% check_equal(eval = FALSE)
  ggplot_fun %>% check_arg("mapping")
  aes_fun <- ex() %>% check_function("aes")
  aes_fun %>% check_arg("x") %>% check_equal(eval = FALSE)
  aes_fun %>% check_arg("fill") %>% check_equal(eval = FALSE)
  geom_bar_fun <- ex() %>% check_function("geom_bar")
  geom_bar_fun %>% check_arg("position") %>% check_equal()
  geom_bar_fun %>% check_arg("color") %>% check_equal()
}, {
  # match solution 1:
  sol_code1 <- 'ggplot(data = bechdel, mapping = aes(x = five_year)) + geom_bar(position = "fill", color = "white", mapping = aes(fill = binary))'
  alt_ex_1 <- ex() %>% override_solution(sol_code1)

  ggplot_fun <- alt_ex_1 %>% check_function("ggplot")
  ggplot_fun %>% check_arg("data") %>% check_equal(eval = FALSE)
  ggplot_fun %>% check_arg("mapping")
  aes_fun <- alt_ex_1 %>% check_function("aes")
  aes_fun %>% check_arg("x") %>% check_equal(eval = FALSE)
  geom_bar_fun <- alt_ex_1 %>% check_function("geom_bar")
  geom_bar_fun %>% check_arg("position") %>% check_equal()
  geom_bar_fun %>% check_arg("color") %>% check_equal()
  geom_bar_fun %>% check_arg("mapping")
  alt_ex_1 %>% check_function("aes", index = 2) %>% check_arg("fill") %>% check_equal(eval = FALSE)
}, {
  # Match solution 2:
  sol_code2 <- 'ggplot(data = bechdel) + geom_bar(position = "fill", color = "white", mapping = aes(x = five_year, fill = binary))'
  alt_ex_2 <- ex() %>% override_solution(sol_code2)
  
  alt_ex_2 %>% check_function("ggplot") %>% check_arg("data") %>% check_equal(eval = FALSE)
  geom_bar_fun <- alt_ex_2 %>% check_function("geom_bar")
  geom_bar_fun %>% check_arg("position") %>% check_equal()
  geom_bar_fun %>% check_arg("color") %>% check_equal()
  geom_bar_fun %>% check_arg("mapping")
  aes_fun <- alt_ex_2 %>% check_function("aes")
  aes_fun %>% check_arg("x") %>% check_equal(eval = FALSE)
  aes_fun %>% check_arg("fill") %>% check_equal(eval = FALSE)
})
# Match solution 3: todo!

success_msg("You are awesome!")
```
