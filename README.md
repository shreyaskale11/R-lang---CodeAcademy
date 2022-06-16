# R-lang---CodeAcademy



```
create_sale_summary_report <- function(df_data) {

  # Process data  

group <- data.frame(Region = df_data$Region, Representative = df_data$Representative, 
                    Total_sales = df_data$Total_sales )
# sorting the sub and marks.
sorted_group <- group[order(group$Region, -group$Total_sales),]
  
# removing duplicates from the sorted sub column
ans <- sorted_group[!duplicated(sorted_group$Region),]

  # Return result
}
# DO NOT CHANGE THIS CODE
```


In R, vectors are a list-like structure that contain items of the same data type.
```{r}
phone <- c(25,255,2525)
typeof(phone)
print(length(phone))
```
When we use the & operator, we are checking that two things are true:
If we only care about either condition being true, we can use the | operator:

```
sort(c(2,4,10,5,1)); # Outputs c(1,2,4,5,10)
length(c(2,4,10,5,1)); # Outputs 5
sum(5,15,10) #Outputs 30
```

The pipe operator, or %>%, helps increase the readability of data frame code by piping the value on its left into the first argument of the function that follows it. 

```
df %>%
  head()
```
Filter the rows of artists where the genre is 'Rock' and spotify_monthly_listeners is greater than 20000000. Save the result to popular_rock_groups, and view it.
```
popular_rock_groups<-artists  %>%
  filter(genre == 'Rock'&spotify_monthly_listeners>20000000 )
popular_rock_groups
```

```
korea_or_before_2000<-artists  %>%
  filter(country == 'South Korea' | year_founded  < 2000)
korea_or_before_2000

```

```{r}
# filter rows with not !
not_rock_groups<-artists %>% filter(!(genre == 'Rock'))

not_rock_groups
```

```
group_asc<- artists %>% arrange(group)
group_asc

```

```{r}
# arrange rows in descending order
youtube_desc<- artists %>% arrange(desc(youtube_subscribers))
youtube_desc
```
Update the call to mutate() by adding one last argument that adds a new column rank_change_13_to_16 that is the change in rank from 2013 to 2016 (rank_2016 - rank_2013).
```
dogs <- dogs %>%
  mutate(avg_height = (height_low_inches + height_high_inches)/2,avg_weight = (weight_low_lbs  + weight_high_lbs)/2,rank_change_13_to_16 = (rank_2016 - rank_2013) )
head(dogs)
```
dplyr’s transmute() function will add new columns while dropping the existing columns that may no longer be useful for your analysis. 
```
dogs <- dogs %>%
  transmute(breed = breed,avg_height = (height_low_inches + height_high_inches)/2,
         avg_weight = (weight_low_lbs + weight_high_lbs)/2,
        rank_change_13_to_16 = rank_2016 - rank_2013)
head(dogs)
```
save col name 
```
new_col_names <- colnames(dogs)
new_col_names 
```
Update the name of avg_height to avg_height_inches, avg_weight to avg_weight_lbs, and rank_change_13_to_16 to popularity_change_13_to_16. Save the updated data frame to dogs.
```
dogs <- dogs %>%
rename(avg_height_inches = avg_height , 
 avg_weight_lbs = avg_weight , 
  popularity_change_13_to_16 =rank_change_13_to_16 )
```

You have 10 different files containing 100 students each. These files follow the naming structure:
exams_0.csv
exams_1.csv
… up to exams_9.csv
You are going to read each file into an individual data frame and then combine all of the entries into one data frame.
First, create a variable called student_files and set it equal to the list.files() of all of the CSV files we want to import.

Read each file in student_files into a data frame using lapply() and save the result to df_list.

Concatenate all of the data frames in df_list into one data frame called students.
```
student_files  <- list.files(pattern = "exams_.*csv")
df_list <- lapply(student_files,read_csv)
students  <- bind_rows(df_list)
nrow_students <- nrow(students)
```
There is a column for the scores on the fractions exam, and a column for the scores on the probability exam.
We want to make each row an observation, so we want to transform this table to look like:
Use gather to create a new table (still called students) that follows this structure. Then view the head() of students.

We want to turn fractions and probability into variables, so those columns are the first two arguments to gather().
We want to call that new column exam, so that’s our key.
The values previously held in fractions and probability, we want to store in a column called score, so that’s the value.
```
original_col_names <- colnames(students)

students<- students %>%
   gather( 'fractions', 'probability' ,key = 'exam',value='score')
   head(students)
gathered_col_names <- colnames(students )
exam_counts <- students%>%
count(exam)
exam_counts 
```
