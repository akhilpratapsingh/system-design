# Promxy and Sharding

## Why Promxy?

Promxy is a prometheus proxy that makes many shards of prometheus appear as a single API endpoint to the user. This significantly simplifies operations and use of prometheus at scale (when you have more than one prometheus host). Promxy delivers this unified access endpoint without requiring any sidecars, custom-builds, or other changes to your prometheus infrastructure.
- Advantages:  
  - Query Federation
  - Single Endpoint
  - Remote Write ability to `destination`
  - Recording Rules
  - Alerting Rules

## Promxy based Sharding  
How was the Sharding achieved?  
Discuss Prometheus Sharding?

## Sharding Logic  
- Base CPU per rule
- Base Memory per rule
- determine the total recording rules and complexity
- configure HPA
- configure prometheus shards

