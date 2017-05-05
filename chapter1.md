---
title       : Starting with data
description : In these exercises, we'll import a dataset containing ecological data of animal species and weights. We'll then explore the data!
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


--- type:NormalExercise lang:r xp:100 skills:1 key:e619cd064b
## Importing your data and first views

In this exercise, you'll import your ecological dataset. After doing so, you'll check out the first rows using the function `head()`. Make sure to read the information that this function call outputs to your console to get a first idea of what your data looks like. Happy importing!

*** =instructions
- Download the file from `"https://ndownloader.figshare.com/files/2292169"` to the location `"data/portal_data_joined.csv"`.
- Import the file from your local file system to a dataframe called `surveys`.
- Check out the first 5 rows of your data using the function `head()`.

*** =hint


*** =pre_exercise_code
```{r}
#Create dir for datasets:
dir.create("data")
```

*** =sample_code
```{r}
# Download the file to your local file system
download.file("https://ndownloader.figshare.com/files/2292169",
              "data/portal_data_joined.csv")

# Import the file into a dataframe: surveys              
surveys <- read.csv('data/portal_data_joined.csv')

# Check out your data!
head(surveys)

```

*** =solution
```{r}
# Download the file to your local file system
download.file("https://ndownloader.figshare.com/files/2292169",
              "data/portal_data_joined.csv")

# Import the file into a dataframe: surveys              
surveys <- read.csv('data/portal_data_joined.csv')

# Check out your data!
head(surveys)

```

*** =sct
```{r}
test_function_v2('download.file', args=c('url', 'destfile'))

test_correct(
    test_object('surveys'), 
    test_function_v2('read.csv', args =c('file')))

ex() %>% check_function('head') %>% 
         check_arg('x') %>% 
         check_equal('Try using `head(surveys)`.')


success_msg("Good work! Don't forget to look at the output of your work in the console and see what you can notice about the dataset that you have imported: what are the column names? What are the values?")
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:739f24d293
## Inspecting data.frame objects

In the previous exercise, you checked out your data by using the function `head()` to display the first five rows of your data. Here you'll use `str()` to dive deeper into the dataset, which is already loaded into `surveys`. In the console provided, use `str()` on `surveys`, check out the output and answer the following questions: what is the class of the object `surveys`? How many rows and how many columns are in this object? How many species have been recorded during these surveys?

[HBA] TBD: incorrect solutions [/HBA]


*** =instructions
- `surveys` is of class `data.frame`, has 13 rows, 34,786 columns and 40 species have been recorded.
- `surveys` is of class `record_id`, has 13 rows, 34,786 columns and 40 species have been recorded.
- `surveys` is of class `data.frame`, has 34,786 rows,  columns and 40 species have been recorded.
- `surveys` is of class `data.frame`, has 34,786 rows,  columns and 26 species have been recorded.

*** =hint

*** =pre_exercise_code
```{r}
dir.create("data")

# Download the file to your local file system
download.file("https://ndownloader.figshare.com/files/2292169",
              "data/portal_data_joined.csv")

# Import the file into a dataframe: surveys              
surveys <- read.csv('data/portal_data_joined.csv')
```

*** =sct
```{r}
test_mc(correct = 3, 
        feedback_msgs = c("Incorrect. You may have mistaken rows for columns: check the output of `str(surveys)` again, remembering that the number of rows is the number of observations and the number of of columns is the number of variables.",
                          "Incorrect: `surveys` is not of class `record_id`. The first thing `str(surveys)` reports is the class.",
                          "Correct! Check out the output of `str(surveys)` more closely and see what other information you clean glean about the dataset there.",
                          "Incorrect: 26 genera (plural of genus!) have been recorded, not 26 species."))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:6691e9ae4e
## Data.frame challenge (1)


*** =instructions

* Create a `data.frame` (`surveys_200`) containing only the observations from row 200 of the `surveys` dataset.

*** =hint

*** =pre_exercise_code
```{r}
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")
```

*** =sample_code
```{r}

```

*** =solution
```{r}
surveys_200 <- surveys[200,]
```

*** =sct
```{r}
test_object('surveys_200')
```

--- type:NormalExercise lang:r xp:100 skills:1 key:3c3adfdbd5
## Data.frame challenge (2)

Notice how nrow() gave you the number of rows in a data.frame?

*** =instructions

* Use that number to pull out just that last row in the data frame
* Compare that with what you see as the last row using `tail()` to make sure it’s meeting expectations.
* Pull out that last row using `nrow()` instead of the row number
* Create a new data frame object (`surveys_last`) from that last row


*** =hint

*** =pre_exercise_code
```{r}
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")
```

*** =sample_code
```{r}
# use last row number to get last row


# use tail to get last row


# use nrow to pull out last row directly


# create new object (surveys_last) from last row

```

*** =solution
```{r}
# use last row number to get last row
surveys[34786,]

# use tail to get last row
tail(surveys, 1)

# use nrow to pull out last row directly
surveys[nrow(surveys),]

# create new object (surveys_last) from last row
surveys_last <- surveys[34786,]

```

*** =sct
```{r}
# MC-Note: this test might not be very robust
test_student_typed('surveys[34786,]')

test_function_v2('tail', args = c('x', 'n'))

# MC-Note: this test might not be very robust
test_student_typed('surveys[nrow(surveys),]')

test_object('surveys_last')
```

--- type:NormalExercise lang:r xp:100 skills:1 key:9ac7c84efa
## Data.frame challenge (3)


*** =instructions

* Use nrow() to extract the row that is in the middle of the data frame. Store the content of this row in an object named `surveys_middle`.

*** =hint

*** =pre_exercise_code
```{r}
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")
```

*** =sample_code
```{r}

```

*** =solution
```{r}
n_middle <- nrow(surveys) / 2
surveys_middle <- surveys[n_middle, ]
```

*** =sct
```{r}
test_function_v2('nrow')
test_object('surveys_middle', incorrect_msg = 'Did you use `nrow(surveys) / 2` to find the index of the middle row?')
```

--- type:NormalExercise lang:r xp:100 skills:1 key:4944bab8e0
## Data.frame challenge (4)

[MC] could break this exercise into smaller steps [/MC]

Recall that `-` can be used to exclude rows.

For example, 

```
surveys[-c(1:5),]
```

returns all but the first 5 rows of `surveys`.

*** =instructions

* Combine `nrow()` with the `-` notation above to reproduce the behavior of `head(surveys)` keeping just the first through 6th rows of the surveys dataset.
* Store the content of your new `data.frame` as surveys_first

*** =hint

*** =pre_exercise_code
```{r}
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")
```

*** =sample_code
```{r}

```

*** =solution
```{r}
surveys_first <- surveys[-c(6:nrow(surveys)), ]
```

*** =sct
```{r}
# makes sure they used nrow (but doesn't check how they used it)
test_function_v2('nrow')
# makes sure they typed a minus sign somewhere
test_student_typed('-', not_typed_msg = "Did you use `-` to remove all rows past the 6th?")

test_object('surveys_first')
```

--- type:NormalExercise lang:r xp:100 skills:1 key:cbfadda567
## Factor challenge (1)


*** =instructions

- Rename “F” and “M” to “female” and “male” respectively.

*** =hint

*** =pre_exercise_code
```{r}
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")
```

*** =sample_code
```{r}
# surveys has already been defined for you
sex <- surveys$sex
levels(sex)[1] <- "missing"

# Rename F and M


```

*** =solution
```{r}
# surveys has already been defined for you
sex <- surveys$sex
levels(sex)[1] <- "missing"

# Rename F and M
levels(sex)[2:3] <- c("Female", "Male")

```

*** =sct
```{r}
ex() %>% check_expr("levels(sex)") %>% check_output() %>% check_equal()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:df8f896c7f
## Factor challenge (2)


*** =instructions
- Now that we have renamed the factor level to “missing”, can you recreate the barplot such that “missing” is last (after “Male”)?

*** =hint

*** =pre_exercise_code
```{r}
surveys <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3707/datasets/combined.csv")
sex <- surveys$sex
levels(sex) <- c("missing", "Female", "Male")

```

*** =sample_code
```{r}
# sex already has factors renamed to "missing", "Female", "Male"
print(levels(sex))

# create barplot of sex with "missing" last

```

*** =solution
```{r}
# sex already has factors renamed to "missing", "Female", "Male"
print(levels(sex))

# create barplot of sex with "missing" last
sex2 <- factor(sex, levels = c("Female", "Male", "missing"))
plot(sex2)

```

*** =sct
```{r}
ex() %>% 
    check_function('plot') %>%
    check_arg('x') %>%
    check_output("Levels: Female Male missing",
                 fixed = TRUE, 
                 missing_msg = "Are the levels of the factor you passed to plot `Female, Male, missing`, in that order? \
                                See the levels argument of `?factor` for help.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:1b0bd6996f
## stringsAsFactors challenge (1)

We have seen how data frames are created when using the read.csv(), but they can also be created by hand with the data.frame() function. There are a few mistakes in this hand-crafted `data.frame`, can you spot and fix them? Don’t hesitate to experiment!

*** =instructions

- Fix the mistakes in making this `data.frame`

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
animal_data <- data.frame(
        animal=c("dog", "cat", "sea cucumber", "sea urchin"),
        feel=c("furry", "squishy", "spiny"),
        weight=c(45, 8 1.1, 0.8)
        )
```

*** =solution
```{r}
animal_data <- data.frame(
        animal=c("dog", "cat", "sea cucumber", "sea urchin"),
        feel=c("furry", "furry", "squishy", "spiny"),
        weight=c(45, 8, 1.1, 0.8)
        )
```

*** =sct
```{r}
# MC-note: need to check SCT
test_correct(test_error(), {
    test_student_typed("8, 1.1", not_typed_msg = "Does your weight row use commas correctly?")
    test_student_typed('"furry", "furry"', not_typed_msg = "Does your feel row have one entry for each animal")
    })
```


--- type:NormalExercise lang:r xp:100 skills:1 key:dce923f581
## stringsAsFactors challenge (2)

[MC-note] might be better doing part as multiple choice?

*** =instructions

Can you predict the class for each of the columns in the following example? Check your guesses using `str(country_climate)`

* Are they what you expected? Why? Why not?
* What would have been different if we had added stringsAsFactors = FALSE to this call?
* Correct the data.frame function call below so that `temperature`, `northern_hemisphere` and `has_kangaroo` are not represented as factors.


*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
country_climate <- data.frame(
       country=c("Canada", "Panama", "South Africa", "Australia"),
       climate=c("cold", "hot", "temperate", "hot/temperate"),
       temperature=c(10, 30, 18, "15"),
       northern_hemisphere=c(TRUE, TRUE, FALSE, "FALSE"),
       has_kangaroo=c(FALSE, FALSE, FALSE, 1)
       )

```

*** =solution
```{r}
country_climate <- data.frame(
       country=c("Canada", "Panama", "South Africa", "Australia"),
       climate=c("cold", "hot", "temperate", "hot/temperate"),
       temperature=c(10, 30, 18, 15),
       northern_hemisphere=c(TRUE, TRUE, FALSE, FALSE),
       has_kangaroo=c(FALSE, FALSE, FALSE, TRUE)
       )
       
```

*** =sct
```{r}
ex() %>% check_object('country_climate') %>% {
    for (colname in c('temperature', 'northern_hemisphere', 'has_kangaroo')) {
        check_column(., colname)
        check_expr(., sprintf("class(country_climate$%s)", colname)) %>% 
            check_output() %>%
            check_equal()
    }
}

```
