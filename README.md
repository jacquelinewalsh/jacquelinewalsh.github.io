**Background and Interests**

I am currently a senior at The George Washington University studying Communication and Journalism. After I finish my undergraduate degree in the next few weeks, I am hoping to be admitted to Northwestern's Sports Journalism Masters program for Fall 2021. I am eager to apply the data journalism skills I have developed over this semester through this course in my future journalism endeveours involving sports. 

**First R Assignment**

Check out a project from earlier this semester that involved working with Impeachment data.

```markdown
1) The column "for_impeachment" indicates whether the member has publicly called for an impeachment inquiry. Filter to return only the ones where the answer is NO.    

impeach <-
  filter (impeach, for_impeachment == "NO")
  
2) Filter to return only results where a member is both against impeachment, and comes from a district that President Trump won in 2016 (which is noted in the "p16winningparty" column)

impeach <-
  filter (impeach, for_impeachment == "NO") %>%
  filter (p16winningparty == "R")

3) Filter for only results where a member is against impeachment, comes from a district that President Trump won in 2016 (which is noted in the "p16winningparty" column), and also comes from a district that Mitt Romney won in 2012 ("p12winningparty").

impeach <-
  filter (impeach, for_impeachment == "NO") %>%
  filter (p16winningparty == "R") %>%
  filter (p12winningparty == "R")

4) Filter for only results from September 2019 where a member is a YES for impeachment. 

impeach <-
  filter (impeach, date_year == "2019") %>%
  filter (date_month == "9") %>%
  filter (for_impeachment == "YES")

5) Filter for only results where a member is a YES for impeachment and is from a district where Clinton won more than 70 percent of the vote in 2016 (found in column "clinton_percent")

impeach <-
  filter (impeach, for_impeachment == "YES") %>%
  filter (clinton_percent > "70")

6) Sort the entire dataframe based on the percentage of a district that has a bachelor's degree or higher ("pct_bachelors"), from lowest to highest

impeach <-
  arrange (impeach, pct_bachelors, .by_group = TRUE)

7) Sort the just those who are NO on impeachment based on the percentage of a district that has a bachelor's degree or higher ("pct_bachelors"), from lowest to highest

impeach <-
  arrange (impeach, pct_bachelors, .by_group = TRUE) %>%
  filter (for_impeachment == "NO") 

8) Sort the just those who are NO on impeachment based on the percentage of a district that has a bachelor's degree or higher ("pct_bachelors"), from lowest to highest.Then filter those records by only those whose bachelor's percentage is below the national average (found in the "pct_bachelors_compared_to_national" column).

impeach <-
  arrange (impeach, pct_bachelors, .by_group = TRUE) %>%
  filter (for_impeachment == "NO") %>%
  filter (pct_bachelors_compared_to_national == "BELOW")

9) Filter for only members from New Jersey who are NO on impeachment

impeach <-
  filter (impeach, for_impeachment == "NO") %>%
  filter (state == "NJ")

Answer = Jefferson Van Drew

10) Filter for those who were YES on impeachment, with a declared date prior to 2019. So only those with dates before 2019.  Then sort those so that the highest Clinton vote percentages are
at the top.   

impeach <-
  arrange (impeach, pct_bachelors, .by_group = TRUE) %>%
  filter (for_impeachment == "YES") %>%
  filter (date_year %in% c("2017", "2018"))

11) Answer this question with a single numeric answer, and show the R code you used to reach that answer: How many members in the dataset who are holdouts on impeachment comes from districts with a GDP below the national figure?

impeach <-
  filter (impeach, for_impeachment == "NO") %>%
  filter (gdp_above_national == "BELOW")

19 members
```

**Biden Transition Tracking**

This project scraped the Biden Transition site to share information on the status of the transition teams.
 
AGENCY TEAMS

Come up with the necessary R code to return the following for the agency review teams.


```markdown
Below write code to show the new names added to the agency review team lists since the prior data provided.

newnames %>% 
  select(agency, name, most_recent_employment, on_multiple_teams, team_lead) %>% 
  gt() %>%
  tab_header(
    title = "New Names Added to the Senior Staff"
  ) %>%
  tab_options(table.align = "left") %>%
  cols_align(
    align = "center",
    columns = vars(team_lead, on_multiple_teams)
  )
```

```markdown
Add data to show the total number of people appointed to each agency team, along with change since last time reflecting the number of new people added. Omit agencies with no change at all.

agencycount_compare %>%
  filter(change!=0) %>%
  gt() %>%
  tab_options(table.align = "left") %>%
  tab_style(
      style = list(
        cell_text (weight = "bold", 
                   color = "blue")
        ),
      locations = cells_body(
        columns = vars(change)
      )
  )
```

```markdown
Show the top 10 largest agency review teams as of today:

agencycount_compare %>%
  select(agency,current) %>%
  arrange(desc(current)) %>%
  head(10) %>%
  gt() %>%
  tab_options(table.align = "left")
```

```markdown
Show the top smallest agency review teams as of today - which we'll define here as less than five members:

agencycount_compare %>%
  select(agency,current) %>%
  arrange(desc(current)) %>%
  head(5) %>%
  gt() %>%
  tab_options(table.align = "left")
```

WHITE HOUSE SENIOR STAFF

Come up with the necessary R code to return the following for the WH senior staff.

```markdown
Below write code to show the new names added to the senior staff lists since the prior data provided.

newnames_staff %>% 
  slect(name,title) %>%
  gt() %>%
  tab_header(
    title = "New Names Added to the Senior Staff"
  ) %>%
  tab_options(table.align = "left")
```

```markdown
Add code to show the total number of people currently named to the WH senior staff, vs. the previous total number.

#find current number of people
num_staffcurrent <- staff_data_current %>%
  nrow()

#find previous number
num_staffprevious <- staff_data_previous %>%
  nrow()

#find the difference 
df_staff <- data.frame("current_total" = num_staffcurrent,
                       "previous_total" = num_staffprevious, 
                       "difference" = num_staffdiff)

df_staff% %>%
  gt()
```

**Flexdashboard with Biden Transition Data**

See [link](jacquelinewalsh.github.io/Test.html) 
