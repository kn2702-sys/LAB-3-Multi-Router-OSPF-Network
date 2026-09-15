# Verification matrix

## Phase 1 — Static

| Check | Where | Expect |
| --- | --- | --- |
| `ping 10.3.3.10` | PC-A | Success |
| `ping 10.1.1.10` | PC-C | Success |
| `show ip route` | R1 | `S 10.3.3.0/24 via 10.1.12.2` |
| `show ip route` | R3 | `S 10.1.1.0/24 via 10.1.23.1` |
| `show ip route` | R2 | Statics to both LANs |

## Phase 2 — OSPF

Run on each router:

```text
show ip ospf neighbor
show ip route
show ip protocols
show ip ospf database
```

| Check | Expect |
| --- | --- |
| R1 neighbor | R2 in state **FULL** |
| R3 neighbor | R2 in state **FULL** |
| R1 route to LAN-C | `O 10.3.3.0/24` via `10.1.12.2` |
| R3 route to LAN-A | `O 10.1.1.0/24` via `10.1.23.1` |
| `show ip protocols` | OSPF 1, RID matches table, networks listed |
| End-to-end | PC-A ↔ PC-C still works |

### Healthy neighbor sample (shape)

```text
Neighbor ID     State           Address         Interface
2.2.2.2         FULL/  -        10.1.12.2       GigabitEthernet0/1
```

Exact DR/BDR columns vary by PT version and network type; **FULL** is the bar.
