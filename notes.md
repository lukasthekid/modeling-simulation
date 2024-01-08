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
* set reasonable arrival rate _r_ of visitor (as time between arrivals)
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
* priority: 
  * dedicated queues for season ticket holder
  * season tickets can use any queue, standard tickets only non-priority queues
  * number of queues:  
    according to expected load on queues  
    $n_q \cdot \frac{v_{st} \cdot t_{st}}{v_{std} \cdot t_{std} + v_{st} \cdot t_{st}} = 7 \cdot \frac{2400 \cdot 3}{3600 \cdot 6 + 2400 \cdot 3} = 7 \cdot 0.25$  
    $n_{qst}$ - number of season ticket priority queues  
    $n_q$ - total number of queues  
    $v_{std}$ - number of standard visitors  
    $v_{st}$ - number of season ticket visitors  
    $t_{std}$ - average check-in time standard visitor  
    $t_{st}$ - average check-in time season ticket visitor  
    we round up, so that **2** of the 7 queues are priority queues for season ticket holders only
  * implementation: send standard visitors to the shortest of the first 5 queues
    ```
    security.getQueues().subList(0, 5).stream().min(Comparator.comparingInt(q -> q.size())).get();
    ```
  * problem in AnyLogic-model: Agents seem to decide for a queue right when spawning instead of near to the queues. Therefore, often a chosen queue has turned into the longest queue, when the agent has arrived at the queue.
  * results are determined with Monte-Carlo-Simulation with 10 iterations and averaged
* implementation of late arrival: Delaying the spawning of agents from a PedSource does not seem to be possible. An alternative idea is to discard each visitor until a certain timestep. For this a selectOutput-node was used with a condition like
    ```
    time() > 1800 || pedSink2.countPeds() > 800
    ```
    which sends each visitor directly to an alternative sink until the delay time has passed (the condition also makes sure that at least 2400 agents remain).
    The discarded visitors need to be considered in the total agents emitted by the source and the interarrival rate. The parameters for the subscriber-source are adapted as follows:
    * subscribers arriving earliest 1.5h before:
      * interarrival rate: **poisson(2.25)**
      * max. number of arrivals: **3200**
    * subscribers arriving earliest 1h before:
      * interarrival rate: **poisson(1.5)**
      * max. number of arrivals: **4800**
* number of fans entering stadium after kickoff (average):
  * (a) 93.9
  * (b) 164.4
  * (c) 256.6
  * (d) 890.0
    in this case the service-points are clearly overwhelmed
* mean check-ins per hour:
  * (a) 3007.9
  * (b) 2991.8
  * (c) 2999.5
  * (d) 2651.4
* mean waiting time in queue in seconds (standard visitor, season ticket holder)
  * (a) 
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
