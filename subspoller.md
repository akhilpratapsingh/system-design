**SubsPoller & Sharding**

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
