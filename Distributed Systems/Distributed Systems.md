

----
# Distributed Systems

## Pervasive Computation & Interaction 

Nowadays computational systems have become more *pervasive*, since they are everywhere. The huge number of computations are **distributed**, concurrent computations either controlled/triggered, or *autonomous* computations. 

Every system comes equipped with ICT technologies for *interacting* with other computational systems. 

## Physical vs Computational
The physical nature of artificial systems adds complexity to computational systems in terms of:
* **spatial distribution**:
* **temporal distribution**
* **unpredictability** of the environment
There is no determinism, there are multiple computational units that works together. 

### Spatial distribution

1) computational unites
2) communication channels (radio, cable, ...)
3) data/information/knowledge
4) sensor, actuators (from where the data are get)

### Temporal distribution
There is no a temporally sequence of events, everything can happen at any time. 

1) *events*: things happens, yet no longer in a clearly-ordered sequence, and also the events are *scattered*. 

System events no longer constitute a totally ordered set, admissible interactions among systems components no longer depend on compresence. 

The Spation-Temporal unity of systems is lost, there is no longer a notion of *system time*, nor a *system location*. The system components are only **partially correlated**, *temporally & spatially*. 

----
# The Cap Theorem

## Failure & Availability 

When a system can hide it failures, it is basically always working (by running other machine in order to cover the problem), it is **highly available**. 

## Features of a Distributed System

The distributed systems should be:
1) *consistent*: behave correctly, always expect to be correct
2) *available*: the system should work, always running
3) *unreliable*: recover up if the system crashes

## Cap theorem

*CAP* theorem, it is only possible to *simultaneously* provide two of the three following properties:
* *consistency*
* *availability*
* *partition tolerance*

### Original theorem
A *distributed database* potentially features three desirable properties at the same time:
1) Consistency
2) Availability
3) Tolerance towards network partition

The three properties are not exactly of the same sort, both technically and conceptually. All of them are desirable, yet forfeiting partition tolerance is not really an option in real-world systems. 


According to the CAP theorem, any *shared-data* distributed system can have at most two of these three properties.
We always have to pick one of the properties and live without it. The (no)*CAP* theorem forces us to choose between *availability* and *consistency*. 

## Consistency, Availability, Network Partition

### Availability
For a Distributed System to be continuously *available*, every request received by a non-failing node in the system must result in a response (maybe not the one that we want). 

"*if the system is available, we got a response*". 


### Consistency 
A *consistent* service is modelled as an atomic data object where:
* Operations are totally ordered
* Each operation occurs in a single instant of time

*Consistency implies that all read operations over a distributed shared memory occurring after a write operation completes must return the value of either this write operation or a later one*.

"*if the system is consistent, we got correct responses*". 

### Network Partition
When a network is partitioned, all the messages sent from nodes in one component of the partition to nodes in another component are lost. 

"If a node A send a message to node B, the network is partitioned if the message does not make it to B". 

* The *availability* is when B, receives the message and responds
* The *consistency* is when B response is correct

### Async Network Theorem
"It is impossible in the *asynchronous network* model to implement a read/write data object that guarantees the following properties:
1) Availability
2) Atomic Consistency"

**Assumptions**:
1) Nodes in the network can be partitioned in two disjoint, non-empty sets G1, G2. 
2) Atomic object *o* has initial value $v_0$
	* *o* is expected to be consistent through G1 and G2
3)  $\alpha_1$ executes a single write $v_1 \neq v_0$ in G1
* **NO MESSAGES ARE SENT/RECEIVED BETWEEN THE TWO NODES**
4) $\alpha_2$ executes a single read of *o* in G2
* **NO MESSAGES ARE SENT/RECEIVED BETWEEN THE TWO NODES**
5) due to availability, $\alpha_1$ completes ($v_0 \rightarrow v_1$) and $\alpha_2$ does too
6)  G2 just sees $\alpha_2$ and must return $v_0$

This obviously violates consistency.
## Switching Strategy based on Partition Tolerance

1) When the network is partitioned, a distributed system should choose a tradeoff between *consistency* and *availability* (point out the problem). 
2) When there is no partition, a system can feature both *consistency* and *availability*

## Beyond ACID

*ACID* semantics might be too strong, because:
* The design space for network services can be partitioned according to the data semantics that each service demands, the knowledge is partitioned (Meteo Cesena, cazzo mene se meteo Mosca è sbagliato)
* For other internet services, is not necessarily strong consistency or durability, but rather *high availability of data*. 

## BASE

BASE (Basically Available Soft State Eventual Consistency)
* **Stale data** can be temporarily tolerated as long as all copied of data eventually reach consistency after short time.
* **Soft state** the data is not durable, I get only a part of the entire data.
* **Approximate answers** delivered quickly may be more valuable than exact answers. 

Most of the cloud services adopts *BASE*, and try to mask *inconsistencies* from users.

## CAP Today

The modern *CAP* goal should be to maximise combinations of consistency and availability that make sense for the specific application. Such an approach incorporates plans for operation during a partition and for recovery afterwards. 
