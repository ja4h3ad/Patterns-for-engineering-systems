# Search State Level by Level

```text
Start at a node
        ↓
Add it to the FIFO queue
        ↓
Remove the next queued node
        ↓
Check whether it is the target
        ↓
Queue each unvisited neighbor
        ↓
Repeat until found or the queue is empty
```

The queue stores nodes waiting to be searched together with the path used to reach each node. The visited set ensures that each node is queued at most once.

## State Invariants

- The queue is first in, first out (FIFO).
- Nodes are processed in order of increasing distance from the start.
- A node is marked as visited when it is queued.
- If the target is reached, its stored path is a shortest path in an unweighted graph.

## Time Efficiency

**O(V + E)**

Where:

- `V` is the number of vertices.
- `E` is the number of edges.

Each reachable vertex is queued and removed at most once, and each outgoing edge is examined at most once. This notebook copies the current path when queuing a neighbor, so path construction adds extra time and memory beyond the core breadth-first search traversal.

## Typical Engineering Patterns

Breadth-first search appears in systems that explore relationships in layers or need a shortest path when every step has equal cost.

Examples include:

- Dependency analysis
- Network routing by hop count
- Social connection discovery
- Web crawling
- File and directory traversal
- Workflow state exploration
- Unweighted maze solving
- Nearest-resource lookup

## AI Applicability

AI systems can use breadth-first search to explore a bounded state or relationship graph while preserving the shortest chain of steps.

Example questions:

- What is the shortest sequence of tool actions from the current state to a goal state?
- What is the smallest number of relationships connecting two concepts?
- Which reachable option is closest to the agent's current state?
