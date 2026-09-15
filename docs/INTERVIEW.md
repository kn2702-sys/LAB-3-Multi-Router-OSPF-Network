# Interview answers (LAB 3)

### What is OSPF?
Open Shortest Path First — a link-state IGP. Routers flood LSAs, build a topology map, and run SPF (Dijkstra) to choose best paths. In this lab, all links are in **Area 0**.

### Why prefer OSPF over static routing in larger networks?
Statics do not adapt. Every new network means manual routes on many boxes. OSPF discovers neighbors, advertises networks, and **reconverges** when a link fails — less human error at scale.

### What is an OSPF neighbor?
A router that has completed OSPF adjacency on a shared link (Hello parameters match, reach **FULL**). Check with `show ip ospf neighbor`. No neighbor → no OSPF routes from that peer.

### What happens when a route / link goes down?
OSPF detects loss (Hello dead interval / interface down), adjacency drops, LSAs update, SPF reruns, and affected routes are removed or replaced. End-to-end traffic fails until an alternate path exists or the link returns.

### What does administrative distance mean?
Trust ranking of routing sources on the same router. **Lower AD wins** when multiple protocols offer the same prefix. Example Cisco defaults: Connected 0 · Static **1** · OSPF **110**. That is why leftover statics can hide OSPF routes if you forget to delete them in Phase 2.
