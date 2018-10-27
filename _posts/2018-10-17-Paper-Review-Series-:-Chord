Chord is a scalable protocol for lookup service in a dynamic peer-to-peer system with frequent node arrivals and departures. Chord is meaningful as efficient location is import in a decentralised system. The paper discussed he system model
that motivates the Chord protocol and proved several of its properties. It also addressed handling of concurrent joins and leaves. Finally it examined experiment results.
Strengths:
1. Basically the idea of the lookup algorithm Chord uses is like binary search. Nodes form a topological ring. Each node, instead of storing information about all other nodes, stores only nodes of double distance away on the ring. To look up the node for some key, hop to the nearest predecessor and halve the distance to the target node. It's proven that with high probability, in logarithmic times of iterations the search will converge. This lookup algorithm makes Chord highly scalable and  lookup performance improved.
2. The “stabilization” protocol, which is all nodes periodically checks its successors' updatedness, guarantees correctness of lookups in case of nodes joining and leaving. It makes fully decentralised system, no master node or hierarchical nodes, and no need global awareness.
3. The look up algorithm is simple and proven correct.
Weakness:
1. Since Chord disregard the physical network topology and assume hops between any nodes are of same cost, a search that involves hops between nodes that are residing far away in the network can be very costly.
