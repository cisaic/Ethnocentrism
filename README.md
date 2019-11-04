# Ethnocentrism assignment

This repo holds the analysis files for the PSYC 315 Ethnocentrism assignment

For this assignment, 3 simulations (run, run-all-strategies, run1plots) were run for 2 x 5 parameters 
Two different population sizes were simulated: 10x10 and 50x50
For each population size, 5 different 'tags' or 'countries' were simulated: 1, 2, 4, 8, 1,000 or 10,000

10,000 tags were simulated for the n=100 population world to simulate an 'every man for himself environment'. 100,000 tags were used in the n=2500 population world. For the first example, as there are only 100 possible agents, but 10,000 possible tags, it is likely that there will be many unique tags, approximating a scenario in which there are many out-groups and no/very vew in-groups. 
It is clear to the author that this does not create a world in which every tag is 100% unique as agent offspring will resemble their parents.
To ensure the 'uniqueness' of each agent, the tag mutation probability of offspring is adjusted from 0.005 to 1, so there is a 100% chance the offspring has a different tag than its parent. In-group/out-group strategy mutation remains the same.

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

### population-strategy-proportions
- analysis of ethnocentrism code generated from function RUN
- box plots comparing strategy proportion in the 10x10 and 50x50 simulation for each tag 
- why box plot? only 10 data points per plot point, not sufficient data to show just mean. wanted to display distribution of the data

### strategy-proportions
- analysis of ethnocentrism code generated from function RUN
- 10x10 box plot comparing strategy proportions per tag for last 100 cycles out of 1000 total cycles over 10 worlds 
- 50x50 box plot comparing strategy proportions per tag for last 100 cycles out of 1000 total cycles over 10 worlds 


**Quick note:**
I realize there's a lot of unecessary repetiton in this code that could easily have been avoided by creating a list of dataframe variable names and generating the different dataframes in a for loop then saving the data to a csv for subsequent programs to access... unfortunately I lacked the foresight to prevent this from happening and the time to refactor the code. Please enjoy the pain

# Graphing data/code

# Code modifications
**Made very few modifications and it's hard to search through whole code**
**So I extracted the modified functions to this file to explain what I did**

## 10000-tag-code:

**Modification made to the MUTATE function ensure tag automatically mutates in a clone**

```
(defun mutate (trait current)
  "(trait current)
Mutate trait from current value if random probability < *mutation-rate*.
If trait is tag, automatically mutate"
  (if (eq trait 'tag)
    (random-mutation current (values-of-trait trait))
    (if (< (random 1.0) *mutation-rate*)
        (random-mutation current (values-of-trait trait))
      current)))
```

## 1-tag-code

**Modification made to the CLONE function to ensure tag does not mutate**
**Commented out function that does that**
**Since there's only 1 tag, offspring tag must be same kind**

```
(defun clone (r c)
  "(r c)
Clone agent at r, c to an empty neighboring location, if any, after possible mutations."
  (let* ((agent (aref *torus* r c))
         (tag (agent-tag agent))
         (igs (agent-igs agent))
         (ogs (agent-ogs agent))
         (possible-locations (empty-neighbors r c))
         (clone-location (if possible-locations
                             (nth 
                              (random (length possible-locations)) 
                              possible-locations)
                           nil))
         ;(tag (mutate 'tag tag))
         (igs (mutate 'igs igs))
         (ogs (mutate 'ogs ogs)))
    (if clone-location
        (setf 
         (aref *torus* (first clone-location) (second clone-location))
         (make-agent :tag tag
                     :igs igs
                     :ogs ogs
                     :ptr *base-ptr*)))))

**Modification of IMMIGRANT function**
**set tag = 1 instead of (random *ntags*)**

(defun immigrant ()
  "()
Make 1 immigrant with random characteristics."
  (let* ((tag 1)
         (igs (random 2))
         (ogs (random 2))
         (location (empty-location))
         (row (first location))
         (column (second location)))
    (setf (aref*torus*row column) 
      (make-agent :tag tag
                  :igs igs
                  :ogs ogs
                  :ptr *base-ptr*))))
```
