Jacksonville Wards Analysis
================
Ray Thompson
6/19/2020

Introduction
============

The purpose of this document is to generate voter statistics on the first ward of Jacksonville, North Carolina. The first half covers general demographics of registered voters. Then an analysis of voting history from elections in the last 10 years. Lastly, I display useful subsets for political campaigns. This is still a work in progress.

### Data

The datasets used in this analysis is public information obtained from the North Carolina [State Board Of Elections website](https://dl.ncsbe.gov/). Below is a list of the columns for the voter and voter history data set.

    ## Rows: 123,731
    ## Columns: 49
    ## $ county_id                <int> 67, 67, 67, 67, 67, 67, 67, 67, 67, 67, 67, …
    ## $ county_desc              <fct> ONSLOW, ONSLOW, ONSLOW, ONSLOW, ONSLOW, ONSL…
    ## $ voter_reg_num            <int> 357175, 369735, 445264, 461549, 449559, 4554…
    ## $ status_cd                <fct> A, R, I, A, I, A, I, A, A, A, A, I, A, I, D,…
    ## $ voter_status_desc        <fct> ACTIVE, REMOVED, INACTIVE, ACTIVE, INACTIVE,…
    ## $ reason_cd                <fct> AV, RL, IU, AV, IN, AV, IU, AV, AV, AV, AV, …
    ## $ voter_status_reason_desc <fct> VERIFIED, MOVED FROM COUNTY, CONFIRMATION RE…
    ## $ last_name                <fct> A'BRIAL, AAGAARD, AARON, AARON, AARON, AARON…
    ## $ first_name               <fct> BRUNO, TERESA, CORY, DAKOTA, DONAVON, HAYLEE…
    ## $ middle_name              <fct> NICKLOUS, INGRAM, BRAM, LEE, VINCENT, NICOLE…
    ## $ name_suffix_lbl          <fct> ,  , , , , , , , , , , , , , , , , , , , , ,…
    ## $ res_street_address       <fct> 609  WOLVERINE PL   , REMOVED, 4059  LILJA C…
    ## $ res_city_desc            <fct> JACKSONVILLE, , MIDWAY PARK, JACKSONVILLE, S…
    ## $ state_cd                 <fct> NC, , NC, NC, NC, NC, NC, NC, NC, NC, NC, NC…
    ## $ zip_code                 <int> 28546, NA, 28544, 28546, 28582, 28582, 28582…
    ## $ mail_addr1               <fct> 609 WOLVERINE PL,  , 4059 LILJA CT, 400 PHOE…
    ## $ mail_addr2               <fct> ,  , , , , , , , , , , , , , , , , , 608 IND…
    ## $ mail_city                <fct> JACKSONVILLE,  , MIDWAY PARK, JACKSONVILLE, …
    ## $ mail_state               <fct> NC,  , NC, NC, NC, NC, NC, NC, NC, NC, NC, N…
    ## $ mail_zipcode             <int> 28546, NA, 28544, 28546, 28582, 28582, 28582…
    ## $ full_phone_number        <dbl> 9104557743, NA, 6023010323, 8633267430, 9103…
    ## $ race_code                <fct> W, W, W, W, U, W, W, O, B, W, O, W, A, O, O,…
    ## $ ethnic_code              <fct> NL, NL, NL, NL, UN, NL, NL, HL, UN, UN, UN, …
    ## $ party_cd                 <fct> REP, REP, UNA, UNA, UNA, UNA, UNA, UNA, DEM,…
    ## $ gender_code              <fct> M, F, M, M, U, F, F, F, F, M, F, F, F, M, M,…
    ## $ birth_age                <int> 32, 52, 26, 23, 22, 21, 63, 37, 70, 58, 22, …
    ## $ birth_state              <fct> NC, MD, AZ, MD, , WA, OK, , NC, , SC, OC, VT…
    ## $ drivers_lic              <fct> Y, Y, Y, Y, N, Y, N, Y, Y, Y, Y, N, N, Y, Y,…
    ## $ registr_dt               <fct> 08/03/2005, 10/24/2007, 08/15/2016, 02/05/20…
    ## $ precinct_abbrv           <fct> BM08, , JA01, EN03, MT24, MT24, MT24, SF18, …
    ## $ precinct_desc            <fct> BM08, , JA01, EN03, MT24, MT24, MT24, SF18, …
    ## $ municipality_abbrv       <fct> , , JAX, JAX, , , , , JAX, , , , JAX, JAX, ,…
    ## $ municipality_desc        <fct> , , JACKSONVILLE, JACKSONVILLE, , , , , JACK…
    ## $ ward_abbrv               <fct> , , JW2, JW3, , , , , JW3, , , , JW2, JW3, ,…
    ## $ ward_desc                <fct> , , JW2, JW3, , , , , JW3, , , , JW2, JW3, ,…
    ## $ cong_dist_abbrv          <int> 3, NA, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, N…
    ## $ super_court_abbrv        <int> 4, NA, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, N…
    ## $ judic_dist_abbrv         <int> 4, NA, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, N…
    ## $ nc_senate_abbrv          <int> 6, NA, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, N…
    ## $ nc_house_abbrv           <int> 14, NA, 15, 14, 14, 14, 14, 15, 15, 14, 4, 4…
    ## $ munic_dist_abbrv         <fct> , , JAX, JAX, , , , , JAX, , , , JAX, JAX, ,…
    ## $ munic_dist_desc          <fct> , , JACKSONVILLE, JACKSONVILLE, , , , , JACK…
    ## $ dist_1_abbrv             <int> 5, NA, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, N…
    ## $ dist_1_desc              <fct> 5TH PROSECUTORIAL, , 5TH PROSECUTORIAL, 5TH …
    ## $ confidential_ind         <fct> N, N, N, N, N, N, N, N, N, N, N, N, N, N, N,…
    ## $ birth_year               <int> 1987, 1967, 1993, 1997, 1997, 1999, 1956, 19…
    ## $ ncid                     <fct> DD106914, DD118372, DD182433, DD195035, DD18…
    ## $ vtd_abbrv                <fct> BM08, , JA01, EN03, MT24, MT24, MT24, SF18, …
    ## $ vtd_desc                 <fct> BM08, , JA01, EN03, MT24, MT24, MT24, SF18, …

    ## Rows: 364,964
    ## Columns: 15
    ## $ county_id         <int> 67, 67, 67, 67, 67, 67, 67, 67, 67, 67, 67, 67, 67,…
    ## $ county_desc       <fct> ONSLOW, ONSLOW, ONSLOW, ONSLOW, ONSLOW, ONSLOW, ONS…
    ## $ voter_reg_num     <int> 480992, 480992, 480992, 480992, 480992, 480992, 478…
    ## $ election_lbl      <fct> 11/02/2010, 11/08/2016, 11/06/2018, 11/04/2014, 11/…
    ## $ election_desc     <fct> 11/02/2010 GENERAL, 11/08/2016 GENERAL, 11/06/2018 …
    ## $ voting_method     <fct> IN-PERSON, ABSENTEE ONESTOP, PROVISIONAL, IN-PERSON…
    ## $ voted_party_cd    <fct> UNA, UNA, REP, UNA, UNA, REP, DEM, DEM, DEM, DEM, D…
    ## $ voted_party_desc  <fct> UNAFFILIATED, UNAFFILIATED, REPUBLICAN, UNAFFILIATE…
    ## $ pct_label         <fct> 08S, 10N, 10N, 08S, 08S, EN03, 13, 13, 13, 13, 13, …
    ## $ pct_description   <fct> SOUTH NEWLIN, NORTH MELVILLE, NORTH MELVILLE, SOUTH…
    ## $ ncid              <fct> AA100682, AA100682, AA100682, AA100682, AA100682, A…
    ## $ voted_county_id   <int> 1, 1, 1, 1, 1, 67, 1, 1, 1, 1, 1, 1, 67, 67, 67, 67…
    ## $ voted_county_desc <fct> ALAMANCE, ALAMANCE, ALAMANCE, ALAMANCE, ALAMANCE, O…
    ## $ vtd_label         <fct> 08S, 10N, 10N, 08S, 08S, EN03, 13, 13, 13, 13, 13, …
    ## $ vtd_description   <fct> 08S, 10N, 10N, 08S, 08S, EN03, 13, 13, 13, 13, 13, …

The voter file provided by the NCSBE contains 123731 records of past and present voters. There is an average of 7778 records for each Ward. Ward 1 contains 3446 records.

Ward Demographics
=================

Party
-----

### Average age by party

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 6 x 2
    ##   party_cd Average.Age
    ##   <fct>          <dbl>
    ## 1 CST             29.8
    ## 2 DEM             47.2
    ## 3 GRE             43  
    ## 4 LIB             31.7
    ## 5 REP             35.5
    ## 6 UNA             34.0

<img src="Wards_files/figure-markdown_github/age-1.png" style="display: block; margin: auto;" />

Unaffiliated voters comprise the largest chunk of registered voters and also have a lower mean age than Democrats and Republicans. Democrats are the second largest chunk with the highest mean age among all parties. Republicans are on average 12 years younger than democrats and 1.5 years older than unaffiliated voters.

### No. of voters by party

    ##  CST  DEM  GRE  LIB  REP  UNA 
    ##    5 1211    1   40  862 1327

### No. of voters per age group

    ## 18-34 35-49 50-64   65+  NA's 
    ##  1811   753   509   355    18

<img src="Wards_files/figure-markdown_github/unnamed-chunk-2-1.png" width="50%" /><img src="Wards_files/figure-markdown_github/unnamed-chunk-2-2.png" width="50%" /><img src="Wards_files/figure-markdown_github/unnamed-chunk-2-3.png" width="50%" /><img src="Wards_files/figure-markdown_github/unnamed-chunk-2-4.png" width="50%" />

There are around 1700 more registered voters in the 18-49 demographic than people 50+. This is interesting because as you'll see in the "Voter History" section of this document, the 50+ demographic takes up a much larger share of the votes cast from 2010-2020.

### Distribution on Map

![](Rplot01.png)

It appears that the first ward is comprised of 5-6 neighborhood with one being inside Camp Lejeune. The age group of 18-34 appears to be the most diverse in terms of party affiliation. There seems to be a trend of democrat affiliation the older an age group is. That does not seem to apply to the neighborhood in Camp Lejeune as the marines there are usually republican or unaffiliated.

### Party by Race

![](Wards_files/figure-markdown_github/unnamed-chunk-3-1.png)

It's obvious that a majority of black people are either in the democratic party or are unaffiliated. There are over 1000 white republican and unaffiliated voters and under 250 white Democratic voters.

### Party by Sex

![](Wards_files/figure-markdown_github/unnamed-chunk-4-1.png)

Overall, there are more female registered voters than males. There are much more black women democrats than black male democrats. There are slightly less white male democrats than white female democrats.

### No. of voters by gender

    ##    F    M    U 
    ## 1917 1325  204

Age
---

### Average Age by Race

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 7 x 2
    ##   race_code Average.Age
    ##   <fct>           <dbl>
    ## 1 A                37.2
    ## 2 B                46.2
    ## 3 I                36.4
    ## 4 M                32.4
    ## 5 O                34.4
    ## 6 U                35.6
    ## 7 W                34.9

![](Wards_files/figure-markdown_github/unnamed-chunk-7-1.png)

### No. of voters by Race

    ##    A    B    I    M    O    U    W 
    ##   38 1222   11   44  187  343 1601

### Distribution on Map

![](Raceplot02.png)

There are two special minority-majority wards in Jacksonville. This district has a slight white majority, but I wouldn't be surprised if this is one of the special wards created ten years ago. The 18-34 demographic is mostly white, but as the sample grows towards 50 years old, two neighborhoods in town become mostly black. The third has so few older members that I believe it may be housing for marines. There are more elderly black registered voters than elderly white voters. There are also more young white registered voters than young black voters.

### Race and Sex

![](Wards_files/figure-markdown_github/unnamed-chunk-9-1.png)

### Average Age by Sex

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 3 x 2
    ##   gender_code Average.age
    ##   <fct>             <dbl>
    ## 1 F                  39.3
    ## 2 M                  38.9
    ## 3 U                  36.4

![](Wards_files/figure-markdown_github/unnamed-chunk-10-1.png)

    ##    F    M    U 
    ## 1917 1325  204

### General Age Summary

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   17.00   25.00   33.00   38.98   50.00  120.00

There are multiple 17 year old voters registered in preparation for the 2020 elections. The oldest person on the roll is 120 and he is listed as voting in 2016 in person. He is the only person on the roll above 100 and I'm not sure if it is an error.

Voter History
=============

Registration
------------

### Registrations by year

    ##         Min.      1st Qu.       Median         Mean      3rd Qu.         Max. 
    ## "1966-10-08" "1984-01-28" "2003-09-24" "1998-02-27" "2012-05-26" "2020-03-06"

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Wards_files/figure-markdown_github/unnamed-chunk-12-1.png) I believe the largest registration spikes are for the 2008, 2012, and 2016 elections. There are noticeably smaller spikes for the 2018 midterms and 2020 election.

Elections
---------

### votes cast by age group

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Wards_files/figure-markdown_github/unnamed-chunk-13-1.png)

    ## 18-34 35-49 50-64   65+  NA's 
    ##  1811   753   509   355    18

The 50+ age group consistently votes more than ages 18-49 although the 2016 saw a roughly equal amount of both. The 2020 primary had a very low number of young voters even though they outnumber elderly voters and had multiple progressive candidates on the ballot.

SubSets
=======

Hypothesis test
===============

Permutation Tests
-----------------

### Difference between generations

![](Wards_files/figure-markdown_github/unnamed-chunk-14-1.png)![](Wards_files/figure-markdown_github/unnamed-chunk-14-2.png)

#### Sample summary

``` r
summary(young$n)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1.00    1.00    2.00    3.13    4.00   15.00

``` r
summary(old$n)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1.00    4.00    7.00    7.61   11.00   18.00

``` r
observed.diff <- mean(old$n) - mean(young$n)
observed.diff
```

    ## [1] 4.48

#### Plotting results

``` r
num_iter <- 10000
n <- 100
result <- numeric(num_iter) #setup a vector to store the permutation test results
sample <- rbind(young,old)
for(i in 1:num_iter)
{
  index <- sample(length(sample$n), size = n, replace = FALSE)  # choose a sample of numbers from the data to represent the votes at random
  result[i] <- mean(sample$n[index]) - mean(sample$n[-index]) 
}
ggplot() + geom_histogram(aes(result)) + geom_vline(xintercept=observed.diff, colour = "red")
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Wards_files/figure-markdown_github/unnamed-chunk-16-1.png)

``` r
pval1 <- (sum(result >= observed.diff) + 1)/(num_iter+1)  # an approximate p-value
pval2 <- (sum(result <= observed.diff) + 1)/(num_iter+1)
pval <- 2*min(pval1,pval2)
pval
```

    ## [1] 0.00019998

### Difference between parties

![](Wards_files/figure-markdown_github/unnamed-chunk-17-1.png)![](Wards_files/figure-markdown_github/unnamed-chunk-17-2.png)![](Wards_files/figure-markdown_github/unnamed-chunk-17-3.png)

#### Sample summary

``` r
summary(dem$n)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##       1       2       5       6       9      18

``` r
summary(rep$n)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1.00    1.75    3.50    5.17    7.00   18.00

``` r
summary(una$n)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1.00    1.00    3.00    4.21    5.00   16.00

``` r
observed.diff <- mean(dem$n) - mean(rep$n)
observed.diff
```

    ## [1] 0.83

#### Plotting results

``` r
num_iter <- 10000
n <- 100

result <- numeric(num_iter)
sample <- rbind(dem,rep)

for(i in 1:num_iter)
{
  index <- sample(length(sample$n), size = n, replace = FALSE)  
  rep_index <- sample(length(sample$n), size = n, replace = FALSE)
  result[i] <- mean(sample$n[index]) - mean(sample$n[-index]) 
}
ggplot() + geom_histogram(aes(result)) + geom_vline(xintercept=observed.diff, colour = "red")
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Wards_files/figure-markdown_github/unnamed-chunk-19-1.png)

``` r
pval1 <- (sum(result >= observed.diff) + 1)/(num_iter+1) 
pval2 <- (sum(result <= observed.diff) + 1)/(num_iter+1)
pval <- 2*min(pval1,pval2)
pval
```

    ## [1] 0.2051795
