# The Log: What every software engineer should know about real-time data's unifying abstraction

Author: Jay Kreps

[Source](https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying)

## Intro

Context:

Author joined LinkedIn as they began to move to distributed systems (circa 2007):

- distributed graph database
- distributed search database
- [Hadoop](https://hadoop.apache.org/) installation
- first and second gen key-value store

What concept do all these systems share? The Log, aka "write-ahead logs", "commit logs", "transaction logs".

## PART ONE: What is a log?

### Basics

- Simplest possible storage abstraction
- Append only
- Sequence of records ordered by time
- Unique seqential numbering
- Reads left to right

### Not that different from a file or table

- file: array of bytes
- table: array of records
- log: file or table where records sorted by time

### Logs in databases

- First appearance: unknown?
- Present in IBM's System R

#### Usage

- Ordering changes
- Distributing data
- Crash recovery
- Replication
  - example: "Oracle, MySQL, and PostgreSQL include log shipping protocols to transmit... to replica databases"
- Subscription
  - example: "Oracle has productized the log as a general data subscription mechanism for non-oracle data subscribers with their XStreams and GoldenGate"

> The use of logs as a mechanism for data subscription seems to have arisen almost by chance.

### Logs in distributed systems

Core design problem for distributed system: contract for ordering changes

"Log-centric approach" State Machine Replication Principle:

> If two identical, deterministic processes begin in the same state and get the same inputs in the same order, they will produce the same output and end in the same state.

Timestamp acts as unique identifier, clock for the state (allows you to time travel)

> As long as two processes process these inputs in the same way, the processes will remaining consistent across replicas.

#### Physical vs Logical logging

- Physical logging: logging the contents of each row that is changed
- Logical logging: logging the SQL commands that lead to the row changes (the insert, update, and delete statements).

#### Models

- "State machine model" ("active-active"): each replica keeps a log of the incoming requests and processes each request

- "Primary-backup model" ("active-passive"): one replica (the "leader") processes requests in the order they arrive and logs out the changes to its state, and other replicas apply the leader's state changes in order (so they're always in sync and ready to take over as leader should the leader fail)


### Changelog 101: Tables and Events are Dual

Real world example:

> The log is similar to the list of all credits and debits and bank processes; a table is all the current account balances.

- Changelog supports near-real-time replicas
- "Tables support data at rest and logs capture change"
- Sorta similar to source code version control (both have to manage distributed, concurrent changes in state)
- Source control sequence of patches is essentially a log


## PART TWO: Data Integration

Definition:

> Data integration is making all the data an organization has available in all its services and systems.

["ETL"](https://en.wikipedia.org/wiki/Extract,_transform,_load): one part of data integration, populating a relational data warehouse

Maslow's Hiearachy of Needs analogy:

- lowest levels: capturing all data (data and processing)
- middle levels: good data models, uniformity
- higher levels: sophisticated processing

Start by building a firm base of reliable, complete data flow.



### Data Integration: Two complications

1. The event data firehose

- Event data: records things that happen rather than things that are
- Examples: user activity logging, machine-level events, etc.
- There's lots of it


2. The explosion of specialized data systems

- Examples: OLAP, search, simple online storage, batch processing, graph analysis, etc.

### Log-structured data flow

> The log is the natural data structure for handling data flow between systems. The recipe is very simple:
> Take all the organization's data and put it into a central log for real-time subscription.

- Each logical data source can be modeled as its own log
  - App that logs out events
  - Writeable database table
- Subscribers read from log, apply, and move on
  - Cache, Hadoop, database, search (any data system)
  - Only knows about the log and not any details of the system of origin
- Log is a "buffer that makes data production asynchronous from data consumption"
  - Helpful when subscribes consume log at different rates

Note: log != pub sub

Log is "messaging system with durability guarantees and strong ordering semantics", aka an "atomic broadcast"

Discussion point:

> I have found that "publish subscribe" doesn't imply much more than indirect addressing of messages—if you compare any two messaging systems promising publish-subscribe, you find that they guarantee very different things, and most models are not useful in this domain.

### At LinkedIn

Early infrastructure:  
  - "databus", log caching abstraction to scale subscription to db changes
  - fed social graph and search indices

Early project for author:  
  - setting up Hadoop
  - move recommendation processes to Hadoop

Challenges:  
  - non-reversable data
  - too specific for batch processing
  - custom config => expensive setup for new data sources

Revelations:  
  - pipelines are super valuable
  - making data available => lotsa cool new possibilities
  - uniform structure => automatic data loading, less config time needed to add new data sources, faster time to higher data coverage

Goal:  
  - Unified, generic log
  - Interface between sources and subscribers
  - Chose Kafka as central pipeline

### Relationship to ETL and the Data Warehouse

- Data warehouse: batch query infrastructure
- Good for reporting, ad hoc analysis

- ETL: extraction and data cleanup process

Challenges:  

> ...incentives are not aligned: data producers are often not very aware of the use of the data in the data warehouse and end up creating data that is hard to extract or requires heavy, hard to scale transformation to get into usable form.

Solution:  
  - well-defined API for adding data
  - aka log, central pipeline

Rewards:  
  - Organizational scalability
    - easy to add new data sources
    - easy to build new reports

Recommendations:  
  - Cleanup data before publishing to log
  - Data shouldn't hvae any "leftovers" from its where it was made or stored (subscribers don't need to know any of these details)
  - Cleanup logic should be lossless and reversible

### Log Files and Events

- Enables decoupled, event-driven systems

### Building a Scalable Log



## PART THREE: Logs & Real-time Stream Processing

### Data flow graphs

### Stateful Real-Time Processing

### Log Compaction


## PART FOUR: System Building

### Unbundling?

### The place of the log in system architecture


## Final Thoughts

