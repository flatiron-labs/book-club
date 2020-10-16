# AWS re:Invent 2018: Close Loops & Opening Minds: How to Take Control of Systems, Big & Small ARC337

> Speaker: Colm MacCárthaigh

> Notes Author: Crystal Chang

> Source: https://www.youtube.com/watch?v=O8xLxNje30M

* Control systems orchestrate how things function like a remote that turns on TV
* Open loop controller -> no feedback once signal sent out (ie. remote sends signal to TV, but never knows if the signal was actually received)
* Tradeoffs in designs in decreasing importance
    * Security
    * Durability/Correctness (ie. If system says it has user data, it definitely has it)
    * Availability
    * Speed
* Control planes vs Data planes
    * Control planes often a bigger design challenge than data planes they support
    * Poorly designed control planes can cause large outages/misconfigurations/data corruption
* What do Control Planes do in the cloud?
    * Manage lifecycle of resources
    * Provision software
    * Provision service configuration
    * Provision user configuration
* Control Theory
    * What makes stable control systems
        * Some kind measurement (ie. In autoscaling, this could be instance CPU usage)
        * Some kind of central controller (ie. Software or algorithm) that takes measurement and if the measurement is not in the desired state, it produces corrections to get measurement into desired state (ie. In autoscaling, decide to scale up)
        * Actuator -> the thing that gets done from the controller’s corrections, which causes a change in the measurement (ie. In autoscaling, launching a new instance)
    * Closed loop system -> constantly measuring, deciding, actuating
    * This type of system is sensitive to lag
        * If autoscaling took hours to launch instances, it’d be useless
    * Can dig further into PID loops if interested
* 10 Patterns for Controlling the Cloud
    * Pattern 1: checksum all the things
        * This is to catch corruption so it doesn’t propagate throughout the system
        * YAML files prone to corruption since they can be truncated and remain valid
    * Pattern 2: Cryptographic Authentication
        * Super important to keep control planes secure since they’re often connected to everything and are security critical systems. If a bad actor got access they could do a lot of damage
        * Encrypt and authenticate everything
        * Ability to revoke and rotate every credential along with watching out for certificate expirations
        * Prevent human access to prod credentials
        * Never allow non-prod control plane to talk to prod data plane
        * This is also just generally good for operational health
    * Pattern 3: Cells, Shells, and Poison Tasters
        * Limit blast radius of damage any error can cause
        * Divide control planes horizontally into regions, availability zones, and cells
        * Compartmentalize control plane so data plane insulated if control plane crashes
        * Poison tasters: check up front that change is safe
            * Little unclear how this occurs. He mentions running a change through as much of what the data plane is going to do as possible (ie. Serialization/deserialization) before even accepting the request. Does this mean things get done twice?
    * Pattern 4: Asynchronous Coupling
        * Synchronous systems are strongly coupled. 2 systems that are synchronously calling each other are really just one system
        * A problem in a synchronous downstream dependency has immediate impact on upstream callers
        * Retries from upstream callers can fan-out and amplify problems
        * Asynchronous coupling systems tend to be more tolerant
        * Can make partial progress even when some components are unavailable
        * Workflows and queues can be tuned to have deterministic retry behavior
    * Pattern 5: Closed Feedback Loop
    * Pattern 6: Small pushes and large pulls
        * Is it better to push or to pull?
        * Ex: should data plane hosts accept connections and be pushed configurations or should they connect to control plane and pull them
        * Answer is it depends on size of “fleets”. Do not want big fleet connecting to small fleet because you can’t cold start a system like that. Big fleet will hammer small fleet and it’ll never recover.
        * Long lived connections can support pushing timely updates regardless of direction of the connection
        * By connecting small fleet to big fleet you avoid overwhelming small fleet and causing retry storm
    * Pattern 7: Avoiding cold starts and cold caches
        * Caches are bi-modal systems, super fast when they have entries, slow when they’re empty
        * Actually advocates not have caches if possible because if you need to cold start a system and there are a large number of requests (“thundering herd”) hitting a cold cache, it’ll never get warm
        * If you have to use a cache, advocates for “self-warming cache” that primes itself before accepting requests
        * Even better recovery pattern is to serve from stale cache if the source is down. Stale cache is likely still correct state. Believes DNS resolvers should do this
    * Pattern 8: Throttles
        * Throttles and rate-limits can moderate problem requestors and dampen fluctuating systems so recovery is possible (this avoids retry storm issue)
        * Need to be careful so throttling doesn’t impact end customer experience
        * Ex: Amazon Elastic Load Balancer is built on a ton of EC2 instances. If a zone goes down, Amazon actually throttles ELBs recovery so that other customers can get their EC2 instances up faster
    * Pattern 9: Deltas
        * If there is too much configuration state to push around it’s more efficient to compute deltas and distribute patches
        * Can just version your data schema that is immutable and append-only (logical clock vs wall clock)
    * Pattern 10: Modality and Constant-Work
        * Using previous patterns, we can build a loosely coupled control plane, with deltas to minimize work, and throttles to keep things safe, but what if a lot of things change at same time? Say an entire region goes down at once?
        * System is lag sensitive so don’t want to build up backlogs and queues
        * At a high level, important to try to minimize the number of states a system can be in. If there are too many possible combinations, it’s impossible to test
        * Systems that change performance in response to workload or data patterns can be fragile
            * Ex. Relational DBs -> good for business queries, terrible for control planes. They have a lot of hidden optimizations. Query optimizer determines most efficient way to execute query by considering query plans (can involve changes to type of indexes to use, how joins/merges are occurring). Query plan flips can drastically alter performance
            * For control plane work, they stick to NoSQL DBs because how execution occurs is more obvious to engineer therefore easier to reason about and allows for stable systems. No hidden optimizations. Just always do it the “dumb” way. Ie. Full table scan, always full join
        * Constant-Work: used for AWS health checks
            * Instead of versioning and patching, customer makes change that just updates file with config on S3 and data plane is in a loop where it gets that file every 10 secs instead of any sort of pushed queue workflow
            * This doesn't build up backlog or queue and is really reliable
