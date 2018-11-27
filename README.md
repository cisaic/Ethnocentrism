# Ethnocentrism assignment

This repo holds the analysis files for the PSYC 315 Ethnocentrism assignment

For this assignment, 3 simulations (run, run-all-strategies, run1plots) were run for 2 x 5 parameters 
Two different population sizes were simulated: 10x10 and 50x50
For each population size, 5 different 'tags' or 'countries' were simulated: 1, 2, 4, 8, 1,000 or 10,000

1,000 tags were simulated for the n=100 population world to simulate an 'every man for himself environment'. 10,000 tags were used in the n=2500 population world. For the first example, as there are only 100 possible agents, but 1000 possible tags, it is likely that there will be many unique tags, approximating a scenario in which there are many out-groups and no/very vew in-groups. 
It is clear to the author that this does not create a world in which every tag is 100% unique as agent offspring will resemble their parents.
Ideally (given some time to re-run the simulations), without restructuring the code very much, the 'uniqueness' of each agent would be ensured by modifying the tag mutation probability of offspring from 0.005 to 1, so there is a 100% chance the offspring has a different tag than its parent. 
Despite this, the author found the results to be sufficient for the purpose of the analysis

# Description of the python files in this repo:

### 10x10behaviour-proportions
- analysis of ethnocentrism code generated from function RUN
- box plot comparing proportions of behaviours (cooperate/defect) by number of tags for the population of size 10x10 

### 50x50behaviour-proportions
- analysis of ethnocentrism code generated from function RUN
- box plot comparing proportions of behaviours (cooperate/defect) by number of tags for the population of size 50x50 

### 10x10strategy-freq
- analysis of ethnocentrism code generated from function RUN-ALL-STRATEGIES
- for 10x10 world:
	- graph of mean strategy frequency (selfish, traitor, ethnocentric, humanitarian) for each tag (1, 2, 4, 8, 1000)
	- graph of strategy frequency for each of the 10 WORLDS generated per tag 

### 50x50strategy-freq
- same as above but for 50x50 population size

#### population-strategy-proportions
- analysis of ethnocentrism code generated from function RUN
- box plots comparing strategy proportion in the 10x10 and 50x50 simulation for each tag 
- why box plot? only 10 data points per plot point, not sufficient data to show just mean. wanted to display distribution of the data

- 10x10strategy-proportions
- 10x10 box plot comparing strategy proportions per tag for last 100 cycles out of 1000 total cycles over 10 worlds 

50x50strategy-proportions
- analysis of ethnocentrism code generated from function RUN
- 10x10 box plot comparing strategy proportions per tag for last 100 cycles out of 1000 total cycles over 10 worlds 


**Quick note:**
I realize there's a lot of unecessary repetiton in this code that could easily have been avoided by creating a list of dataframe variable names and generating the different dataframes in a for loop then saving the data to a csv for subsequent programs to access... unfortunately I lacked the foresight to prevent this from happening and the time to refactor the code. Please enjoy the pain
