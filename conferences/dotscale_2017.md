% DotScale 2017 Summary
% Alexis 'Horgix' Chotard - Xebia

# Introduction

Hello, this is my summary of the dotScale 2017

- Photos: https://flic.kr/s/aHskVVNvzx
- Videos: https://www.dotconferences.com/conference/dotscale

# Scaling trust

## Speaker

- David Mazieres
- Professor of Computer Science at Stanford ( https://cs.stanford.edu/ )
- Chief Scientist at Stellar ( https://www.stellar.org/ )
- http://www.scs.stanford.edu/~dm/

## Introduction

What if you want **all** Certificate Authorities in the world to **agree** on
something?

**Problem: who are "all" CAs?**

- The 180+ CAs with 65+ owners in Mozilla's root CA list?
- The root CA set shipped in your OS distribution?
- Your organization in-house CA that isn't globally recognized?

Really want all of the above for *all people*

## Application 1: global timestamp service

- Certificate Transparency (CT) provides trusted logs alongside CAs
- Generalize CT logging to leverage logs for timestamping documents?

Problem: which log to use?

- Different people trust different logs authority
- Don't know in advance to whom you will need to prove timestamp

What if your log choice proves untrustworthy? Example: "Google reducing trust
in Symantec certificates following numerous slip-ups"

**Using Internet-Level-Consensus (ILC) for timestamps would avoid this
problem**

## Application 2: Software transparency

- In 2016, FBI ordered Apple to sign a compromised bootloader
- Apple appears to have refused, but how can we know for sure?

Make software updates visible through *software transparency*

- Devices refuse to install updates not in public log
- Log intergrity secured through ILC. Instead of trusing 1 thing, all the world
  can agree

**Binary transparency and secure package management can both benefit from ILC**

## Application 3: internet payments

- Suppose you want to send $1 to Nigeria over the Internet
- It may require multiple banks, currency trades, etc.

- Need to avoid getting stuck or allowing double spending
- ILC can secure atomic transactions across multiple organizations... even
  organizations with no prior relationship!

**Technique currently in use by Stellar payment network**

## Background: byzantine agreement

Practical solution to consensus among N nodes:

- Pick *T* such that any *T* nodes constitute a quorum
- Tolerated faulty nodes that crash or send contradictory messages
- Safety requires: # failures < f(S) = 2T - N - 1

- Hence, any two quorums share a non-faulty node, can't lose history

- Liveness: # failures < f(L) = N - T (1 non faulty quorum)
- Typically N = 3f + 1 and T = 2f + 1 to tolerate f(S) = f(L) = f failures
- Problem: at internet level, can't enumerate N nodes

## FBA : Federated Byzantine Ageeeement

Generalize byzantine agreement so participants determine quorums in
decentralized way

Each node *v* picks one or more *quorum slices*:

- *v* only trusts quorums that are a superset of one of its slices
- If you care about an authority, put it in all your slices

Definition of FBA System:

> An FBAS is of a *a* set of nodes *V* and a quorum function *Q*, where Q(a) is
> the set slices chosen by node *V*

## Tiered quorum slice example

- Like the Internet, no central authority appints top tier
- But market can decide on de facto tier one organizations
- Don't even requires exact agreement on who is a top tier node

## FBA fault tolerance

- For safety, every two quorums must share a correct node
- Conceptually remove all ill-behaved nodes from all slices
- If two disjoint quorums result, can't guarantee safety

- For liveness, well-behaved nodes must form a quorum
- Otherwise, depend on failed nodes to reach agreement

## The *Stellar Consensus Protocol* (SCP)

- FBA protocol in production use by Stellar payment network
- Guarantees safety if every two quorums share honest node
- Optimal, as otherwise it can't guarantee safety
- Guarantees a well-behaved quorum will not get stuck
- Core idea: **federated voting**

## SCP : high level view

Phase1 - Nomination:

- Nodes nominate values
- Propagate and converge on set of nominated values
- Deterministically combine nominated values into composite value x
- Problem: impossible to know when protocol has converged

Phase2 - Balloting:

- Similar to Byzantine Paxos, but with federated voting
- Works (less efficiently) even when Phase 1 hasn't converged

## Conclusion

Links:

- www.stellar.org/papers/stellar-consensus-protocol.pdf
- IETF internet level consensus ML : www.ietf.org/mailman/listinfo/ilc


# Chaos management during a major incident

## Introduction

> Failure free operations require experience with failure - Richard Cook

This talk will be war stories and frameworks and how to deal with failures

## A story about failure

### Chapter I - "This is fine"

Story:

- Almost every engineer I knew was on the call
- 60 or 70 people
- Someone even dialed in from a Bar!

- Most people were doing the same task.
- We had no clue where to start

### Chapter II - Dark and stormy night

Nobody to coordinate

### Caphter III : The exec-swoop

> "Can you send me a spreadsheet with a list of affected customers?"

Not working on fixing the actual problem, but everyone ended up running a
script at the same time to know which customers were impacted

### Chapter IV - The morning after

> "You're the person that can be blamed for this incident and the loss of $$$"

- Burden of doing the root cause analysis and blaming people
- What's wrong with the picture?

## Define, Prepare, Measure

- **Define** a business metric and have the entire company care about it.
  Online retailer like Amazon? Monitor your orders number!
- **Prepare** the infrastructure for this changement
- **Measure** the impact, and get a feeling of the system

- Failures should be unique; if not, automate the response.
- Example: do not page the entire company for a full disk => auto recover from
  it by a script

- Single responsibility principle
- One invidiual should be working on exactly one thing on an incident

### Role: The Subject Matter Expert

- Someone who can come on a system and figure out what is failing
- Doesn't mean there is only one

### Role: The Incident Commander

- Someone who acts as the **single source of truth** and **orchestrating
  people**
- Notify that this is a major incident
- Verify that all SMEs are present on the call
- Divide and conquer: bring down the entire issue into smaller tasks and
  dispatch them across experts, and check back with them
- Communicate effectively: avoid the bystandard
    - Don't say "Please say yes, if you think this is good"
    - Do ask "Is there any strong objection to that?"

### Role: The Deputy

- Hot standby and assist the incident commander
- Get all SMEs up to speed about what's happening
- Liaise with stakeholders

### Role: The Scribe

- Documents the timeline of an incident as it progresses

### Role: Customer Liaison

- Imagine you're a cloud provider and you just went down: big customer impact
- Ok, many engineers are working to fighting the incident
- That's when we need a customer liaison that's responsible to communicate with
  customers to make sure they know that you're working on it, and which can
  communicate advancement
- Keep the incident commander apprised of any customer informations/feedback

## Misc

- Transfer of command if necessary
- Long running incident: it is OK to be tired, just pass the work to someone
  else
- Need of blameless post-mortem

- Review (Human-side)
- Shit happens, prepare for it.
- Develop on-call empathy. Companies do not need on-call heroes.
- People are your most valuable asset. Don't burn them out doing something that
  can be automated.
- Do not trigger a major incident for every system incident that you see. That
  should be reserved for something that is missions critical and assessed by
  metrics.

## Conclusion

- Just breathe, that helps a lot :D
- At the end of the day, just respect people for their time
- Organization learn as they fail? Or it's possible to be prepared? Dual sided
  thing. Many things are identifiable by simulations, but you can't simulate
  and prepare for everything


# Searching for the Server in Serverless

## Speaker

- Clay Smith
- Technologist at New Relic ( https://newrelic.com/ )
- https://twitter.com/smithclay
- https://github.com/smithclay
- https://clay.fyi/

## Introduction

- Simple app architecture with FaaS
- Functions + API Gateway
- Is this going to (not) work for me?

1. **Invoke**: event trigger. Things like file upload, HTTP request, but also
   more exotic things like infrastructure : VMs spinning up or shutting down,
   etc
2. **Run**: function invoked by the trigger
3. **End**: Result or Error or Timeout

## FaaS : typical metrics

- Error count
- Function invocation count
- function duration (ms)

Last 2 directly impact how much you're going to pay the service provider!

Cold start vs Warm start

- **Cold**: create + initialize + handler
- **Warm**: only handler because it already got loaded

## Lambda running commands

Here the speaker was trying to "reverse-engineer" how Lambdas on AWS are
working and are being run :)

- Lambda discovery v2 with SSH Server
- Terrible idea :D
- Massive a number of dependencies for an SSH server to run
- Lambda don't allow inbound connection...
- ... but it can open a tunnel...
- Got a terrible "lambda shell" to discover interesting things

- Info from /proc and can read and write it...
- => Containers are involved
- But a lot of data in /proc predate of cgroups
- Like : cpuinfo 2x Intel Xeon, /proc/meminfo , /proc/modules , etc
- Almost exactly a c4.large on EC2 compute optimized instance

## Lambdas on a VM

- c4.large instance with a 10Gbps connection
- Lambda = 128MB Function
- Packing densely

Cold start discovery in Code : https://github.com/smithclay/lambda-proc-info

## Warming methodology

- Scheduled event, cycles for a 4 minute interval => lambda
- Call the function to make sure it stays warm
- Only effective for non concurrent operations

## Lambda cold start: is it a constant?

- For this function, for this region, etc... approx 7-8 hours
- Can see it hopping from EC2 instance to EC2 instance
- Hostname of the host EC2 itself, not the container!
- Doesn't appear to stick around long, just a couple of hours
- No real pattern for the subnets it runs into but we can see it cycle across
  the 3 AZs in us-west-2

## Design your own FaaS

- High availability (multi-AZ or region)
- Elastic CMs and Automagic Freezing Containers
- Really good scheduling algorithm

## FaaS : No silver bullet

"I've got a quick, **computationally intensive** task that I need to perform
**occcasionally** in response to a **well defined event** that isn't that
sensitive to latency" - The ideal FaaS Developer

Example: generating images thumbnails

Last word : measure and share :)


# Automation

## Speaker

- Gary Bernhardt
- Lead Maintainer of Ansible ( https://www.ansible.com/ )
- https://twitter.com/thejimic
- https://github.com/jimi-c

## Introduction

- wat lightning talk ; Note from myself, in case you didn't see it, go and
  watch it now, it's 4min17 : https://www.destroyallsoftware.com/talks/wat
- Watomation

- War stories of using automation in a less optimal way
- Automate everything

## Example

- Facebook outage, September 24th, 2010
- Time warner outage prompts investigation on reliability, September 4th, 2014
- AWS S3 outage of course! "I don't always use automation, but when i do, I
  check my variable inputs first" :D

- Not a problem with automation, but with the lack of it
- Lessons netflix learned from the AWS outage, April 29th 2011

## Why these outages, despite automationn?

Out environments are becoming increasingly complex:

1. Manual steps == human error
2. Microservices are popular, but even simple LB/web/middleware/db setups can
   have dozens of failure points
3. Failure to automate rollback/failover

*"Shoot and pray"*

A lot of older systems exist, which have to be interfaced with, and generally
don't provide a lot of modern datacenter protections. Example: Mainframe!

## What can we do ?

- Keep calm and automate all the things
- Automation at least allows us to avoid mistakes we already did in the past by
  automating it

## What else can you automate ?

- If it has a remote API, you can automate it (with Ansible)
- Example: even lightbulbs! https://github.com/jimi-c/hue

## Network Ops

In 2016, almost all major internet service outages were caused by one of two
problems:

1. DDoS attacks
2. BGP configuration mistakes

## Best practices

1. Use built-in modules before reverting to shell/script commands
2. Prefix variable names, especially for something generic like "port",
   especially when using them with Ansible roles
3. Keep it simple


# Deep DevOps

## Speaker

- Andrew Shafer
- The little devop that could
- https://twitter.com/littleidea
- https://github.com/littleidea
- https://stochasticresonance.wordpress.com/

## Learning to learn

- Were are we?
- How we got here?

- Operations is the secret sauce.
- "You can either easily manage complex systems at scale... or you can't"
- Been using that same slide for the better part of a decade
- Same tools, same advice, drastically different results
- What, how and why you automate is as important that you do
- Containers everywhere
- "If Tetris has taught me anything, it's that errors pile up"

## Why > what

- Pareto and inefficient Nash Equilibrium rule everything around you
- Nash equilibrium - no one will change

- Punctuated equilibrium
- Evolutionary gradualism is virtually non-existent in the fossil record
- Evolution in the fossil records comes in sudden jumps (and extinction events)

- Nash Equilibria until death do us part
- ... lose if you keep playing the same way

## What is the devops?

- Developers and Operations can and should work together
- System administration evolving to look more like software development
- Evolving together as global community sharing solutions

## CALMS

- Optimizing human performance and experience operating software...
- "I push a button, people bring me food, it's awesome"

- software is changing everything... including software... and organizations

- You are either building a software business...
- or you will be losing to someone who is

- Yu are either building a learning organization...
- or you will be losing to someone who is

## What they really want

Everyone wants the devops... but what they really want is:

- scalability
- availability
- reliability
- operability
- usability
- all of that for free
- and without changing anything!

"Continuously DevOps microservices", Bingo!

- DevOps as SRE is spoken at scale. At GoogleTM
- Not that Google is the best at every possible thing, but where is your book?

## SRE

- Developers and operations can and should work together
- Solving system administration with software

Homework:

- Embracing risk
- Eliminating toil
- Service Level Objectives
- Bonues : communication and collaboration in SRE

## Why > what

- Google is an organization that changes
- They have built into their system this process organization changement

- Who puts as much effort into designing organizations as our computational
  systems?
- How many of our orgs are able and willing to change ?
- You haven't learnt anything until you change your behavior (ex: music, chess,
  etc; until you changed and decided to play you weren't learning it)

- The learning organization is one that has the capacity to integrate people
  and sructures...
- No one originally set out to do devops, continous deliver, microservices,
  these were natural consequences
- **Don't fixate on the words, don't fixage on the tools, fixate on outcomes**

- **principles > practices > tools**
- **mindset > skillsete > toolset**
- **adapt > adopt**

- The problem is neither technical nor social
- The problem is socio-technical
- We have to solve both together


# Distributed systems should operate themselves

## Speaker

- Benjamin Hindman
- Co-creator of Apache Mesos ( http://mesos.apache.org/ )
- Co-Founder & Chief Architect at Mesosphere ( https://mesosphere.com/ )
- https://twitter.com/benh
- https://github.com/benh

## Introduction

- Distributed systems **are hard to build**
- For this talk : distributed systems != most orgs, stateless independant
  services. We're talking about distributed systems with state, replication,
  etc

## Distributed systems are hard(er) to operate

1. Download
2. Deploy
3. Monitor
4. Maintain
5. Upgrade -> goto 1

## Deploy

- fault tolerance
- + high availability
- + latency
- + bandwidth
- + CPU/mem resources
- + ...
- **= configuration**

- Most of us do this by the book ("Hadoop Operations", etc.) and infer from the
  book what we need to do.
- To do that today, we express this configuration by 1: express to Chef,
  Puppet, Ansible, Marathon, Swarm, K8s, whatever. which gets us to 2:
  orchestrate

## Maintain

- First - Debug
    1. Usually start back at the book
    2. Look on the internet
    3. Ask friends
- Second - Fix (scale, patch, etc)
- Then, a week later, debug again...
    - Hopefully not the same thing :D
    - But the circumstances are the same
- Finally, write **code** so it never happens again...

## Upgrade

Sad state of distributed systems upgrade currently.

Thesis: **distributed systems should (be able to) operate themselves; deploy,
monitor, upgrade, ...**

Why:

- Operators have *inadequate knowledge* of Distributed Systems needs/semantics
  to make optimal decisions (even after reading the book)
- Execution needs/semantics can't esasily or efficiently be expressed to
  underlying system, and vice versa

## Example: Hadoop Map/Reduce

1. Express
2. Orchestrate

- Some people don't realize that map needs more ressources than reduce
- Configuration spectrum: coarse-grained - fine-grained

- **Coarse grained**: easiest to express (how most of us would do it), but
  worst resources utilization
- **Fine grained**: hardest to express (if even possible) but best resources
  utilization

## Why can't hadoop decide this for me in the first place?

- Applications "operate" themselves on Linux; when an application need to
  "scale up" it asks the OS for more ressources
- Syscall interface: memory allocate, clone/fork, create file, read/write, ...

But it wasn't always like this. Once up a time... before virtual memory... we
preconfigured the amount of memory we gave to the application and it took
ohysical memory address range as an **input**

## How

Distributed systems need **interface to communicate** with underlying system,
and vice versa (and the vice versa is actually critical)

- Interface: resources allocation, launch container/VM, create storage,
  attach/detach storage, ...
- Just like applications on Linux

## Learning from history... bidirectional interface:

- Coming back to this vice versa... the OS able to talk back to the app?
- Operating System should be able to callback into application
- Callback interface: paging/swapping, CPU deallocation, ...
- Better than LRU: ask the application what pages to swap!
- Example: back pressure! Same with CPU deallocation: search for "scheduler
  activations" and "lithe composition"

- Intel threading building blocks
- Intel math library

## Consequences of inadequate interfaces for parallel software...

- Operating System has inadequate knowledge of applications execution
- Needs/semantics to make optimal decisions; back to application execution
  needs/semantic can't easily or efficiently be expressed to operating system,
  and vice versa.

## Abstractions

- Bigger picture: abstractions exist for good reasons, but without sufficient
  communication they force sub-optimal outcoomes...
- Comparison: managers exist for a good reason, but without enough
  communication they force sub-optimal choices

- Distributed Systems need bidirectional interface too
- Callback interface: container/VM failed, resource deallocation, ...
- Resource deallocation example: tell the distributed system about "planned
  failures" (i.e. maintenance) so it can react to it and stop scheduling tasks
  on a node

## Apache Mesos

- Distributed System <-> Apache mesos
- Apache Mesos + Mesosphere Marathon (or Apache Aurora)

1. Express: user to Marathon
2. Orchestrate : Marathon to Mesos

Swarm or Kubernetes is just the same: express and it orchestrates for you

*Does {marathon, swarm, k8s} have adequate knowledge of distributed systems
execution needs/semantics to make optimal decisions?*

Your stateless independent (micro)service CAN easiy and efficiently be
expressed for {marathon, swarm, k8s}. And it should be!

## Control planes

**Reality** is people are (already) building software that operated distributed
systems. Common pattern: ad-hoc control planes

**Goal: provide distributed systems as SaaS**

- What happens if there's a bug in the control plane?
- What if my control plane has diverged from yours?
- What happens when a new realease of the distributed system invalidates an
  assumption the control plane previously made?

## A better world...

- **Control planes should be built into distributed systems itself by the
  experts who built the distributed system in the first place!**
- As an industry, we should strive to build a standard interface distributed
  systems can leverage
- Vice-versa: abstractions exist for good reasons, ...

# Conclusion

- How do we scale the operations of dsitributed systems?
- Let them **scale** themselves!

- Operating systems are for 2 people: people using it, but also for software
- A lot of tools that has been done in the past were built to empower *people*
  to do stuff, but it should just be the machine that does it itself

# Scaling out (Postgre)SQL

## Speaker

- Marco Slot
- Principal Software Engineer at Citus Data
- https://www.citusdata.com/
- marco@citusdata.com
- https://twitter.com/marcoslot
- https://github.com/marcocitus

## Why SQL?

- Learned that scalable DBs are not SQL DBs
- Things could be simpler

- Before : SQL DB => (SELECT ...) => Application
- Now : Streaming => Storage => Map/Reduce => NoSQL => Application

- If data is stored in a NoSQL store, we need to deploy some new systems
  (spark, k/v storage...) for our app to work with it.

## About SQL Databases

- SQL databases
    - are general-purpose data platforms
    - are Very powerufl!
- But they don't scale :(
- Actually, the proble, is not that they don't scale, but that they're **hard**
  to scale

## Why hard to scale?

- How do you take a SQL query and distribute it to many servers in a
  distributed system ?
- SQL <=> relational algebra
- Main thing we need to add : `FROM sharded_table` .... `Collect(R1, R2, ...)` =>
  `R'`. It's a Gather operation
- Relational algebra, commutativity, etc.

## PostgreSQL

- Citus
- dblink
- PostGIS
- PL/Python
- Replication
- Indexes
- JSONB
- 2 Phase Commit
- Sequences
- Transactinos
- Full-text Search

## Conclusion

**PostgreSQL is becoming and extensible, scalable general-purpose data
platform**

- How PostgreSQL fits in the NewSQL tendencies?
- 20 years work on it
- Indexes in postgres are incredibly powerful

# Lightning talks

- A few lightning talks were just too fast. One was on implementing graph data
  structures in Redis

## Use multiple cloud platforms to increase profit (LT by Algolia)

- Every business has ONE goal: make money
- Increase income, reduce cost
- One thing in your job they don't tell you: save money!

### How can I know what/how to reduce?

4 easy steps :

- Collect billing data
    - AWS: Cost Explorer
    - GCP: Export billing to bigquery
    - Azure: ... something :D
- Monitor this data
- Alert on this data
- Reduce. (how?)

### How can I reduce cost?

- Reserved instances
- MsgPack
- CDN
- Trusted Advisor
- Spot instances
- Preemptible failure

### Conclusion

- Design for failure
- DNS - LB - ASG - Cache - DB = Standard.
- => Use multiple cloud providers
- DNS to LB between providers

## A short introduction on interval tree clocks (LT by Pierre Chapuis)

- causality => version vector
- dynamic system => actio explosion => ITC

Idea:

- Instead of locks attributing unique IDs, we attribute intervals
- New device => Take an existing device, and fork it, and split
  the interval
- Event occurs => We increase the hight of the curve in our interval
- Compare curves height on our interval.
- Device leave => Merge information in the informations of another device, and
  then give back our share of the interval to the other system.

See more on https://github.com/catwell/itc.lua
