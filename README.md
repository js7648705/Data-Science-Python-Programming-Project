# Data-Science-Python-Programming-Project
## Introduction
The data for this assignment come from the Hospital Compare web site (http://hospitalcompare.hhs.gov) run by the U.S. Department of Health and Human Services. The purpose of the web site is to provide data and information about the quality of care at over 4,000 Medicare-certified hospitals in the U.S. This dataset es-sentially covers all major U.S. hospitals. This dataset is used for a variety of purposes, including determining whether hospitals should be fined for not providing high quality care to patients (see http://goo.gl/jAXFX for some background on this particular topic).

The Hospital Compare web site contains a lot of data and we will only look at a small subset for this assignment. The zip file for this assignment contains three files.

* outcome-of-care-measures.csv: Contains information about 30-day mortality and readmission rates for heart attacks, heart failure, and pneumonia for over 4,000 hospitals.
* hospital-data.csv: Contains information about each hospital.
* Hospital_Revised_Flatfiles.pdf: Descriptions of the variables in each file (i.e the code book).

A description of the variables in each of the files is in the included PDF file named Hospital_Revised_Flatfiles.pdf. This document contains information about many other files that are not included with this programming assignment. We will want to focus on the variables for Number 19 (Outcome of Care Measures.csv") and Number 11 ("Hospital_Data.csv"). It useful to print out this document (at least the pages for Tables 19 and 11) to have next to you while you work on this assignment. In particular, the numbers of the variables for each table indicate column indices in each table (i.e. "Hospital Name" is column 2 in the outcome-of-care-measures.csv file).
### 1. Plotting the 30-day mortality rates for heart attack, heart failure and pneumonia
The data orginally is read in as characters, so first, we have converted it in to numeric and coerced the errors, and then plotted the histogram for      each column (`heart attack, heart failure and pneumonia`)
### 2. Finding the best hospital in a state
Created a function called `best` that take two arguments: the 2-character abbreviated name of a `state and outcome`. The function reads the outcome-of-care-measures.csv file and returns a character vector with the name of the hospital that has the best (i.e. lowest) 30-day mortality for the specified outcome
in that state. The hospital name is the name provided in the Hospital.Name variable. The outcomes can be one of (`heart attack, heart failure, or pneumonia`). Hospitals that do not have data on a particular outcome have been excluded from the set of hospitals when deciding the rankings.
#### a. Handling ties 
If there is a tie for the best hospital for a given outcome, then the hospital names are sorted in alphabetical order and the first hospital in that set is chosen (i.e. if hospitals "b", "c", and "f" are tied for best, then hospital "b" is returned.
#### b. Checking the validity of its arguments
The function checks the validity of its arguments. If an invalid state value is passed to best, the function throw an error with the exact message "invalid state". If an invalid outcome value is passed to best, the function should throw an error with the exact message "invalid outcome".
### 3. Ranking hospitals by outcome in a state
Wrote a function called `rankhospital` that takes three arguments: the 2-character abbreviated name of a `state (state), an outcome (outcome), and the ranking of a hospital in that state for that outcome (num)` . The function reads the outcome-of-care-measures.csv file and returns a character vector with the name of the hospital that has the ranking specified by the num argument. For example, the call rankhospital(`"MD", "heart failure", 5` ) would return a character vector containing the name of the hospital with the 5th lowest 30-day death rate for heart failure. The num argument can take values `"best", "worst", or an integer`  indicating the ranking (smaller numbers are better). If the number given by num is larger than the number of hospitals in that state, then the function return NA. Hospitals that do not have data on a particular outcome are excluded from the set of hospitals when deciding the rankings.
#### a. Handling ties. 
It may occur that multiple hospitals have the same 30-day mortality rate for a given cause of death. In those cases ties are broken by using the hospital name. For example, in Texas ("TX"),the hospitals with lowest 30-day mortality rate for heart failure are shown here.

##### head(texas)
Hospital.Name  Rate  Rank\
3935 FORT DUNCAN MEDICAL CENTER  8.1  1\
4085 TOMBALL REGIONAL MEDICAL CENTER  8.5  2\
4103 CYPRESS FAIRBANKS MEDICAL CENTER  8.7  3\
3954 DETAR HOSPITAL NAVARRO  8.7  4\
4010 METHODIST HOSPITAL,THE  8.8  5\
3962 MISSION REGIONAL MEDICAL CENTER  8.8  6

Note that Cypress Fairbanks Medical Center and Detar Hospital Navarro both have the same 30-day rate (8.7). However, because Cypress comes before Detar alphabetically, Cypress is ranked number 3 in this scheme and Detar is ranked number 4. The "sort_values function" was being used to sort multiple vectors in this manner (i.e. where one vector is used to break ties in another vector).

#### b. Checking the validity of its arguments
The function checks the validity of its arguments. If an invalid state value is passed to best, the function throw an error with the exact message "invalid state". If an invalid outcome value is passed to best, the function should throw an error with the exact message "invalid outcome".

### 4. Ranking hospitals in all states
Developed a function called `rankall` that takes two arguments:`an outcome name (outcome) and a hospital rank-ing (num)`. The function reads the outcome-of-care-measures.csv file and returns a 2-column data frame containing the hospital in each state  that has the ranking specified in num. For example the function call rankall("heart attack", "best") returns a data frame containing the names of the hospitals that are the best in their respective states for 30-day heart attack death rates. The function returns a value for every state (some may be NA). The first column in the data frame is named hospital, which contains the hospital name, and the second column is named state, which contains the 2-character abbreviation for the state name. Hospitals that do not have data on a particular outcome are excluded from the set of hospitals when deciding the rankings.

#### a. Handling ties. 
The rankall function handles ties in the 30-day mortality rates in the same way that the rankhospital function handles ties.
The function should use the following template.\
rankall <- function(outcome, num = "best") {\
Read outcome data\
Check that state and outcome are valid\
For each state, find the hospital of the given rank\
Return a data frame with the hospital names and the\
(abbreviated) state name\
}

#### b. Checking the validity of its arguments
The function checks the validity of its arguments. If an invalid outcome value is passed to rankall, the function should throw an error with the exact message "invalid outcome". The num variable can take values "best", "worst", or an integer indicating the ranking (smaller numbers are better). If the number given by num is larger than the number of hospitals in that state, then the function returns NA.
