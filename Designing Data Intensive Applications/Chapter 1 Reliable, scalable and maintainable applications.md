
# Introduction

Many applications today are data-intensive, as opposed to compute-intensive. Raw CPU power is rarely a limiting factor for these applications - bigger problems are usually the amount of data, the complexity of data, and the speed at which it is changing.

Note: databases, queues, caches, etc. we think of them as being very different categories of tools. Although a database and message queue have some superficial similarity both store data for some time.
	(((only different implementation)))
Therefore refer them as data systems

# Reliablity

Few points to sum up reliability
1. The application performs the functions that user expected.
2. It can tolerate user making mistakes or using software in unexpected ways.
3. Its performance is good enough for required use-case, under the expected load.
4. The system prevents any unauthorised access & abuse.

*The Things that can go wrong are called faults and the system that can cope with these faults are called fault-tolerant or resilient*

```bash
example: Netflix chaos monkey
it is used to stress test cloud infrastructure by purposely injecting failures
```

# Hardware Faults

Hardware failures are gonna be there (specially when working with large datacenters) hard disk crash, faulty RAM, power grid blackout, unplugging wrong network cable

Also note Hard Disks are reported as having a mean time to failure (MTTF) of about 10-50 years

But hardware faults are not generally connected (except cases like let's say natural disaster or extreme high server temperature can cause a chain of failures)

# Software Errors

As hardware faults are more random and independent not the case with **Software errors** they tend to cause many more system failures.

*For example a leap second on June 30 2012 caused many applications to hang simultaneously due to a bug in the linux kernel*

# Human Errors

Self explanatory

# Scalability

One common reason for degradation is increased load
**Scalability** is a term we use to describe a system's ability to cope with the increased load.

**Load??**
The best definition for load depends on the architecture of your system
 1. Requests per second (for web)
 2. Ratio of reads to write (In a Db)
 3. Number of simultaneously active users (in a chat room)
 4. Hit rate (in case of cache)
