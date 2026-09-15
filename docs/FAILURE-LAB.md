# Phase 3 — Destroy the path, watch OSPF think

Prerequisite: Phase 2 healthy (FULL neighbors, PC-A pings PC-C).

## Experiment 1 — Shut R1–R2 link

On **R1**:

```text
interface GigabitEthernet0/1
 shutdown
```

### Ask yourself

- What happens to the OSPF adjacency?  
- What disappears from `show ip route`?  
- Can PC-A still reach PC-C? *(In this linear topology: no alternate path.)*  
- How fast does the neighbor go **DOWN**?

### Capture

| Command | Before | After shutdown | After `no shutdown` |
| --- | --- | --- | --- |
| `show ip ospf neighbor` | | | |
| `show ip route` | | | |
| PC-A `ping 10.3.3.10` | | | |

Restore:

```text
interface GigabitEthernet0/1
 no shutdown
```

Wait for FULL; confirm ping returns. That delay is **convergence**.

## Experiment 2 — Shut R2–R3 link

Repeat from R2 or R3 on `10.1.23.0/30`. Same questions.

## What you should be able to say aloud

> When the link drops, OSPF tears down the adjacency, withdraws routes learned over that neighbor, and the remote LAN disappears from the RIB until the link and adjacency recover. With only one path, traffic fails until convergence restores that path.

Optional stretch (not required): add a second path R1—R3 and watch OSPF pick a new next hop after a failure — classic multi-path intuition.
