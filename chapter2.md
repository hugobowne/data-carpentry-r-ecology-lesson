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
