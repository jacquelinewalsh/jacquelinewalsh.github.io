#Background and Interests
I am currently a senior at The George Washington University studying Communication and Journalism. After I finish my undergraduate degree in the next few weeks, I am hoping to be admitted to Northwestern's Sports Journalism Masters program for Fall 2021. I am eager to apply the data journalism expertise I have developed over this semester through this course in my future journalism endeveours involving sports. 

##First R Assignment
Here is a project from an assignment this semester that involved working with Impeachment data.

```markdown
# 1) The column "for_impeachment" indicates whether the member has publicly called for
# an impeachment inquiry. Filter to return only the ones where the answer is NO.    

impeach <-
  filter (impeach, for_impeachment == "NO")
  
# 2) Filter to return only results where a member is both against impeachment, and comes from a 
# district that President Trump won in 2016 (which is noted in the "p16winningparty" column)

impeach <-
  filter (impeach, for_impeachment == "NO") %>%
  filter (p16winningparty == "R")

# 3) Filter for only results where a member is against impeachment, comes from a 
# district that President Trump won in 2016 (which is noted in the "p16winningparty" column),
# and also comes from a district that Mitt Romney won in 2012 ("p12winningparty").

impeach <-
  filter (impeach, for_impeachment == "NO") %>%
  filter (p16winningparty == "R") %>%
  filter (p12winningparty == "R")

# 4) Filter for only results from September 2019 where a member is a YES for impeachment. 

impeach <-
  filter (impeach, date_year == "2019") %>%
  filter (date_month == "9") %>%
  filter (for_impeachment == "YES")

# 4) Filter for only results where a member is a YES for impeachment and is from a district
# where Clinton won more than 70 percent of the vote in 2016 (found in column "clinton_percent")

impeach <-
  filter (impeach, for_impeachment == "YES") %>%
  filter (clinton_percent > "70")


# 5) Sort the entire dataframe based on the percentage of a district that has a 
# bachelor's degree or higher ("pct_bachelors"), from lowest to highest

impeach <-
  arrange (impeach, pct_bachelors, .by_group = TRUE)


# 6) Sort the just those who are NO on impeachment based on the percentage of a district that has a 
# bachelor's degree or higher ("pct_bachelors"), from lowest to highest

impeach <-
  arrange (impeach, pct_bachelors, .by_group = TRUE) %>%
  filter (for_impeachment == "NO") 

# 7) Sort the just those who are NO on impeachment based on the percentage of a district that has a 
# bachelor's degree or higher ("pct_bachelors"), from lowest to highest.
# Then filter those records by only those whose bachelor's percentage is below the national average (found
# in the "pct_bachelors_compared_to_national" column).

impeach <-
  arrange (impeach, pct_bachelors, .by_group = TRUE) %>%
  filter (for_impeachment == "NO") %>%
  filter (pct_bachelors_compared_to_national == "BELOW")

# 8) Filter for only members from New Jersey who are NO on impeachment

impeach <-
  filter (impeach, for_impeachment == "NO") %>%
  filter (state == "NJ")

#Answer = Jefferson Van Drew

# 9) Filter for those who were YES on impeachment, with a declared date prior to 2019. So only
# those with dates before 2019.  Then sort those so that the highest Clinton vote percentages are 
# at the top.   

impeach <-
  arrange (impeach, pct_bachelors, .by_group = TRUE) %>%
  filter (for_impeachment == "YES") %>%
  filter (date_year %in% c("2017", "2018"))

# 10) Answer this question with a single numeric answer, and show the R code you
# used to reach that answer: How many members in the dataset who are holdouts on impeachment
# comes from districts with a GDP below the national figure?

impeach <-
  filter (impeach, for_impeachment == "NO") %>%
  filter (gdp_above_national == "BELOW")

#19 members
```

##Biden Transition Tracking
This project scraped the Biden Transition site and captured what was new, then generated a dynamic report that can be updated multiple times a day as necessary to share information on the status of the transition teams.

See the report here.


```markdown
Syntax highlighted code block

[Link](url) and ![Image](src)
```
