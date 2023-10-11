**Contenuto**
- [[#Pervasive Computation & Interaction|Pervasive Computation & Interaction]]
- [[#Physical vs Computational|Physical vs Computational]]
	- [[#Physical vs Computational#Spatial distribution|Spatial distribution]]
	- [[#Physical vs Computational#Temporal distribution|Temporal distribution]]
- [[#Failure & Availability|Failure & Availability]]
- [[#Features of a Distributed System|Features of a Distributed System]]
- [[#Cap theorem|Cap theorem]]
	- [[#Cap theorem#Original theorem|Original theorem]]
- [[#Consistency, Availability, Network Partition|Consistency, Availability, Network Partition]]
	- [[#Consistency, Availability, Network Partition#Availability|Availability]]
	- [[#Consistency, Availability, Network Partition#Consistency|Consistency]]
	- [[#Consistency, Availability, Network Partition#Network Partition|Network Partition]]
	- [[#Consistency, Availability, Network Partition#Async Network Theorem|Async Network Theorem]]
- [[#Switching Strategy based on Partition Tolerance|Switching Strategy based on Partition Tolerance]]
- [[#Beyond ACID|Beyond ACID]]
- [[#BASE|BASE]]
- [[#CAP Today|CAP Today]]
- [[#Replication and Consistency|Replication and Consistency]]
	- [[#Replication and Consistency#Consistency|Consistency]]
		- [[#Consistency#Data-Centric Consistency Model|Data-Centric Consistency Model]]
			- [[#Data-Centric Consistency Model#Continuous Consistency|Continuous Consistency]]
			- [[#Data-Centric Consistency Model#Inconsistency (conit)|Inconsistency (conit)]]
			- [[#Data-Centric Consistency Model#Sequential Consistency|Sequential Consistency]]
			- [[#Data-Centric Consistency Model#Casual Consistency|Casual Consistency]]
		- [[#Consistency#Client-Centric Consistency Model|Client-Centric Consistency Model]]
			- [[#Client-Centric Consistency Model#Eventual Consistency|Eventual Consistency]]
		- [[#Consistency#Some Definitions|Some Definitions]]
	- [[#Replication and Consistency#Replication|Replication]]
- [[#Dependability|Dependability]]
	- [[#Dependability#Faults and Errors (chap: 8)|Faults and Errors (chap: 8)]]
		- [[#Faults and Errors (chap: 8)#Failure masking with Redundancy|Failure masking with Redundancy]]

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
2) communication channels (radio, cable, …)
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

---
## Replication and Consistency
Why replication?
- Increasing the **reliability** of systems.
- Improving **performance**.
- **Scaling**, both in number of nodes in the same machine and in different geographical areas.

In general, the benefits of distributed systems includes, reliability, **fault tolerance**, accessibility, performance and scalability.

Those benefits come with a cost, in terms of physical costs of machines and areas to host them (which must include some number of computation resources and a sufficient bandwidth), and **consistency**.

### Consistency
The notion of consistency can vary between use cases in a distributed system, for example an application could possibly not need all replicas to be up to date to the latest version. For this reasons, we define **models of consistencies**.

#### Data-Centric Consistency Model
The problem to face in those scenarios, is how to ensure consistency of data across distributed copies, and especially how to handle actions that are performed over data.

A way to look at this problem is to try to ensure data consistency only to the user level. When a user asks for data, it is not important that all replicas under the hood are up to date, but the consistency is built giving to him the most updated data in a replica of the distributed system.

This consideration leads to the following definition:

> A **consistency model** is essentially a contract among the *processes* and the *data stores*, ensuring the correctness of data.

So, once agreed on a set of rules (or protocol), consistency is ensured between process and data stores. Now the model has shifted focus from the *replicated data* to the *process using data*.

> [!info]
> It is important to note that the notion of "correctness" strictly depends on what the process expects.

##### Continuous Consistency
The goal of **Continuous Consistency** is to keep limits to **deviations** between replicas. The level of consistency is defined through three independent axes for deviation:
- *Numerical* deviation.
- *Staleness* deviations (Staleness$^{-1}$ = Freshness).
- *Ordering* deviations

##### Inconsistency (conit)
In the data-centric perspective, we measure deviation by the use of the traditional notion of **unit of consistency**, called **conit**.
**Conit** is a measuring unit that depends on the nature of the data store.  We then measure the **deviation** in terms of *difference of conits*.

##### Sequential Consistency
In a distributed environment, if i can define an ordering (not easy due to different clocks in different machines), I don't need to replicate all data, but i replicate the **order of the operations** that have been made. In this way, all update operations are seen by all processes in the same order.
In this way, the results of every operation that changes the state of the data store can be seen by all other processes **in the same order**, as if every operation was made *sequentially*: In this circumstance we talk about *Sequential Consistency*.

##### Casual Consistency
Formally, a data store is *casually consistent* when all processes see **write** operations that are in a **cause/effect** relation, **in the same order**.
Basically, every write operations causes some effects or actions, so most of the write operations create a "cause/effect" relation. With this kind of consistency, every process sees the same order of write operations that caused some effects. (very similar to the sequential, but only for those operations with cause/effect relationship).

#### Client-Centric Consistency Model
In this context, things are a little bit different. The main idea is that a **client connects with different replicas over time**, and the goal of *client-centric models* is to ensure that whenever a client connects to a new replica, **that replica** is **up to date**, according to the **previous access of the client** to the same data in other replicas.

In this scenario, **consistency** is **no longer** referred to the **resource itself**, but rather on the **view that the client has of the resource**.

##### Eventual Consistency
This is applicable to all those distributed data stores with a single authority updating, with many processes simply reading.
In this case, non-updated data may be provided to readers, but in most cases this inconsistency might be acceptable to readers (e.g. weather forecast of 10 minutes ago). Typically, if no updates takes place for a while, **gradually** all replicas **will become consistent**: this is called **eventual consistency** (eventual = prima o poi).

#### Some Definitions
**Monotonic Reads**:
> A data store is said to provide **monotonic-read consistency** if a process reads the value of a data item $x$, any successive read operation on $x$ by the process will always return that same value, or a most recent value

**Monotonic Writes**:
> A data store is said to provide **monotonic-write consistency** if a write operation by a process on a data item $x$ is completed before any successive operation on $x$ by the same process.

**Read Your Writes**:
> A data store is said to provide **read-your-writes consistency** if the effect of a write operation by a process on a data item $x$ will *always* be seen by a succesive read operation on $x$ by the same process.

**Writes Follow Reads**:
> A data store is said to provide **writes-follow-reads consistency** if a write operation by a process on data item $x$ following a previous read operation on $x$ by the same process is guaranteed to take place on the same or a more recent value of $x$ that was read.

The idea behind this, is that writes affect only **up-to-date** data items.

### Replication
Replication in DS, means deciding where, when and by whom replicas should be placed, and with which mechanisms replicas are kept consistent.
We can find in this two, similar yet very different problems: (i) placing *replica servers* and (ii) placing content.

- Most of the time, replication does not mean replicating data, but most of the time,  **services could be replicated**: this means replicating functions which may or may not insist on the same data store.
- For the same reason of data store replication, **processes** could be replicated. This might require cloning, or more higher-level mechanisms like goal passing.

This means that replication is harder than we could think, and it involves not only data and databases (yet they remain one of the main focus), but also entire services and processes or any kind of resource we could possibly need.

---
## Dependability
Distributed systems must be dependable; this means that it has to esure:
- **Availability**
> Refers to the property that a system is ready for **immediate use**.
> - It is the probability that a system is operating correctly at any given moment.
- **Reliability**
> Refers to the property that a system can **run continuously** without failure.
> - It is defined in terms of a time interval (so high reliable systems are most likely to keep on running fo a long time)
- **Safety**
> Refers to the situation that when a system temporarily fails to operate correctly, **nothing catastrophic happens**.
> - Difficult to be defined and ensured.
> - Catastrophic refers to those states when there is no established path from fault back to normal operation.
- **Maintainability**
> Refers to how easily a failed system can be repaired.
> - Maintainability is closely related to availability.
> 	- Highly-maintainable systems may also show a high degree of availability.

### Faults and Errors (chap: 8)
We can define **failure** when a system does not behave as promised, where an **error** is part of this system state that have caused the failure.
Is clear that Dependability is closely related to **Fault Tolerance** and in controlling faults. Controlling faults can be distinguished in three different activities:
- **Preventing** faults.
- **Removing** faults.
- **Forecasting** faults.

In every cases, every distributed system must ensure fault tolerance, meaning that the system always try to provide its functions eve in the presence of faults. The most basic way to hide the presence of faults in  a DS, is via *software-redundancy*.

We can define a taxonomy of faults:
- **Transient Faults**: they occur once, and then disappear.
- **Intermittent Faults**: they occur and the vanishes, and then reappears, and so on. Those are then so called "errori cancro", because when someone says "here is the fault", you don't make it in time to come to they're position that the fault disappeared! sarà roba ciooooooooooooooooooooooooooooo.
- **Permanent Faults**: they keep on existing until the faulty component is fixed/replaced.

Here is some failure models:
![[Pasted image 20231006190126.png|center|400]]

#### Failure masking with Redundancy
As said before,  we can hide failures from other processes through redundancy. The redundancy can involve:
- *Informations*, for example extra bits in data (e.g. Hamming codes).
- *time*: redoing the transactions after no responses.
- *physical*

## Computational Process
The elementary computational process is **sequential**, so every operation is done one at the time. This type of machine has:
* *input / output*
* *context*
As a result, in the following a *computing machine* is the place where a *computational process* occurs. 

The context can be:
* computing machine
* resources
* time
* space
all of them are *relevant* to model in order to understand the dynamics of the *computational process*. 

### Context for computation

* *timed computation*: whenever the time of the computational machine is **relevant/essential** for the computing process
* *spatial computation*: whenever the *spatial features* of the computational machine are **relevant/essential** for the computing process
+ *situated computation*: whenever the *environment* of the computational machine is **relevant/essential**. The *environment* is any meaningful combination of **temporal** and **spatial**

Understanding a *computational process* requires the precise definition of its computational context. Computational process **depends** on how we define the features of the context. 

## Computational System

In a computational system, two or more computational process:
* **behave** by computing
* **work together** by interacting

### Type of Computational System

1) *Parallel Systems*
2) *Concurrent Systems*
3) *Distributed Systems*

#### Parallel System

The **parallel computing** is typically used for non-sequential computing process, where more than one computation can be performed *at the same time*.  It typically requires a *multi-core architectures* and i can be used to solve *computationally - intensive* problems. A parallel system is a computational system performing parallel computations. 

##### Parallel Computation

We talk of *parallel computation* whenever the **temporal context** is the same fo all computational process

#### Concurrency System

There are two terms for the concurrency system:
1) **interleaving**: where events occurring in separate concurrent process could occur in any relative order. 
2) **true concurrency**: where partial orderings are used to explicitly capture temporal relations between events. 
A concurrent system is a computational system performing concurrent computation. 
##### Concurrent Computation
We talk of concurrent computation whenever at least two computational process have a different **temporal context**. 


#### Distributed System
The term refers to a number of *asynchronous* computational process located on different devices and communicating via message passing. Is an activity performed on a **spatially** distributed system. This type of systems are a collection of devices working together through a network connection. The focus is on the **spatial distribution of devices**.  A distributed system is a computational system performing distributed computations. 

##### Distributed Computing 
In **distributed computing** the focus is on the spatial distribution of processes. The **spatial context** defines the Distributed Computing and the Distributed System.  A **distributed computation** is whenever at least two computational process have a different **spatial context**. 


#### Parallel vs Concurrency

* In *parallel systems* the events are totally ordered
* in *concurrent system* events are at most partially ordered
**This two systems have a different temporal context**

## Agreement Problems

Agreement problem: When the different components of a system have potentially divergent views over the system state. A *coherent* overall system behaviour can be achieved only when all the components come to **agree** about everything relevant for the system. They have to reach the *same conclusion*. 

### Components and Connectors

Non trivial computational systems are *concurrent* or more generally *distributed systems*, correspondingly concurrent / distributed systems are typically modelled as collections of computing process or devices, interconnected as to interact. 

The time model can be:
* **sync**: when all computations have the same time reference
* **async**: otherwise

The **fault tolerance** is the general property of distributed systems to keep working beyond faults. 

### Consensus

A fundamental problem of *fault tolerant* distributed computing is for the *reliable* process to reach **consensus**. The **consensus** is the process by which we reach *agreement* over system state between *unreliable* machines connected by *asynchronous* networks. 

The basic form: achieving consensus on a **single bit**: 
* each processor has an initial bit
* a fixed number n of processors
* the single bit consensus problem is for the non faulty process to agree on a bit, called **consensus value**, y
**Solvability** depends on the existence of a protocol such that all *non faulty* processors terminate with the same value y. 

The goal of the protocol is for the *non faulty* processes to agree on a vector y, called **consensus vector**. The consensus is about what any processor thinks about the initial value.

### Faults 

Look for an agreement protocol that is reliable as possible in the presence of such faults. So the best that one can hope for is a protocol that is **tolerant** to a prescribed number of "expected" faults. 

## Fischer Lynch Paterson

In a fully asynchronous system, no *consensus* protocol can tolerate even one single *crash failures* under the mere requirement of *non triviality*. Even the simplest case leads to impossibility results. 

### Paxos

* Two phase process:
	1) *promise*
	2) *commit*
* Majority agreement
* Monotonically increasing numbers

### Paxos steps

1) Values are proposed
2) no single acceptor for proposal, multiple acceptors
3) *quorum*: if the bare majority of acceptors, then it is chosen
4) once a value has been chosen, future proposals must propose the same value

In order to perform this algorithm there are needed two phase:
1) In the first phase need to figure out if any value has already been chosen
2) Propose accordingly in the second phase 

### State Machine Replication

All distributed replicas of a replicas of a resource need to agree on the same state over time. State machine approach is a general method for implementing fault tolerant services in distributed systems. 

* The same state machine is replicated over a distributed system
* Each one has a consensus module
* Any operation over any replicated machine is performed only if and when all machines have agreed over the same ordering execution

Need consensus over an array of values.

---

## Distributed Systems

A *distributed system* can be defined as a collection of *autonomous computational* entities conceived as a single coherent system by its designer. A distributed system is made of: 
* independent computational entities
* no assumptions on their individual nature 
* heterogeneity
A distributed system can be seen as a single coherent system. We have in a distributed system:
* physical distribution of components
* network base communication
* uncoupling in terms of control 

### Issues

* *Collaboration*: in order to achieve coherence manu autonomous entities should collaborate as a single system
* *Amalgamation*: in order to achieve uniformity mani *heterogeneous* entities should *amalgamate*

## Middleware

A distributed system is organised around a **middleware**, the *middleware layer* extends over multiple machines, and offers each application the same interface. 

Through the *separation* the middleware layer:
* *enables* meaningful interaction between autonomous distributed components
* communication issue
* hides differences in technology, structure and behaviour 

---
### Distributed Ledger Technology Blockchain as Middleware

## Middleware 

The middleware lies in the middle between the operating system and the applications. The middleware is developed once for many applications and it can abstract from the specific OS. 

A key feature of the middleware is **interoperability**:
* applications using the same middlware can interoperate
* this is true of any common platform

### Models from middleware to applications

Being asymptotically the most cost effective when development time goes to zero. Adopting a given middleware should ease both new application development and legacy integration. *Middleware* tries to cast a **model** on heterogeneous applications.

### Abstract vs Concrete Middleware

* ***abstract middleware** a common model
* **concrete middleware** a common infrastructure

*standardisation efforts* become critical to build momentum around infrastructure technology. Now we need:
* authentication
* authorisation
* security
* distributed access to shared resources

### Distributed Ledger Technology

**Distributed Ledge Technology** refers to process and related technologies that enable nodes in a network to securely propose, validate and record state changes to a *synchronised ledger*. The ledger is synchronised. 

* **ledger**: information store that keeps records of transactions that are intended to be final, definitive and immutable
* **distributed ledger**: ledger that is shared across a set of DLT nodes
* **distributed ledger technology**: technology that enables the operation of distributed ledgers. 

* Distributed systems are typically required to be open
* shared **standards** works at the core of any open system
* middleware is the most obvious place for standards
* standardising middleware as the most general foundation

DLT is a secure, cost-effective technology that enables the deployment of globally scalable services, the DLT is considered as temper resistant and auditable technology that is resistant to *systemic failures*. 


### Blockchain
A Blockchain is a way to implement a distributed ledger, but not all distributed ledgers necessarily employ blockchains. 









