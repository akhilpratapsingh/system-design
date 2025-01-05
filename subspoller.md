# SubsPoller & Sharding
## Situation
- The deployment process for onboarding metrics was manual and very cumbersome. It involved hand wiring subscriptions with their metadata e.g. metrics-names to be pulled in a yaml file.
- For small projects this was manageable but for high-volume subscription teams e.g. platform team, this process was cumbersome.
- The CI process(kitt) didn't allow for deploying more than 10 such files at a time, which made managing the project very busy work and prone to error.
- For those providerTypes, where high count subscriptions were present, we manually sharded them down into parts such that they could be deployed without exceeding pod cpu and OOMing.
- This manual processes made the onboarding slow and operational burden for the team.
## Task
## Action
## Result
>Azure Exporter:
>Azure exporter is a project which helps pulling azure metrics for our customers..

Why SubsPoller?
> Customers with high subscription count and large number of metrics couldn't be handled manually via updating the yaml files.
> When metrics metadata were updated/edited, it would incur additional manual change, which was time-consuming and error prone.
> I put forward a design to automatically shard the metrics, provided by the customer.
> Design
>
> Supporting Infrastructure:
>
> Advantages:
> >
