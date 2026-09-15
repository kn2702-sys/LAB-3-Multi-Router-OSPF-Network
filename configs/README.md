# Configs

| Folder | Use when |
| --- | --- |
| `PHASE1-static/` | First bring-up — prove end-to-end with static routes |
| `PHASE2-ospf/` | Replace statics with OSPF Area 0 |

Paste into each router CLI in Packet Tracer. If your PT model labels interfaces `FastEthernet`, rename only the interface names — keep IPs identical.

Wildcard reminder: `/24` → `0.0.0.255` · `/30` → `0.0.0.3`
