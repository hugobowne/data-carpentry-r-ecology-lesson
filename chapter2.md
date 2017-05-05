---
title       : Manipulating data frames
description : Insert the chapter description here
--- type:NormalExercise lang:r xp:100 skills:1 key:cbc1898792
## Pipes challenge


*** =instructions

- Using pipes, subset the survey data to include individuals collected before 1995 and retain only the columns year, sex, and weight.


*** =hint

*** =pre_exercise_code
```{r}
library(dplyr)
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")
```

*** =sample_code
```{r}

```

*** =solution
```{r}
surveys %>% 
    filter(year < 1995) %>%
    select(year, sex, weight)
```

*** =sct
```{r}
e
ex() %>% 
    check_function('filter') %>% 
    check_code(c("year < 1995", "year <= 1996",
                 "1995 > year", "1996 >= year"),
               fixed = TRUE)
    
ex() %>% check_function('select') %>% {
    check_code(., "year")
    check_code(., "sex")
    check_code(., "weight")
    }
```

--- type:NormalExercise lang:r xp:100 skills:1 key:30bfe02d63
## Mutate challenge


*** =instructions

Create a new data frame, named `hindfoot`, from the survey data that meets the following criteria:

- Contains only the `species_id` column and a new column called `hindfoot_half`.
- `hindfoot_half` contains values that are half the `hindfoot_length` values. 
- `hindfoot_half` has no NAs and all values are less than 30.

**Hint:** Think about how the commands should be ordered to produce this data frame!

*** =hint

*** =pre_exercise_code
```{r}
library(dplyr)
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")

```

*** =sample_code
```{r}

```

*** =solution
```{r}
hindfoot <- surveys %>%
    mutate(hindfoot_half = hindfoot_length / 2) %>%
    filter(!is.na(hindfoot_half) | hindfoot_half >= 30) %>%
    select(species_id, hindfoot_half)
```

*** =sct
```{r}
test_correct(ex() %>% check_object('hindfoot') %>% check_equal(), {
    ex() %>% check_function('mutate')
    ex() %>% check_function('filter')
    ex() %>% check_function('select')
})
```

--- type:NormalExercise lang:r xp:100 skills:1 key:d814d055fc
## Split-apply-combine challenge (1)


*** =instructions

- How many individuals were caught in each plot_type surveyed?

*** =hint

*** =pre_exercise_code
```{r}
library(dplyr)
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")

```

*** =sample_code
```{r}

```

*** =solution
```{r}
surveys %>%
  group_by(plot_type) %>%
  tally()
```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:87223a9f01
## Split-apply-combine challenge (2)

[MC-Note] 
It's not clear to me what the answer is to this challenge.
Should students filter groups of species_id with no `hindfoot_length` measures?

*** =instructions

- Use `group_by()` and `summarize()` to find the mean, min, and max hindfoot length for each species (using `species_id`).

*** =hint

*** =pre_exercise_code
```{r}
library(dplyr)
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")

```

*** =sample_code
```{r}

```

*** =solution
```{r}
surveys %>% 
    group_by(species_id) %>%
    summarize(mean(hindfoot_length, na.rm = TRUE), 
              min(hindfoot_length, na.rm = TRUE), 
              max(hindfoot_length, na.rm = TRUE))
```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:df9352def1
## Split-apply-combine challenge (3)


*** =instructions

- What was the heaviest animal measured in each year? Return the columns `year`, `genus`, `species_id`, and `weight`.

*** =hint

*** =pre_exercise_code
```{r}
library(dplyr)
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")

```

*** =sample_code
```{r}
```

*** =solution
```{r}
surveys %>%
    group_by(year) %>%
    filter(weight < max(weight)) %>%
    select(year, genus, species_id, weight)

```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:72bf13bbef
## Split-apply-combine challenge (4)


*** =instructions

- You saw above how to count the number of individuals of each sex using a combination of `group_by()` and `tally()`. How could you get the same result using `group_by()` and `summarize()`?


*** =hint

- Check out the `n` function, by running `?n` in the console.

*** =pre_exercise_code
```{r}
library(dplyr)
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")

```

*** =sample_code
```{r}

```

*** =solution
```{r}
surveys %>%
    group_by(sex) %>%
    summarize(n = n())
```

*** =sct
```{r}

```
