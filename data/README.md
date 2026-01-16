## `ambiguity.csv`

- `name` : candidate name
- `distID` : unique identification number for Congressional dirict
- `ideology` : candidate left-right orientation
- `democrat` : 1 if Democrat, 0 if Republican
- `mismatch` : disagreement between candidate ideology and dirict voter ideology
- `incumbent` : 1 if incumbent, 0 if not
- `demHeterogeneity` : how much voters in a district differ acrding to race, education, occupation, etc.
- `attHeterogeneity` : how much voters in a district differ acrding to political ideology
- `distLean` : overall ideological lean in a district
- `totalIssuePages` : number of issues candidates commented on (response)

## `birdkeeping.csv`

- `female` = sex (1 = Female, 0 = Male)
- `age` = age, in years
- `highstatus` = socioeconomic status (1 = High, 0 = Low), dermined by the occupation of the household’s primary wage earner
- `yrsmoke` = years of smoking prior to diagnosis or exination
- `cigsday` = average rate of smoking, in cigarettes per day
- `bird` = indicator of birdkeeping (1 = Yes, 0 = No), determined by whether or not there were caged birds in the home for more than 6 consecutive months from 5 to 14 years before diagnosis (cases) or examination (controls)
- `cancer` = indicator of lung cancer diagnosis (1 = Cancer, 0 = No Cancer)
    
    
**R code from BMLR that can be used to create new variables.**

```{r, eval = FALSE}
birds <- read_csv("data/birdkeeping.csv") %>%
  mutate(sex = ifelse(female == 1, "Female", "Male"),
         socioecon_status = ifelse(highstatus == 1, 
                                   "High", "Low"),
         keep_bird = ifelse(bird == 1, "Keep Bird", "No Bird"),
         lung_cancer = ifelse(cancer == 1, "Cancer", 
                              "No Cancer")) %>%
  mutate(years_factor = cut(yrsmoke, 
                            breaks = c(-Inf, 0, 25, Inf),
            labels = c("No smoking", "1-25 years", 
                       "Over 25 years")))
```