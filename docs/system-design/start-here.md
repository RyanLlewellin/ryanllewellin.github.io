# Quick Start

https://github.com/donnemartin/system-design-primer

## [Steps to Approaching a Question](https://github.com/donnemartin/system-design-primer#how-to-approach-a-system-design-interview-question)

### 1. Gather requirements and scope the problem
 - Who's using it?
 - How are they using it?
 - How many are using it?

 ### 2. Create a high level design
 - Sketch out all the components

 ### 3. Design core components
 - Dive into each component of the previous step with more details

 ### 4. Scale
 - Load balancer
 - Horizontal & Vertical scaling
   - Horizontal is adding more machines to existing pool of resources ("Scaling out")
   - Vertical is adding more power (CPU, RAM) to an existing machine ("Scaling Up") [Usually easier and cheaper]
- Caching
- Database sharding
  - Splits a single dataset into partitions (shards)
  - Each shard contains unique rows of information that you can store separately across multiple computers, called nodes. 
  - All shards run on separate nodes but share the original database's schema or design.


### 5. 