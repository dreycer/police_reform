
# Clustering US Counties to Provide Data for Improvement in Police Scorecard 

### Danielle Reycer
---

## Table of Contents
1. [Background](#Background)
2. [Problem Statement](#Problem-Statement)
3. [My Notebooks](#My-Notebooks)
4. [Conclusions](#Conclusions)
5. [Next Steps](#Next-Steps)
6. [Data](#Data)
7. [References](#References)

---
---

## Background
In May 2020, for 9 minutes and 29 seconds, a police officer pressed his knee into the neck of George Floyd, an unarmed Black man. This deadly use of force by the now-former Minneapolis police officer (recently convincted of the murder of George Floyd), reinvigorated a very public debate about police brutality and racism.

As protests have spread around the globe, the pressure is on police departments and politicians, particularly in the United States, to do something — from reforming law-enforcement tactics to defunding or even abolishing police departments. 

And although researchers are encouraged by the momentum for change, some are also concerned that, without ample evidence to support new policies, leaders might miss the mark. Many have been arguing for years about the need for better data on the use of force by the police in the United States, and for rigorous studies that test interventions such as training on how to de-escalate tense interactions or mandating the use of body-worn cameras by officers. Those data and studies have begun to materialize, spurred by protests in 2014 after the deadly shooting of Michael Brown in Ferguson, Missouri, and the death by chokehold of Eric Garner in New York City.

Government officials, academic researchers and media outlets launched data-collection projects around that time to better understand the frequency of police violence and the risk factors that contribute to it. From these growing data sets come some disturbing findings. About 1,000 civilians are killed each year by law-enforcement officers in the United States. By one estimate, Black men are 2.5 times more likely than white men to be killed by police during their lifetime. And in another study, Black people who were fatally shot by police seemed to be twice as likely as white people to be unarmed.

Sources:
* https://en.wikipedia.org/wiki/Derek_Chauvin 
* https://www.nature.com/articles/d41586-020-01846-z 


---
## Problem Statement

Much of the police reform being demanded by protestors will have to come from local or state-level politicians and policies. Often, local policy-makers rely on changes that have worked in counties or cities that are most like their own. By giving local and county politicians this information, I am providing them with a starting point for what to research in order to improve their own policing. Instead of choosing policies 'in the dark,' this work provides a solid starting place for reform.

I aim to produce a function that, when given a county and its associated state, returns the current county average police scorecard overall score (if there is one) as well as returning the top three scoring counties that are most similar in regards to separate data based on these factors: 
* Quality of Life
* Health Behaviors
* Access & Quality of Clinical Care
* Education
* Family & Social Support
* Community Safety
* Physical Environment


---

## My Notebooks

* `demographics_cleaning_1.ipynb`: First round of cleaning on the demographics data
* `demographics_cleaning_2.ipynb`: Second round of cleaning on the demographics data
* `police_scorecard_cleaning.ipynb`: Cleaning and paring down the Police Scorecard Data
* `police_corr_with_demographics.ipynb`: Studying correlation between demographics and the Police Scorecard Values
* `model_and_function.ipynb`: Performing PCA, creating a running a clustering model (KMeans), visualizing the clusters, and creating my final function - providing the top counties scorecard in the same cluster.
* Note there is also a `code_for_future_work` folder with a few notebooks. Since I hope to revisit this work, I wanted to keep all my notebooks in a single repository.

---

## Conclusions


Through PCA, I was able to improve my model significantly. I analyzed the weights of each feature to pull out themes from each principal component. I found that the first component weighed heavily on the overall occurrences of different categories. There were no features that represented percentages of the county population. The top weighted features were population, education, and family-related. In comparison, the top weighted features from the second principal component contained only percentage values from the populations. The focus appeared to rely on education and healthcare/healthcare access with a slight emphasis on family demographics. 

The work I have done provides a starting place for local governments and politicians to get a list of counties that are most like their own that have the highest average police scorecard value. This information can be used to begin a larger research project into policies that have been enacted in those counties. If lawmakers want to get more granular, they can also research the individual precincts within the top counties. As of now that would have to be done manually through the police scorecard website. 

---

## Next Steps

As part of my efforts to increase my silhouette score, I tried including voting data (% of voters in each county who voted republican, democrat, or 'other'), but it lowered my score. I do think that with more data, it could be possible to get more clear separation of clusters. There is more data available from the County Health Rankings that could be imported, explored, and cleaned. I could also look for other sources of data to merge, such as data from the US Census. I am also interested in getting more granular with the data, since Police Scorecard has scored over 16,000 municipalities/precincts. It's possible that we could get city/town specific demographic data, but this work recognized the limitations of finding such data at such a small level. To illustrate the complicated nature of this level of granularity, as of 2018, there were 19,495 incorporated cities, towns and villages in the United States. 14,768 of these have populations below 5,000. [Source](https://worldpopulationreview.com/us-city-rankings/how-many-cities-are-in-the-us). 

It is also possible that local politicians looking to improve their police scorecard may want to see more granular data than the function currently offers. A future feature would be to drill down into the precincts that have been scored within each top scoring county in each of the clusters. I could work to extract that information based on the FIPS codes from the original Police Scorecard data.

My current function lives inside a Jupyter Notebook, but I have also created a sample phone app Wireframe as a starting idea of what an easy to use application could look like. 

---

## Data 

### Data Information

### Police Scorecard

The Police Scorecard is the first nationwide public evaluation of policing in the United States. The Scorecard calculates levels of police violence, accountability, racial bias and other policing outcomes for over 16,000 municipal and county law enforcement agencies, covering nearly 100% of the US population. The indicators included in this scorecard were selected based on a review of the research literature, input from activists and experts in the field, and a review of publicly available datasets on policing from federal, state, and local agencies. This project is designed to help communities, researchers, police leaders and policy-makers take data-informed action to reduce police use of force, increase accountability and reimagine public safety in their jurisdictions.

---

### County Health Rankings

The CHR&R program provides data, evidence, guidance, and examples to build awareness of the multiple factors that influence health and support community leaders working to improve health and increase health equity. The Rankings are unique in their ability to measure the health of nearly every county in all 50 states, and are complemented by guidance, tools, and resources designed to accelerate community learning and action.


### Data Dictionary

---

|Feature |Type |Dataset |Description |
|--- |--- |--- |--- |
|**agency_name** |object |Police Scorecard |Name of Police Agency |
|**location_name** |object |Police Scorecard |City |
|**calc_overall_score** |int64 |Police Scorecard |Overall Policing Score |
|**FIPS** |object |demographics |County Identifer/mapper |
|**State** |object |demographics |State that the county is in|
|**County** |object |demographics |Individual division of a state |
|**% Fair or poor health** |float |demographics |Percentage of adults reporting fair or poor health |
|**Average number of physically unhealthy days** |float |demographics |Average number of physically unhealthy days reported in past 30 days |
|**Average number of physically unhealthy days** |float |demographics |Average number of mentally unhealthy days reported in past 30 days |
|**% Low birthweight** |float |demographics |Percentage of live births with low birthweight (< 2,500 grams) |
|**% Smokers** |float |demographics |Percentage of adults who are current smokers |
|**% Adults with Obesity** |float |demographics |Percentage of the adult population (age 20 and older) that reports a body mass index (BMI) greater than or equal to 30 kg/m2 |
|**% Physically Inactive** |float |demographics |Percentage of adults age 20 and over reporting no leisure-time physical activity |
|**% With Access to Exercise Opportunities** |float |demographics |Percentage of population with adequate access to locations for physical activity |
|**% Excessive Drinking** |float |demographics |Percentage of adults reporting binge or heavy drinking |
|**# Alcohol-Impaired Driving Deaths** |float |demographics |driving deaths with alcohol involvement |
|**# Driving Deaths** |float |demographics |overall driving deaths |
|**% Driving Deaths with Alcohol Involvement** |float |demographics |% of driving deaths with alcohol involvement |
|**# Uninsured** |float |demographics |Number of people without insurance |
|**% Uninsured** |float |demographics |Percentage of people without insurance |
|**Preventable Hospitalization Rate** |float |demographics |Rate of hospital stays for ambulatory-care sensitive conditions per 100,000 Medicare enrollees |
|**% With Annual Mammogram** |float |demographics |Percentage of people needing one who received an annual mammogram |
|**% Vaccinated** |float |demographics |Percent of people who received normal vaccinations, not including COVID |
|**# Completed High School** |integer |demographics |Number of people in the county who completed high school |
|**Population** |float |demographics |Adults age 25 and older |
|**% Completed High School** |float |demographics |Percentage of people aged 25 and older who completed high school |
|**# Some College** |integer |demographics |Number of people who completed some college |
|**Population.1** |float |demographics |Adults age 25-44 |
|**% Some College** |float |demographics |Percentage of people aged 25-44 who have completed some college |
|**# Unemployed** |integer |demographics |Number of people age 16+ unemployed and looking for work |
|**Labor Force** |float |demographics |Size of the labor force |
|**% Unemployed** |float |demographics |Percentage of population ages 16+ unemployed and looking for work |
|**% Children in Poverty** |float |demographics |Percentage of children (under age 18) living in poverty |
|**Income Ratio** |float |demographics |Ratio of household income at the 80th percentile to income at the 20th percentile |
|**# Children in Single-Parent Households** |integer |demographics |Number of children that live in single-parent households |
|**# Children in Households** |integer |demographics |Number of children in households |
|**% Children in Single-Parent Households** |float |demographics |Percentage of children that live in single-parent households |
|**# Associations** |integer |demographics |Number of social associations |
|**Social Association Rate** |float |demographics |Associations per 10,000 population |
|**Violent Crime Rate** |float |demographics |Violent crimes per 100,000 population |
|**# Injury Deaths** |integer |demographics |Number of injury deaths |
|**Injury Death Rate** |float |demographics |Injury mortality rate per 100,000 |
|**Average Daily PM2.5** |float |demographics |Average daily amount of fine particulate matter in micrograms per cubic meter |
|**% Severe Housing Problems** |float |demographics |Percentage of households with at least 1 of 4 housing problems: overcrowding, high housing costs, or lack of kitchen or plumbing facilities |
|**Severe Housing Cost Burden** |float |demographics |Percentage of households with high housing costs |
|**Overcrowding** |float |demographics |Percentage of households with overcrowding |
|**Inadequate Facilities** |float |demographics |Percentage of households with lack of kitchen or plumbing facilities |
|**% Drive Alone to Work** |float |demographics |Percentage of workers who drive alone to work |
|**# Workers who Drive Alone** |integer |demographics |Number of workers who commute in their car, truck or van alone |
|**% Long Commute - Drives Alone** |float |demographics |Among workers who commute in their car alone, the percentage that commute more than 30 minutes |
|**Water_Violation** |float |demographics |Whether or not the county had a water violation |



---

## Additional References

* https://www.census.gov/data/datasets/time-series/demo/popest/2010s-counties-total.html#par_textimage_70769902
* https://www.weather.gov/gis/Counties
* https://electionlab.mit.edu/data


---

