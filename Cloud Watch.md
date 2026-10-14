---
type: service
section: fundamentals
certs: [CLF, SAA, DVA, SOA]
tags: [infrastructure, observability, fundamentals]
---
# Cloud Watch

Collects and manages operational data. Cloud Watch includes:
- [[Metric]] - AWS Products, Apps, or On-premises.
- Cloud Watch [[Log]] - AWS Products, Apps, or On-premises.
- Cloud Watch [[Event]]s - AWS Services & Schedules

When you need to collect [[metric]]s or [[log]]s from on-premises, or from outside AWS, or something that AWS does not exposed by default, you need to install [[Cloud Watch Agent]].

Cloud Watch has [[metric]]s, [[alarm]], and [[statistic]]
- Metrics are collections of related data point in a time-ordered structure.
- Alarms are configured based on metrics
- Statistics are aggregated from metrics

[[Namespace]] is a container for monitoring data. All AWS data will go to `AWS/<service>` namespace, for example `AWS/EC2`.

To aggregate, or to filter the metrcis, we can use [[dimension]]s. AWS sends Instance ID and Instance Type by default.