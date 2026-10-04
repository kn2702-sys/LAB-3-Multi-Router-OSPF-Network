# Build order (Packet Tracer)

Estimated time: 60–90 minutes across both phases.

## Devices

| Device | Role |
| --- | --- |
| R1, R2, R3 | Routers (2911 / 1941 / ISR) |
| PC-A | Host on LAN-A |
| PC-C | Host on LAN-C |

## Cabling

| From | To | Network |
| --- | --- | --- |
| PC-A Fa0 | R1 Gi0/0 | `10.1.1.0/24` |
| R1 Gi0/1 | R2 Gi0/0 | `10.1.12.0/30` |
| R2 Gi0/1 | R3 Gi0/1 | `10.1.23.0/30` |
| PC-C Fa0 | R3 Gi0/0 | `10.3.3.0/24` |

## Host IP

| Host | IP | Mask | Gateway |
| --- | --- | --- | --- |
| PC-A | `10.1.1.10` | `/24` | `10.1.1.1` |
| PC-C | `10.3.3.10` | `/24` | `10.3.3.1` |

## Sequence

1. Cable and set host IPs.  
2. Load **PHASE1** configs on R1 → R2 → R3.  
3. Verify with [`VERIFICATION.md`](VERIFICATION.md) Phase 1.  
4. Load **PHASE2** configs (or manually `no ip route` then `router ospf`).  
5. Verify OSPF neighbors and `O` routes.  
6. Run [`FAILURE-LAB.md`](FAILURE-LAB.md).  
7. Save screenshots under `assets/screenshots/`.

The working `Lab-3-OSPF-Network.pkt` topology is committed in the repo root.
