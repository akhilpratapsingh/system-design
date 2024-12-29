# Challenging Project
## Situation
  Describe Setup
  - Project involves pulling customers application metrics.
  - Customer's application metrics are deployed in vms.
  - The vms produce metrics to /metrics endpoint.
  - Metrics are scraped by prometheus pod.
    - Prometheus collects and stores its metrics as time series data, i.e. metrics information is stored with the timestamp at which it was recorded, alongside optional key-value pairs called labels.
  - Whitelisted metrics are scraped and written to timeseries database, m3db. <todo> What are the advantages of having timeseries database vs relational database?

For customers with relatively smaller metric loads, vertically scaling prometheus pods provided some relief, but those customers whose requirement couldn't be met with vertical scaling a single instance, were complaining about the product not meeting their scale-requirements:
- Ability to federate queries.
  - This posed problems in creating centralized dashboards, where in all the results of all prometheus instances could be aggregated. A centralized dashboard was absent thus making observability and telemetry a pain point.
  - Global queries, for the customers with sharded prometheuses, were an issue. e.g. count all 4xx instances across all scraped targets of a given application.
- Query Latency was a major concern among customers with applications who were not using prometheus recording rules.
  - My Team wasn't able to offer prometheus recording rules because of non-centralized query federation, thus contributing to query latency.
- Didn't have the ability to automatically shard the prometheus pods s.t. the prometheus pods scale up and down based on params e.g. cpu-utilization and memory-utilization
  - The absence of automatic sharding caused frequent incidents & escalations and made the OnCall burden worse.
  - My team handled this via manuall tweaking the allocated prometheus cpu and memory. This proved cumbersome to maintain and support.
 
## Task
- Provide customers with large metrics volume and cardinality a way to:
  - centralized query federation to all their prometheuses
  - Move away from manual sharding to automatic sharding based on CPU/Memory utilization metrics.   
## Action
- Initial deliberation and research resulted in a requirement for a centralized query federation tool.
  - Upon research I found that for addressing query federation, I can use a project promxy[prometheus-proxy].
  - I setup a small use-case on a dev k8s cluster and started experimenting w.r.t. query federation.
    ### Challenges
    - I was new to tech-stack and took time to ramp-up on:
      - kubebuilder
      - reconciliation based on controllers
      - golang syntax and semantics
      - setup and testing
    - Dublin team was rolled off and new team from IDC was hired
      - Significant ramp up challenge, coupled with timezone challenges caused us to stretch.
      - Tech stack ramp up the IDC Team
      - Team's leadership and customer's were still expecting the product launch to stay intact.
## Result
- This enabled our customers to:
  - query federation
  - automatic sharding
  - observability and telemetry
  - reduced oncall burden of my team.
  - overall costs reduction since we were able to work with 
