# Football stadium

## Description
* Simulation of waiting queues in front of a football stadium.
* Play around with different scenarios
* Is it true that staying in one lane is faster than switching lane?
* What happenes if a big group of Ultras shows up all at once?


## Parameters
* number of visitors: **6000**
* first visitors arrival: **2h** before
* check-in time:
  * standard visitor: **6 $\pm$ 3s**
  * season ticket holders: **3 $\pm$ 1s**
* share of season ticket holders: **40%**
* entry gates: _n_
* arrival rate of visitors: _r_
* pedestrian speed:
  * initial: **[0.3, 0.7]**
  * comfortable: **[0.5, 1.0]**

## Tools
* AnyLogic with Pedestrian library


## Modeling paradigm
* agent-based


## Tasks
### Task 1
* determine number of gates _n_, so that **99%** of fans are inside the stadium at kickoff
* set reasonable arrival rate _r_ of visitor
* keep _n_ for following tasks

->
* $n = 7$
* $r = poisson(\frac{total\ arrival\ time\ in\ seconds}{expected\ visitors}) = poisson(\frac{7200}{expected\ visitors})$ per second

### Task 2
* **1h** before kickoff **500** Ultras (standard visitors)
* can the queue be processed until kickoff?

->
* 

### Task 3
* determine number of minutes the last fan will miss the kickoff, if total number of visitors exceeds **8000**

->
* 

### Task 4
* effects of prioritizing season ticket holders:
  * average queuing times
  * number of fans entering after kickoff
* experiment with season ticket holders taking advantage of priority and arriving later than normal

->
* compare 
  * (a) no priority (task1)
  * (b) with priority for season ticket holders
  * (c) with priority and arriving earliest 1.5h before
  * (d) with priority and arriving earliest 1h before
* number of fans entering after kickoff (average):
  * (a) 15.7
  * (b) 
  * (c) 
  * (d) 
* mean check-ins per hour:
  * (a) 15.7
  * (b) 
  * (c) 
  * (d) 


### Task 5
* is staying in a queue faster than switching queues?
* implement impatient visitor that switches queues **once** after a certain wait time threshold
* reasonable conditions for switching to another queue
* compare resulting waiting times to normal visitors

->
* 


## ToDos
* 2x/3x speedup simulation (arrival rates, pedestrian speeds, check-in times)
* (task 4) how to prioritize season ticket holders?
* (task 5) simulate impatient visitor
* report
