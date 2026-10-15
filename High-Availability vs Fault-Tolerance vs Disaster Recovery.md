---
type: concept
section: fundamentals
certs: [CLF, SAA, DVA, SOA]
tags: [infrastructure, concept, fundamentals]
---
# High-Availability vs Fault-Tolerance vs Disaster Recovery

[[High-Availability]] or HA aims to ensure an agreed level of operational **performance**, usually **uptime**, for a higher than normal periods. --> Minimize the [[outages]]

[[Fault-Torlerance]] or FT is the property that **enables** a system to **continue operating** properly in the event of the failure of some (one or more faults within) of its components. --> What means to operate through failure. FT can be more expensive or more complicated than HA.

[[Disaster Recovery]] or DR is a set of policies, tools and procedures to **enable the recovery** or **continuation** of **vital** technology and subsystems, **following a natural  or human-induced disaster**.

## Differences Between HA, FT, and DR

### High Availability (HA)

- **Goal**: Minimize downtime.
- **Disruptions**: Brief user disruptions are acceptable.
- **Cost**: Lower implementation cost compared to FT.

### Fault Tolerance (FT)

- **Goal**: Continue operating through failures.
- **Disruptions**: No user disruption during failure.
- **Cost**: More expensive and complex than HA.

### Disaster Recovery (DR)

- **Goal**: Recover from a major disaster when HA and FT fail.
- **Disruptions**: Recovery after failure; may require human intervention.
- **Cost**: Can vary based on the level of preparedness and automation.

## Importance for Solutions Architects

As an AWS Solutions Architect, it is essential to **understand the differences** between HA, FT, and DR to design the appropriate solutions for your customers:

- **HA**: Suitable when brief user disruptions are acceptable, and the focus is on minimizing downtime.
- **FT**: Needed for critical systems that must operate without interruption, even in the face of component failures.
- **DR**: Necessary for **recovery planning** when major disasters occur, ensuring business continuity.