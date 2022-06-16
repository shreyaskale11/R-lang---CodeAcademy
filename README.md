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










